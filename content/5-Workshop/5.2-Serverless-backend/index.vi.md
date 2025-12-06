---
title: "Phần 2: Triển khai Backend với API Gateway, Lambda, RDS và Cognito"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

## Giới thiệu

Chào mừng bạn đến với phần thứ hai trong chuỗi workshop xây dựng ứng dụng serverless của chúng tôi! Trong phiên thực hành này, bạn sẽ xây dựng một cơ sở hạ tầng backend hoàn chỉnh, bảo mật cho ứng dụng serverless của mình bằng cách sử dụng các dịch vụ được quản lý (managed services) của AWS.

Sau đó, bạn sẽ học cách kết nối backend serverless này với frontend mà chúng ta đã xây dựng trước đó ở Phần 1.

Các ứng dụng hiện đại yêu cầu hệ thống backend mạnh mẽ, có khả năng mở rộng để xử lý logic nghiệp vụ, quản lý dữ liệu an toàn và xác thực người dùng. Trong workshop này, bạn sẽ tạo ra một kiến trúc backend hoàn toàn serverless sử dụng AWS Lambda để tính toán, Amazon RDS để lưu trữ dữ liệu bền vững, API Gateway cho các RESTful API, Amazon Cognito để xác thực người dùng và AWS Secrets Manager để quản lý thông tin xác thực một cách bảo mật.

![Sơ đồ](/images/5-Workshop/diagram.png)

### Những gì bạn sẽ xây dựng

Kết thúc phần này, bạn sẽ triển khai được một cơ sở hạ tầng backend hoàn chỉnh bao gồm:

- **RESTful APIs**: Các endpoint API Gateway xử lý các yêu cầu HTTP và định tuyến chúng đến các Lambda function thích hợp.
- **Điện toán Serverless**: Các Lambda function được viết bằng Node.js/Python để thực thi logic nghiệp vụ của bạn.
- **Cơ sở dữ liệu được quản lý**: Cơ sở dữ liệu Amazon RDS PostgreSQL để lưu trữ dữ liệu tin cậy.
- **Xác thực Người dùng**: Amazon Cognito user pools cho việc đăng ký, đăng nhập và quản lý người dùng.
- **Bảo mật API**: Cognito authorizers bảo vệ các API endpoint của bạn.
  Hơn nữa, thực thi quy tắc buộc API Gateway chỉ chấp nhận các yêu cầu bắt nguồn từ CloudFront.
- **Quản lý Bí mật**: AWS Secrets Manager lưu trữ an toàn thông tin đăng nhập cơ sở dữ liệu và tạo ra một giá trị bảo mật để nhúng vào custom header của CloudFront nhằm hạn chế quyền truy cập vào API Gateway.
- **Bảo mật Mạng**: Cấu hình VPC để cô lập cơ sở dữ liệu của bạn khỏi internet công cộng.

### Tại sao lại chọn Kiến trúc này?

Kiến trúc backend serverless này mang lại một số lợi ích chính:

- **Không cần quản lý máy chủ**: AWS xử lý việc cung cấp tài nguyên, cập nhật bản vá và mở rộng quy mô.
- **Trả tiền theo mức sử dụng**: Chỉ trả tiền cho thời gian tính toán và dung lượng lưu trữ thực tế được sử dụng.
- **Tự động mở rộng**: Tự động xử lý lượng truy cập tăng đột biến từ 0 đến hàng nghìn yêu cầu.
- **Bảo mật tích hợp sẵn**: Nhiều lớp bảo mật bao gồm IAM, Cognito, VPC và quản lý bí mật.
- **Năng suất lập trình viên**: Tập trung vào viết code, không phải lo về cơ sở hạ tầng.

### Thời lượng Workshop

**Thời gian ước tính**: 3-4 giờ

- Thiết lập VPC và mạng: 20 phút
- Tạo cơ sở dữ liệu RDS: 30 phút
- Cấu hình Secrets Manager: 15 phút
- Phát triển Lambda function: 45 phút
- Thiết lập API Gateway: 40 phút
- Cấu hình Cognito: 45 phút
- Tích hợp và kiểm thử: 45 phút

## Cấu trúc Workshop

Workshop này được chia thành các phần sau:

### **Phần 1: Thiết lập VPC và Mạng**

- Tạo VPC để cô lập cơ sở dữ liệu
- Cấu hình subnets (chúng ta sẽ thiết lập 1 Availability Zone cho workshop này)
- Thiết lập security groups để truy cập cơ sở dữ liệu

### **Phần 2: Thiết lập Cơ sở dữ liệu RDS**

- Tạo RDS PostgreSQL instance
- Cấu hình các tham số cơ sở dữ liệu
- Tạo schema và các bảng cơ sở dữ liệu
- Thiết lập user và quyền hạn cơ sở dữ liệu

### **Phần 3: Cấu hình AWS Secrets Manager**

- Lưu trữ thông tin xác thực cơ sở dữ liệu một cách an toàn
- Cấu hình xoay vòng bí mật (tùy chọn)
- Cấp quyền cho Lambda truy cập bí mật
- Tạo VPC Endpoint để Lambda gọi AWS Secrets Manager
- Tạo role cho Lambda để truy cập vào RDS và AWS Secrets Manager

### **Phần 4: Phát triển Lambda Functions**

- Tạo Lambda execution role với các quyền phù hợp
- Viết các Lambda function cho các thao tác CRUD
- Đóng gói và triển khai Lambda function
- Cấu hình biến môi trường (environment variables)
- Kết nối Lambda với RDS thông qua VPC
- Kiểm thử Lambda

### **Phần 5: Thiết lập API Gateway**

- Tạo REST API
- Định nghĩa các resource và method
- Cấu hình tích hợp Lambda proxy
- Thiết lập CORS để tích hợp frontend
- Triển khai API đến một stage

### **Phần 6: Cấu hình Amazon Cognito**

- Tạo Cognito user pool
- Cấu hình thuộc tính người dùng và chính sách (policies)
- Thiết lập app client cho ứng dụng của bạn
- Cấu hình domain cho user pool
- Kiểm thử đăng ký và xác thực người dùng

### **Phần 7: Bảo mật API với Cognito**

- Tạo Cognito authorizer trong API Gateway
- Bảo mật các API endpoint bằng xác thực
- Kiểm thử các lệnh gọi API đã xác thực
- Xử lý authorization tokens trong Lambda

### **Phần 8: Kiểm thử Tích hợp**

- Kiểm thử các endpoint không yêu cầu xác thực
- Kiểm thử các endpoint yêu cầu xác thực với token
- Xác minh các thao tác cơ sở dữ liệu
- Kiểm thử xử lý lỗi
- (Tùy chọn) Tích hợp với frontend từ Phần 1: Triển khai Frontend

### **Phần 9: Giám sát và Ghi log**

- Xem CloudWatch Logs của Lambda
- Giám sát các chỉ số (metrics) của API Gateway
- Theo dõi hoạt động người dùng trên Cognito
- Thiết lập cảnh báo CloudWatch

### **Phần 10: Dọn dẹp**

- Xóa các tài nguyên theo đúng thứ tự
- Xác minh việc loại bỏ chi phí
- Lưu các cấu hình để sử dụng trong tương lai
