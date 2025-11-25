---
title: "Week 4 Worklog"
date: "2025-09-29"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:

- Nắm vững cấu hình Amazon RDS, bao gồm thiết lập VPC, security group và quản lý backup.
- Học triển khai ứng dụng web có khả năng mở rộng bằng Auto Scaling Group và Application Load Balancer.
- Củng cố kỹ năng giám sát với CloudWatch: metrics, logs, alarms và dashboard tùy chỉnh.
- Tìm hiểu mô hình DNS lai sử dụng Route 53 Resolver trong môi trường doanh nghiệp.
- Thành thạo AWS CLI để quản lý tài nguyên S3, EC2, VPC và IAM.
- Xây dựng pipeline CI/CD hoàn chỉnh với CodeCommit, CodeBuild, CodeDeploy và CodePipeline.
- Thiết lập chiến lược backup tự động bằng AWS Backup và lifecycle policy.
- Triển khai ứng dụng container với Docker và container registry trên AWS.
- Tìm hiểu quy trình di chuyển máy ảo (VM) gồm import và export giữa các môi trường.
- Xây dựng ứng dụng serverless bằng AWS Lambda và API Gateway.
- Hiểu hệ thống giám sát bảo mật tập trung bằng AWS Security Hub.

### Các nhiệm vụ đã hoàn thành trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Bắt đầu    | Hoàn thành | Tài liệu tham khảo                   |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | ---------- | ------------------------------------ |
| 2    | - **Cấu hình và quản lý Amazon RDS:** <br>&emsp; + Thiết lập VPC, security group và DB subnet group <br>&emsp; + Tạo EC2 và RDS instance <br>&emsp; + Deploy ứng dụng mẫu kết nối RDS <br>&emsp; + Thực hiện backup và restore <br>&emsp; + Dọn dẹp tài nguyên <br><br> - **Triển khai ứng dụng có khả năng mở rộng:** <br>&emsp; + Cấu hình VPC, subnet và security group <br>&emsp; + Tạo Launch Template <br>&emsp; + Tạo Target Group và ALB <br>&emsp; + Tạo Auto Scaling Group với chính sách manual / scheduled / dynamic <br>&emsp; + Dọn tài nguyên <br><br> - **Giám sát với CloudWatch:** <br>&emsp; + Phân tích metrics bằng search và math expression <br>&emsp; + Query logs bằng Logs Insights <br>&emsp; + Tạo Metric Filter <br>&emsp; + Tạo Alarm <br>&emsp; + Xây dashboard <br>&emsp; + Xóa alarms và dashboards | 29/09/2025 | 29/09/2025 | RDS, Auto Scaling, CloudWatch Labs   |
| 3    | - **Triển khai DNS lai với Route 53 Resolver:** <br>&emsp; + Deploy hạ tầng bằng CloudFormation <br>&emsp; + Tạo Microsoft AD mô phỏng DNS on-prem <br>&emsp; + Tạo outbound & inbound endpoint <br>&emsp; + Cấu hình rule chuyển tiếp DNS <br>&emsp; + Kiểm tra phân giải 2 chiều và dọn tài nguyên <br><br> - **Quản lý AWS bằng CLI:** <br>&emsp; + Cài đặt và cấu hình AWS CLI <br>&emsp; + Quản lý S3, SNS, IAM bằng CLI <br>&emsp; + Thao tác bucket và object <br>&emsp; + Tạo và quản lý VPC bằng CLI <br>&emsp; + Tạo và xoá EC2 bằng CLI <br>&emsp; + Dọn tài nguyên                                                                                                                                                                                                                                                       | 30/09/2025 | 30/09/2025 | Route 53 Resolver, AWS CLI Labs      |
| 4    | - **Xây dựng pipeline CI/CD tự động:** <br>&emsp; + Tạo repo CodeCommit <br>&emsp; + Cấu hình CodeBuild để build và package app <br>&emsp; + Tạo CodeDeploy để tự động deploy <br>&emsp; + Dùng CodePipeline để điều phối toàn bộ quy trình <br>&emsp; + Test bằng cách push code <br>&emsp; + Dọn tài nguyên <br><br> - **Tự động hóa backup EC2 bằng AWS Backup:** <br>&emsp; + Deploy hạ tầng bằng CloudFormation <br>&emsp; + Tạo backup plan với lifecycle policy <br>&emsp; + Cấu hình thông báo backup <br>&emsp; + Test backup & restore <br>&emsp; + Xoá stack và backup                                                                                                                                                                                                                                                    | 01/10/2025 | 01/10/2025 | CodePipeline, AWS Backup Labs        |
| 5    | - **Triển khai ứng dụng Docker trên AWS:** <br>&emsp; + Tạo VPC, security group, IAM role <br>&emsp; + Tạo RDS instance <br>&emsp; + Deploy ứng dụng bằng Docker image <br>&emsp; + Triển khai lại bằng Docker Compose <br>&emsp; + Push image lên ECR / Docker Hub <br>&emsp; + Xóa tài nguyên <br><br> - **Di chuyển máy ảo (VM Import/Export):** <br>&emsp; + Export VM từ on-prem <br>&emsp; + Upload image lên S3 <br>&emsp; + Import thành AMI <br>&emsp; + Tạo EC2 từ AMI <br>&emsp; + Export EC2 trở lại S3 <br>&emsp; + Xóa toàn bộ                                                                                                                                                                                                                                                                                         | 02/10/2025 | 02/10/2025 | Docker on AWS, VM Import/Export Labs |
| 6    | - **Triển khai ứng dụng serverless:** <br>&emsp; + Chuẩn bị package Lambda <br>&emsp; + Tạo IAM role cho Lambda <br>&emsp; + Deploy Lambda function <br>&emsp; + Tạo HTTP API và tích hợp Lambda <br>&emsp; + Deploy và test endpoint <br>&emsp; + Xóa API, Lambda, IAM role <br><br> - **Giám sát bảo mật tập trung với Security Hub:** <br>&emsp; + Enable Security Hub <br>&emsp; + Xem dashboard và findings <br>&emsp; + Phân tích phát hiện từ GuardDuty, Inspector, Macie <br>&emsp; + Xem biểu đồ rủi ro                                                                                                                                                                                                                                                                                                                     | 03/10/2025 | 03/10/2025 | Lambda & Security Hub Labs           |

### Thành tựu Tuần 4:

- Cấu hình thành công Amazon RDS cùng toàn bộ networking và backup.
- Xây dựng hạ tầng Auto Scaling + ALB cho ứng dụng mở rộng.
- Hoàn thiện giám sát CloudWatch với metrics, logs, alarms, dashboards.
- Cấu hình DNS lai với Route 53 Resolver + Microsoft AD.
- Thành thạo AWS CLI cho nhiều dịch vụ khác nhau.
- Xây dựng pipeline CI/CD tự động đầy đủ.
- Thiết lập backup tự động theo lifecycle với AWS Backup.
- Deploy ứng dụng Docker và publish image lên ECR.
- Hoàn tất quy trình di chuyển VM import/export.
- Xây dựng ứng dụng serverless với Lambda + API Gateway.
- Giám sát bảo mật tập trung bằng Security Hub.
