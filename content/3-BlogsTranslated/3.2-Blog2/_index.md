---
title: "Blog 2"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Create an SSL connection to Amazon RDS for Db2 in Java without KeyStore or Keytool

> by Vikram Khatri, Amine Yahsine, Ashish Saraswat, and Sumit Kumar

This article outlines a simplified method for establishing a secure SSL database connection in Java, specifically for Amazon Relational Database Service (Amazon RDS) for Db2. The approach allows developers to bypass the traditional complexities associated with the `keytool` utility and the management of Java KeyStores. The primary benefits of this technique include its simplicity, its suitability for automated environments like CI/CD pipelines, and its ability to maintain strong security through proper TLS 1.2 negotiation and server certificate validation.

---

## Solution Overview

Instead of relying on a traditional Java TrustStore, this solution leverages a specific configuration property supported by the IBM JDBC driver. The driver can be instructed to use a PEM-formatted server certificate directly, which eliminates the need to convert the certificate or import it into a `.jks` file.

This is accomplished by setting the `sslCertLocation` property:

```java
properties.put("sslCertLocation", "/path/to/certchain.pem");
```

To ensure the connection is encrypted and uses a secure protocol, the following JDBC driver connection properties must also be set:

```java
sslConnection=true
sslVersion=TLSv1.2
```

This method is particularly well-suited for cloud environments like AWS, where Amazon RDS provides a PEM-formatted certificate bundle. The solution was tested with an IBM Db2 JDBC Driver (`db2jcc4.jar` v4.33.31), Java 11+, and a PEM certificate from Amazon RDS.

---

## Prerequisites

Before implementing this solution, the following resources are assumed to be in place:

- An Amazon RDS for Db2 server instance with SSL already enabled.
- A certificate chain PEM file, such as the region-specific `us-east-1-bundle.pem` available for download from AWS.
- A recent version of the IBM Data Server Driver (`db2jcc4.jar` version 4.33 or later).
- Java 8 or higher, with support for TLS 1.2.

---

## The Java Program

The full source code for a Java program (`Db2SSLTest.java`) that connects to Amazon RDS for Db2 using this SSL method is provided below:

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

## Compile and Run

Assuming the IBM JDBC driver is located at `~/sqllib/java/db2jcc4.jar`, the following shell script illustrates how to compile and run the Java program. The script also includes a function to retrieve the database password from AWS Secrets Manager or prompt the user for it manually.

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

## Considerations

There is a limitation in the JDBC driver (at the time of writing) that prevents the use of a global certificate bundle (like `global-bundle.pem`) with the `sslCertLocation` property. If an application connects to a single AWS Region, it is recommended to use a region-specific certificate file (e.g., `us-east-1-bundle.pem`). If there is an absolute requirement to use the global bundle, developers must revert to the traditional method of using `keytool` to store the certificates in a keystore.

---

## Troubleshooting

The following are solutions to common issues:

- **Failing SSL connection:** If the SSL connection fails after being enabled in the RDS for Db2 instance, the instance must be restarted. The SSL enablement only takes effect after a restart.
- **Unable to locate the `db2jcc4.jar` file:** This file is included with various IBM DB2 client packages, such as the data server client or runtime client.
- **Unable to connect to the RDS database:** If a connection fails after cataloging a database with SSL using `db2cli` commands, there might be an existing database connection that is not aware of the newly cataloged database. The `db2 terminate` command should be used to close existing connections before testing again.

---

## Conclusion

This post demonstrates that it is not always necessary to use the Java KeyStore or `keytool` utility to enable SSL connections. With a PEM certificate and a modern JDBC driver, a secure connection can be established with minimal setup. This approach is especially valuable for developers who need to perform rapid SSL testing, for automated environments such as CI/CD and containers, and for anyone looking to simplify secure Java-to-Db2 connectivity.
