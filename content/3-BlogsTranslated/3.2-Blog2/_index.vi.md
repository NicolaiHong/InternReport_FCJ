---
title: "Blog 2"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Tạo kết nối SSL tới Amazon RDS for Db2 trong Java không cần KeyStore hoặc Keytool

> bởi Vikram Khatri, Amine Yahsine, Ashish Saraswat, and Sumit Kumar

Bài viết này trình bày một phương pháp đơn giản hóa để thiết lập kết nối cơ sở dữ liệu bảo mật SSL trong Java dành cho Amazon Relational Database Service (Amazon RDS) for Db2. Cách tiếp cận này cho phép developer bỏ qua độ phức tạp truyền thống liên quan tới tiện ích `keytool` và việc quản lý Java KeyStore (JKS). Lợi ích chính: đơn giản, phù hợp môi trường tự động hóa như CI/CD pipelines, và vẫn duy trì bảo mật mạnh thông qua thương lượng TLS 1.2 đúng chuẩn và xác thực chứng chỉ máy chủ.

---

## Tổng quan giải pháp

Thay vì dựa vào một Java TrustStore truyền thống, giải pháp này tận dụng một thuộc tính cấu hình đặc thù do IBM JDBC Driver hỗ trợ. Driver có thể được chỉ định dùng trực tiếp chứng chỉ máy chủ định dạng PEM, loại bỏ nhu cầu chuyển đổi hoặc import vào file `.jks`.

Điều này được thực hiện bằng cách thiết lập thuộc tính `sslCertLocation`:

```java
properties.put("sslCertLocation", "/path/to/certchain.pem");
```

Để đảm bảo kết nối được mã hóa và dùng giao thức an toàn, cần đặt thêm các thuộc tính kết nối JDBC driver sau:

```java
sslConnection=true
sslVersion=TLSv1.2
```

Phương pháp này đặc biệt phù hợp môi trường đám mây như AWS, nơi Amazon RDS cung cấp một bundle chứng chỉ định dạng PEM. Giải pháp đã được kiểm thử với IBM Db2 JDBC Driver (`db2jcc4.jar` v4.33.31), Java 11+, và chứng chỉ PEM từ Amazon RDS.

---

## Điều kiện tiên quyết

Trước khi triển khai, giả định bạn đã có:

- Một instance Amazon RDS for Db2 với SSL đã bật.
- File chuỗi chứng chỉ PEM (ví dụ: `us-east-1-bundle.pem` theo vùng, tải từ AWS).
- Phiên bản mới của IBM Data Server Driver (`db2jcc4.jar` phiên bản 4.33 hoặc mới hơn).
- Java 8 hoặc cao hơn, hỗ trợ TLS 1.2.

---

## Chương trình Java

Mã nguồn đầy đủ của chương trình Java (`Db2SSLTest.java`) kết nối tới Amazon RDS for Db2 bằng phương pháp SSL này:

```java
import java.sql.*;
import java.util.Properties;
public class Db2SSLTest {
  public static void main(String[] args) {
    if (args.length != 6) {
      System.out.println("Usage: java Db2SSLTest " +
        " <certchain.pem> " +
        "  <hostname> <port> <database> <userid> <password>");
      System.exit(1);
    }
    Properties properties = new Properties();
    String certPath = args[0];
    String hostname = args[1];
    String port = args[2];
    String database = args[3];
    String userid = args[4];
    String password = args[5];
    properties.put("sslConnection", "true");
    properties.put("sslVersion", "TLSv1.2");
    properties.put("sslCertLocation", certPath);
    properties.put("user", userid);
    properties.put("password", password);
    String url = "jdbc:db2://" + hostname + ":" +
        port + "/" + database;
    try {
      Class.forName("com.ibm.db2.jcc.DB2Driver");
      Connection conn = DriverManager.getConnection(url,
                          properties);
      Statement stmt = conn.createStatement();
      ResultSet rs = stmt.executeQuery("SELECT CURRENT " +
          " TIMESTAMP " +
          " FROM SYSIBM.SYSDUMMY1");
      if (rs.next()) {
        System.out.println("SSL Connection successful!");
        System.out.println("Current timestamp: " +
           rs.getString(1));
      }
      rs.close();
      stmt.close();
      conn.close();
    } catch (Exception e) {
      System.err.println("Error: " + e.getMessage());
      e.printStackTrace();
    }
  }
}
```

---

## Biên dịch và chạy

Giả sử IBM JDBC driver nằm tại `~/sqllib/java/db2jcc4.jar`, script shell dưới đây minh họa cách biên dịch và chạy chương trình Java. Script cũng có hàm lấy mật khẩu DB từ AWS Secrets Manager hoặc nhắc người dùng nhập tay.

```bash
#!/usr/bin/env bash
# Retrieves the master user password for a specified DB instance.
# This function attempts to obtain the master user password for the provided
# DB instance ID. It first checks if the password can be retrieved from the
# AWS Secrets Manager. If a valid secret is not found, it prompts the user
# to manually enter the password.
#
# Args:
#     DB_INSTANCE_ID (str): The database instance identifier.
#
# Environment Variables:
#     REGION: The AWS region where the DB instance is located.
#
# Exports:
#     MASTER_USER_PASSWORD: The retrieved or entered master user password.
#
# Returns:
#     int: Returns 1 if the password retrieval fails, otherwise 0.
get_master_password() {
 DB_INSTANCE_ID=$1
 SECRET_ARN=$(aws rds describe-db-instances \
 --db-instance-identifier "$DB_INSTANCE_ID" \
 --region $REGION \
 --query "DBInstances[0].MasterUserSecret.SecretArn" \
 --output text)
 if [[ -z "$SECRET_ARN" || "$SECRET_ARN" == "None" ]]; then
   read -rsp "Enter Master User password: " MASTER_USER_PASSWORD
   echo
 else
   SECRET_JSON=$(aws secretsmanager get-secret-value \
     --secret-id "$SECRET_ARN" \
     --query "SecretString" \
     --region $REGION \
     --output text)
   MASTER_USER_PASSWORD=$(jq -r '.password' <<< "$SECRET_JSON")
   if [[ -z "$MASTER_USER_PASSWORD" ]]; then
     echo "Failed to get password from secret manager '$SECRET_ARN'. Exiting..."
     return 1
   fi
   export MASTER_USER_PASSWORD=$MASTER_USER_PASSWORD
 fi
}
# Retrieves the master user name for a specified DB instance.
#
# This function queries AWS RDS to obtain the master user name for the provided
# DB instance identifier. If the master user name is not found, it returns an
# error message.
#
# Environment Variables:
#     DB_INSTANCE_IDENTIFIER: The database instance identifier.
#     REGION: The AWS region where the DB instance is located.
#
# Exports:
#     MASTER_USER_NAME: The retrieved master user name.
#
# Returns:
#     int: Returns 1 if the master user name is not found, otherwise 0.
get_master_user_name() {
 local master_user_name=($(aws rds describe-db-instances \
   --db-instance-identifier "$DB_INSTANCE_IDENTIFIER" \
   --region $REGION \
   --query "DBInstances[0].MasterUsername" \
   --output text))
 if [ "$master_user_name" = "None" ]; then
   echo "Not found"
   return 1
 else
   export MASTER_USER_NAME=$master_user_name
 fi
}
# Retrieves the database address for a specified DB instance.
#
# This function queries AWS RDS to obtain the database endpoint address for the
# provided DB instance identifier. If the address is not found, it returns an
# error message.
#
# Environment Variables:
#     DB_INSTANCE_IDENTIFIER: The database instance identifier.
#     REGION: The AWS region where the DB instance is located.
#
# Exports:
#     DB_ADDRESS: The retrieved database endpoint address.
#
# Returns:
#     int: Returns 1 if the database address is not found, otherwise 0.
get_db_address() {
 local db_address=($(aws rds describe-db-instances \
   --db-instance-identifier "$DB_INSTANCE_IDENTIFIER" \
   --region $REGION \
   --query "DBInstances[0].Endpoint.Address" \
   --output text))
 if [ -z "$db_address" ]; then
   echo "Not found"
   return 1
 else
   export DB_ADDRESS=$db_address
 fi
}
# Retrieves the SSL port number for a specified DB instance.
#
# This function queries AWS RDS to obtain the parameter group name associated
# with the provided DB instance identifier, and then queries the parameter
# group to obtain the SSL port number. If the SSL port is not found, it returns
# an error message.
#
# Environment Variables:
#     DB_INSTANCE_IDENTIFIER: The database instance identifier.
#     REGION: The AWS region where the DB instance is located.
#
# Exports:
#     SSL_PORT: The retrieved SSL port number.
#
# Returns:
#     int: Returns 1 if the SSL port is not found, otherwise 0.
get_ssl_port() {
 SSL_PORT=""
 DB_PARAM_GROUP_NAME=$(aws rds describe-db-instances \
     --db-instance-identifier "$DB_INSTANCE_IDENTIFIER" \
     --region $REGION \
     --query "DBInstances[0].DBParameterGroups[0].DBParameterGroupName" \
     --output text)
 if [ "$DB_PARAM_GROUP_NAME" != "" ]; then
   SSL_PORT=$(aws rds describe-db-parameters \
       --db-parameter-group-name "$DB_PARAM_GROUP_NAME" \
       --region $REGION \
       --query "Parameters[?ParameterName=='ssl_svcename'].ParameterValue" \
       --output text)
   if [ "$SSL_PORT" = "None" ]; then
     SSL_PORT=""
     return 1
   fi
 fi
 export SSL_PORT=$SSL_PORT
 return 0
}
# Main entry point for the script.
#
# This function compiles a Java program, downloads the SSL certificate, retrieves
# the master user name, master password, database address, and SSL port from AWS
# RDS, and then runs the Java program with the retrieved parameters.
#
# Exports:
#     None
#
# Returns:
#     int: Returns 0 if the program runs successfully, otherwise 1.
main () {
 DB_INSTANCE_IDENTIFIER="viz-demo"
 CL_PATH=.:$HOME/sqllib/java/db2jcc4.jar
 REGION="us-east-1"
 PROG_NAME=Db2SSLTest
 JAVA_FILE=${PROG_NAME}.java
 DBNAME="TEST"
 if ! command -v javac &>/dev/null; then
   echo "javac is not installed. Please install Java Development Kit (JDK) to compile Java programs."
   exit 1
 fi
 echo "Compile Java program $JAVA_FILE"
 javac -cp $CL_PATH $JAVA_FILE
 echo "Downloading SSL certificate..."
 CERTCHAIN="/home/db2inst1/us-east-1-bundle.pem"
 if [ -f "$CERTCHAIN" ]; then
   echo "Certificate already exists. Skipping download."
 else
   echo "Certificate does not exist. Downloading..."
   if ! curl -sL "https://truststore.pki.rds.amazonaws.com/us-east-1/$REGION-bundle.pem" -o $REGION-bundle.pem; then
     echo "Failed to download SSL certificate. Please check your network connection or the URL."
     exit 1
   fi
 fi
 if get_master_user_name "$DB_INSTANCE_IDENTIFIER"; then
   echo "Master user name: $MASTER_USER_NAME"
   USER="$MASTER_USER_NAME"
 else
   echo "Failed to retrieve master user name. Exiting..."
   exit 1
 fi
 if get_master_password "$DB_INSTANCE_IDENTIFIER"; then
   PASSWORD=$MASTER_USER_PASSWORD
 else
   echo "Failed to retrieve master password. Exiting..."
   exit 1
 fi
 if get_db_address "$DB_INSTANCE_IDENTIFIER"; then
   echo "DB Address: $DB_ADDRESS"
   HOST="$DB_ADDRESS"
 else
   echo "Failed to retrieve DB address. Exiting..."
   exit 1
 fi
 if get_ssl_port "$DB_INSTANCE_IDENTIFIER"; then
   echo "SSL Port: $SSL_PORT"
   PORT="$SSL_PORT"
 else
   echo "Failed to retrieve SSL port. Exiting..."
   exit 1
 fi
 # Use -Djavax.net.debug=ssl:handshake:verbose to debug SSL issues
 echo "Running Java program..."
 java \
 -cp "$CL_PATH" $PROG_NAME $CERTCHAIN $HOST $PORT $DBNAME $USER $PASSWORD
}
main "$@"
```

---

## Lưu ý

Hiện có một hạn chế trong JDBC driver (tại thời điểm viết) ngăn việc sử dụng global certificate bundle (như `global-bundle.pem`) với thuộc tính `sslCertLocation`. Nếu ứng dụng chỉ kết nối một AWS Region, nên dùng file chứng chỉ theo vùng (ví dụ: `us-east-1-bundle.pem`). Nếu bắt buộc phải dùng global bundle, developer cần quay lại phương pháp truyền thống với `keytool` để lưu chứng chỉ vào keystore.

---

## Xử lý sự cố

Một số vấn đề thường gặp và cách xử lý:

- Failing SSL connection: Sau khi bật SSL trên instance RDS for Db2, cần khởi động lại instance; việc bật chỉ có hiệu lực sau restart.
- Không tìm thấy `db2jcc4.jar`: File nằm trong các gói IBM DB2 client khác nhau (data server client / runtime client).
- Không kết nối được RDS database: Nếu lỗi sau khi catalog database với SSL qua lệnh `db2cli`, có thể còn kết nối cũ chưa nhận metadata mới. Chạy `db2 terminate` để đóng kết nối rồi thử lại.

---

## Kết luận

Bài viết cho thấy không phải lúc nào cũng cần Java KeyStore hoặc tiện ích `keytool` để bật kết nối SSL. Với chứng chỉ PEM và JDBC driver hiện đại, có thể thiết lập kết nối bảo mật với cấu hình tối thiểu. Cách tiếp cận này đặc biệt giá trị cho developer cần thử nghiệm SSL nhanh, môi trường tự động như CI/CD và container, hoặc bất kỳ ai muốn đơn giản hóa kết nối bảo mật Java → Db2.
