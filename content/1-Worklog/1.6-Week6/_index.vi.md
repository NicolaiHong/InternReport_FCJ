---
title: "Nhật ký công việc Tuần 6"
date: "2025-11-26"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Học cách quản lý quyền truy cập EC2 bằng IAM, sử dụng tag tài nguyên và permission boundaries.
- Thiết lập và cấu hình công cụ giám sát như Grafana và AWS CloudWatch.
- Triển khai AWS Systems Manager để quản lý bản vá và thực thi lệnh từ xa.
- Tối ưu hóa EC2 bằng thực hành right-sizing và AWS Compute Optimizer.
- Áp dụng mã hóa cho dữ liệu S3 bằng AWS KMS và cấu hình ghi nhật ký kiểm toán.
- Phân tích chi phí và mô hình sử dụng AWS bằng Cost Explorer.
- Xây dựng pipeline và data lake sử dụng S3, Kinesis, Glue, Athena và QuickSight.
- Tự động hóa provisioning hạ tầng bằng template AWS CloudFormation.

### Công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                                                                                   |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 2    | - **Quản lý truy cập dịch vụ EC2 bằng tag tài nguyên thông qua IAM:** <br>&emsp; + Tạo một IAM user để chuẩn bị <br>&emsp; + Tạo một custom IAM Policy để xác định quyền cụ thể <br>&emsp; + Thiết lập một IAM Role để user hoặc dịch vụ có thể assume <br>&emsp; + Kiểm tra policy bằng cách đổi role và thử truy cập <br> <br> - **Bắt đầu với Grafana cơ bản:** <br>&emsp; + Tạo VPC và subnet để thiết lập môi trường mạng <br>&emsp; + Cấu hình Security Group để kiểm soát lưu lượng vào/ra <br>&emsp; + Khởi chạy một EC2 instance để host ứng dụng giám sát <br>&emsp; + Tạo IAM User và Role để truy cập an toàn tài nguyên AWS <br>&emsp; + Gán IAM Role cho EC2 instance <br>&emsp; + Cài đặt Grafana trên EC2 instance <br>&emsp; + Thiết lập dashboard giám sát trong Grafana                                                                                                                                             | 10/13/2025   | 10/13/2025      | IAM services: <br> <https://000028.awsstudygroup.com/> <br> Grafana basic: <br> <https://000029.awsstudygroup.com/>                  |
| 3    | - **Giới hạn quyền người dùng với IAM Permission Boundary:** <br>&emsp; + Thực hiện các bước chuẩn bị cho bài tập <br>&emsp; + Tạo một policy hạn chế để định nghĩa quyền lớn nhất được cho phép <br>&emsp; + Tạo một IAM user mới với quyền bị giới hạn <br>&emsp; + Kiểm tra giới hạn của IAM user để xác minh permission boundary <br> <br> - **Quản lý bản vá và chạy lệnh trên nhiều server bằng AWS Systems Manager:** <br>&emsp; + Tạo VPC và Subnet cho môi trường mạng <br>&emsp; + Khởi chạy một EC2 Windows công khai <br>&emsp; + Tạo một IAM Role với quyền cần thiết <br>&emsp; + Gán IAM Role cho EC2 instance <br>&emsp; + Cấu hình và sử dụng Patch Manager để quản lý vá <br>&emsp; + Dùng Run Command để thực thi lệnh trên các server                                                                                                                                                                              | 10/14/2025   | 10/14/2025      | IAM permission boundary: <br> <https://000030.awsstudygroup.com/> <br> AWS Systems Manager: <br> <https://000031.awsstudygroup.com/> |
| 4    | - **Thực hiện best practice right-sizing cho Amazon EC2:** <br>&emsp; + Làm quen với Amazon CloudWatch để giám sát <br>&emsp; + Tạo và gán IAM Role cho CloudWatch Agent <br>&emsp; + Cài đặt CloudWatch Agent trên EC2 instance <br>&emsp; + Sử dụng AWS Compute Optimizer để phân tích và tối ưu cấu hình EC2 <br> <br> - **Mã hóa dữ liệu lưu trữ tại S3 bằng AWS KMS:** <br>&emsp; + Tạo các IAM policy, role, group và user cần thiết <br>&emsp; + Thiết lập một KMS key <br>&emsp; + Tạo bucket S3 và upload dữ liệu <br>&emsp; + Cấu hình AWS CloudTrail để ghi nhật ký và sử dụng Amazon Athena để truy vấn dữ liệu <br>&emsp; + Kiểm tra và chia sẻ dữ liệu đã được mã hóa trên S3                                                                                                                                                                                                                                            | 10/15/2025   | 10/15/2025      | EC2 right-sizing: <br> <https://000032.awsstudygroup.com/> <br> S3 encryption with KMS: <br> <https://000033.awsstudygroup.com/>     |
| 5    | - **Trực quan hóa và phân tích chi phí bằng AWS Cost Explorer:** <br>&emsp; + Xem dữ liệu chi phí và sử dụng theo dịch vụ và theo tài khoản <br>&emsp; + Phân tích phạm vi và hiệu quả của Savings Plans và Reserved Instances <br>&emsp; + Đánh giá tính co giãn chi phí (cost elasticity) <br>&emsp; + Tạo báo cáo tùy chỉnh cho các instance EC2 <br>&emsp; + Dùng Cost Explorer để phân tích chi tiết chi phí <br>&emsp; + Kiểm tra chi phí truyền dữ liệu cho các kiến trúc phổ biến <br> <br> - **Xây dựng data lake trên AWS:** <br>&emsp; + Tạo IAM Role và Policy với quyền cần thiết <br>&emsp; + Thiết lập bucket S3 để lưu trữ dữ liệu <br>&emsp; + Tạo Kinesis Data Firehose delivery stream để thu thập dữ liệu <br>&emsp; + Dùng Glue Crawler để tạo data catalog <br>&emsp; + Thực hiện chuyển đổi dữ liệu <br>&emsp; + Phân tích dữ liệu bằng Amazon Athena <br>&emsp; + Trực quan hóa dữ liệu bằng Amazon QuickSight | 10/16/2025   | 10/17/2025      | AWS Cost Explorer: <br> <https://000034.awsstudygroup.com/> <br> Data lake on AWS: <br> <https://000035.awsstudygroup.com/>          |
| 6    | - **Nghiên cứu AWS CloudWatch cho giám sát và observability:** <br>&emsp; + Khám phá CloudWatch Metrics: xem, tìm kiếm và sử dụng expressions <br>&emsp; + Làm việc với CloudWatch Logs, Logs Insights và Metric Filters <br>&emsp; + Cấu hình CloudWatch Alarms để gửi thông báo <br>&emsp; + Tạo CloudWatch Dashboards để trực quan hóa dữ liệu <br> <br> - **Tự động hóa hạ tầng bằng AWS CloudFormation:** <br>&emsp; + Tạo IAM Users và Roles để chuẩn bị <br>&emsp; + Phát triển template CloudFormation cơ bản để provision tài nguyên <br>&emsp; + Khám phá các tính năng nâng cao như Custom Resources với Lambda <br>&emsp; + Sử dụng Mappings, StackSets và Drift Detection cho các triển khai phức tạp                                                                                                                                                                                                                     | 10/17/2025   | 10/17/2025      | AWS CloudWatch: <br> <https://000036.awsstudygroup.com/> <br> AWS CloudFormation: <br> <https://000037.awsstudygroup.com/>           |

### Thành tựu tuần 6:

- Quản lý truy cập EC2 qua IAM:
  - Cấu hình chính sách truy cập dựa trên tag tài nguyên
  - Áp dụng permission boundaries để giới hạn khả năng của người dùng
- Thiết lập hệ thống giám sát và observability:
  - Triển khai Grafana trên EC2 để tạo dashboard tùy chỉnh
  - Cấu hình CloudWatch Metrics, Logs và Alarms để giám sát tài nguyên
- Triển khai khả năng của AWS Systems Manager:
  - Sử dụng Patch Manager để tự động cập nhật bản vá cho server
  - Thực thi lệnh từ xa trên nhiều instance bằng Run Command
- Ứng dụng tối ưu hóa EC2 và quản lý chi phí:
  - Cài và cấu hình CloudWatch Agent để thu thập metric chi tiết
  - Phân tích cấu hình instance bằng AWS Compute Optimizer
  - Xem xét mẫu chi phí và xu hướng bằng Cost Explorer
- Bảo mật lưu trữ dữ liệu bằng mã hóa:
  - Tạo và quản lý KMS key cho mã hóa S3
  - Thiết lập CloudTrail và dùng Athena cho phân tích nhật ký kiểm toán
- Xây dựng pipeline và data lake:
  - Cấu hình Kinesis Data Firehose để ingest dữ liệu streaming
  - Tạo data catalog bằng Glue Crawler
  - Phân tích dữ liệu bằng Athena và trực quan hóa bằng QuickSight
- Tự động hóa triển khai hạ tầng bằng CloudFormation:
  - Phát triển template để provisioning tài nguyên
  - Khám phá các tính năng nâng cao như Lambda-backed custom resources và StackSets
