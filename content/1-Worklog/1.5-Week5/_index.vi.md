---
title: "Week 5 Worklog"
date: "2025-10-10"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu Tuần 5:

- Triển khai các kỹ thuật networking nâng cao với VPC Peering và Transit Gateway để kết nối nhiều VPC.
- Deploy ứng dụng full-stack sử dụng EC2, RDS, Auto Scaling và tích hợp CloudFront.
- Xây dựng giải pháp tối ưu chi phí bằng serverless với AWS Lambda để tự động quản lý EC2.
- Thiết lập pipeline CI/CD bằng bộ công cụ AWS Developer Tools cho quá trình deploy tự động.
- Cấu hình hybrid cloud storage bằng AWS Storage Gateway để kết nối môi trường on-premises.
- Quản lý hệ thống file doanh nghiệp bằng Amazon FSx và tăng cường bảo mật web bằng AWS WAF.
- Tổ chức tài nguyên AWS hiệu quả với Tags và Resource Groups.
- Nâng cao kỹ năng thao tác bằng cả AWS Management Console và AWS CLI.

---

### Nhiệm vụ đã thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Bắt đầu    | Hoàn thành | Tài liệu tham khảo                                                                                           |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ------------------------------------------------------------------------------------------------------------ |
| 2    | - **Thiết lập VPC Peering giữa hai VPC:**<br> + Khởi tạo môi trường bằng CloudFormation<br> + Tạo Security Group cho EC2<br> + Khởi tạo EC2 ở từng VPC để kiểm tra kết nối<br> + Cập nhật Network ACLs<br> + Tạo & chấp nhận kết nối Peering<br> + Cấu hình Route Tables để định tuyến<br> + Bật Cross-Peer DNS để resolve tên miền<br><br> - **Triển khai kiến trúc mạng mở rộng với Transit Gateway:**<br> + Tạo Key Pair<br> + Khởi tạo môi trường bằng CloudFormation<br> + Tạo Transit Gateway làm trung tâm kết nối<br> + Gắn các VPC vào Transit Gateway<br> + Cấu hình Transit Gateway Route Tables<br> + Cập nhật Route Tables của VPC | 10/06/2025 | 10/06/2025 | VPC Peering: <https://000019.awsstudygroup.com/> <br> Transit Gateway: <https://000020.awsstudygroup.com/>   |
| 3    | - **Triển khai WordPress trên AWS:**<br> + Chuẩn bị VPC/Subnet<br> + Tạo Security Group cho EC2 và RDS<br> + Tạo EC2 host WordPress<br> + Tạo RDS cho database<br> + Cài đặt và cấu hình WordPress<br> + Thiết lập Auto Scaling<br> + Thực hiện backup/restore database<br> + Tích hợp CloudFront để tăng tốc hiệu năng<br><br> - **Tối ưu chi phí EC2 bằng Lambda:**<br> + Gắn tags cho EC2 để quản lý chi phí<br> + Tạo IAM Role cho Lambda<br> + Viết Lambda tự động tắt/bật EC2<br> + Kiểm thử hoạt động của Lambda                                                                                                                         | 10/07/2025 | 10/07/2025 | WordPress: <https://000021.awsstudygroup.com/> <br> Lambda Optimization: <https://000022.awsstudygroup.com/> |
| 4    | - **Tự động hoá triển khai ứng dụng với CI/CD Pipeline:**<br> + Chuẩn bị tài nguyên cần thiết<br> + Cài đặt CodeDeploy Agent lên EC2<br> + Tạo repo CodeCommit lưu mã nguồn<br> + Cấu hình CodeBuild để build ứng dụng<br> + Thiết lập CodeDeploy để deploy tự động<br> + Xây dựng CodePipeline orchestrate toàn bộ pipeline<br> + Xử lý lỗi trong quá trình chạy pipeline<br><br> - **Sử dụng Storage Gateway cho hybrid cloud:**<br> + Tạo S3 Bucket<br> + Tạo EC2 host Storage Gateway<br> + Khởi tạo Storage Gateway<br> + Tạo File Shares<br> + Mount File Shares trên máy on-premises                                                     | 10/08/2025 | 10/08/2025 | CI/CD: <https://000023.awsstudygroup.com/> <br> Storage Gateway: <https://000024.awsstudygroup.com/>         |
| 5    | - **Quản lý Amazon FSx for Windows File Server:**<br> + Tạo môi trường<br> + Tạo file system SSD và HDD Multi-AZ<br> + Tạo file shares<br> + Kiểm thử hiệu năng<br> + Bật Data Deduplication & Shadow Copies<br> + Quản lý sessions, open files, quotas<br> + Bật Continuous Access share<br> + Scale throughput và storage<br> + Xoá môi trường khi hoàn tất<br> + Tham khảo AWS CLI để quản lý FSx<br><br> - **Triển khai AWS WAF:**<br> + Tạo S3 bucket và deploy web mẫu<br> + Sử dụng Managed Rules<br> + Tạo Custom Rules nâng cao<br> + Kiểm thử rule<br> + Bật logging<br> + Cleanup tài nguyên                                         | 10/09/2025 | 10/09/2025 | Amazon FSx: <https://000025.awsstudygroup.com/> <br> AWS WAF: <https://000026.awsstudygroup.com/>            |
| 6    | - **Quản lý tài nguyên bằng Tags & Resource Groups:**<br> + Hiểu và sử dụng tags trên Console<br> + Tạo EC2 với tags<br> + Thêm/xoá tags trên resource<br> + Lọc tài nguyên theo tags<br> + Sử dụng tags với AWS CLI<br> + Gắn tags cho EC2 qua CLI<br> + Gắn tags khi tạo mới tài nguyên bằng CLI<br> + Liệt kê tài nguyên có tag bằng CLI<br> + Tạo Resource Group dựa trên tags<br> + Quản lý tài nguyên trong Resource Group                                                                                                                                                                                                                | 10/10/2025 | 10/10/2025 | Tags & Resource Groups: <https://000027.awsstudygroup.com/>                                                  |

---

### Thành tựu Tuần 5:

- Hoàn thiện networking nâng cao trên AWS:

  - VPC Peering giúp kết nối trực tiếp giữa các VPC
  - Transit Gateway làm trung tâm kết nối toàn hệ thống
  - Cấu hình routing và DNS giữa nhiều VPC

- Deploy và tối ưu ứng dụng cloud:

  - WordPress tích hợp RDS
  - Auto Scaling + CloudFront tăng hiệu năng và tính sẵn sàng
  - Lambda tối ưu chi phí EC2 tự động

- Xây dựng quy trình DevOps hoàn chỉnh:

  - Pipeline CI/CD đầy đủ với CodeCommit – CodeBuild – CodeDeploy – CodePipeline
  - Tự động hoá triển khai
  - Hybrid storage bằng Storage Gateway

- Quản lý hệ thống file và bảo mật ở cấp doanh nghiệp:

  - FSx Multi-AZ, quản lý quotas, deduplication
  - AWS WAF với quản lý rule nâng cao

- Áp dụng chiến lược quản trị tài nguyên hiệu quả:

  - Tối ưu chi phí & quản lý bằng Tags
  - Quản lý tài nguyên tập trung bằng Resource Groups
  - Thao tác chuyên sâu bằng Console & CLI

- Trải nghiệm thực tế với Infrastructure as Code thông qua CloudFormation để tạo môi trường nhất quán.
