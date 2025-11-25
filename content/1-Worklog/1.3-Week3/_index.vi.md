---
title: "Week 3 Worklog"
date: "2025-09-20"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu của Tuần 3:

- Hoàn thành các lab AWS quan trọng, bao gồm Site-to-Site VPN và các thao tác cơ bản với EC2.
- Học và hoàn thành đầy đủ bốn module của khóa AWS Cloud Technical Essentials.
- Nâng cao kỹ năng sử dụng AWS Console và AWS CLI (quản lý credential, key pairs, khám phá region và service).
- Phối hợp với đội product/design để phân tích và ghi chú UI/UX của TypeRush từ bản thiết kế Figma.
- Đánh giá các phương án lưu trữ và đưa ra quyết định sử dụng NoSQL cho TextService.
- Thử nghiệm tích hợp MongoDB (tạo môi trường, seeding, refactor service, kiểm thử).
- Xây dựng thói quen trao đổi và cộng tác hiệu quả với team First Cloud Journey.

### Các công việc đã thực hiện trong tuần:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Start Date | Completion Date | Reference Material                                                                                                     |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 2   | - **Lab 03:** AWS Site-to-Site VPN: <br>&emsp; + Xây dựng đầy đủ môi trường Site-to-Site VPN gồm VPC mới, EC2 đóng vai Customer Gateway, Virtual Private Gateway và VPN Connection. <br>&emsp; + Cấu hình và kiểm tra kết nối đường hầm VPN. <br><br> - **Lab 04:** Amazon EC2 Fundamentals: <br>&emsp; + Khởi tạo và kết nối EC2 Windows Server và Amazon Linux. <br>&emsp; + Triển khai ứng dụng CRUD "AWS User Management" trên cả Windows và Linux. <br>&emsp; + Khám phá các tính năng EC2: thay đổi type, quản lý snapshot EBS, tạo custom AMI.                                                                                                                                                                                                            | 09/22/2025 | 09/22/2025      | VPN Lab (Lab 03): <br> https://000003.awsstudygroup.com/ <br> EC2 Lab (Lab 04): <br> https://000004.awsstudygroup.com/ |
| 3   | - Bắt đầu khóa AWS Cloud Technical Essentials và hoàn thành 2 module đầu: <br>&emsp; + **Module 1:** Cloud Foundations & IAM <br>&emsp;&emsp; - Định nghĩa cloud computing và giá trị của nó. <br>&emsp;&emsp; - So sánh workload on-premise và workload trên cloud. <br>&emsp;&emsp; - Tạo tài khoản AWS và tìm hiểu các cách tương tác (Console/CLI/SDK). <br>&emsp;&emsp; - Tìm hiểu Global Infrastructure (Region, AZ). <br>&emsp;&emsp; - Học và áp dụng best practices của IAM. <br>&emsp; + **Module 2:** Compute & Networking <br>&emsp;&emsp; - Tìm hiểu kiến trúc EC2. <br>&emsp;&emsp; - Phân biệt container và virtual machine. <br>&emsp;&emsp; - Khám phá serverless và các trường hợp sử dụng. <br>&emsp;&emsp; - Tìm hiểu VPC và tạo custom VPC. | 09/23/2025 | 09/23/2025      | AWS Cloud Technical Essentials: <br> https://www.coursera.org/learn/aws-cloud-technical-essentials                     |
| 4   | - Phối hợp với team design để tài liệu hóa UI/UX TypeRush: <br>&emsp; + Tham gia buổi review cross-functional để xem xét toàn bộ flow Figma mới. <br>&emsp; + Phân tích các màn hình chính (login, game, score, settings) để hiểu bố cục, visual hierarchy và user interaction. <br>&emsp; + Ghi lại danh sách câu hỏi kỹ thuật và các điểm cần xác thực với design. <br>&emsp; + Bắt đầu chuyển thiết kế thành yêu cầu component và user stories phục vụ cho sprint sau. <br><br> - Thảo luận hướng lưu trữ TextService với team lead: <br>&emsp; + So sánh mô hình lưu trữ SQL và NoSQL dựa trên cấu trúc dữ liệu và cách truy cập. <br>&emsp; + Trình bày ưu/nhược điểm và case sử dụng. <br>&emsp; + Chốt sử dụng NoSQL vì linh hoạt và dễ mở rộng.          | 09/24/2025 | 09/24/2025      |                                                                                                                        |
| 5   | - Tích hợp và thử nghiệm MongoDB cho prototype TextService: <br>&emsp; + Dựng môi trường MongoDB bằng Docker. <br>&emsp; + Điều chỉnh script seeding để insert tài liệu (words/sentences) vào collection. <br>&emsp; + Refactor TextService để đọc/ghi qua MongoDB. <br>&emsp; + Kiểm thử đầy đủ để xác nhận kết nối và luồng dữ liệu hoạt động đúng.                                                                                                                                                                                                                                                                                                                                                                                                            | 09/25/2025 | 09/25/2025      |                                                                                                                        |
| 6   | - Hoàn thành 2 module cuối của AWS Cloud Technical Essentials: <br>&emsp; + **Module 3:** Storage & Databases <br>&emsp;&emsp; - Phân biệt file storage, block storage và object storage. <br>&emsp;&emsp; - Tìm hiểu Amazon S3, tạo S3 bucket. <br>&emsp;&emsp; - Tìm hiểu EBS và các dịch vụ database của AWS. <br>&emsp;&emsp; - Tạo DynamoDB table. <br>&emsp; + **Module 4:** Monitoring & High Availability <br>&emsp;&emsp; - Tìm hiểu CloudWatch và các lợi ích khi monitoring. <br>&emsp;&emsp; - Học cách tối ưu hiệu suất và chi phí. <br>&emsp;&emsp; - Tìm hiểu cơ chế ELB phân phối lưu lượng. <br>&emsp;&emsp; - Phân biệt scaling up và scaling out, triển khai mô hình high availability.                                                       | 09/26/2025 | 09/26/2025      | AWS Cloud Technical Essentials: <br> https://www.coursera.org/learn/aws-cloud-technical-essentials                     |

### Thành tựu Tuần 3:

- **Hoàn tất các AWS Labs:**

  - Xây dựng Site-to-Site VPN hoàn chỉnh (VPC, EC2 gateway, virtual private gateway, cấu hình tunnel).
  - Hoàn thiện EC2 fundamentals: chạy Windows/Linux, deploy CRUD app, quản lý snapshot, tạo custom AMI.

- **Hoàn thành toàn bộ 4 module của AWS Cloud Technical Essentials**  
  (Cloud Foundations/IAM, Compute & Networking, Storage & Databases, Monitoring & High Availability).

- **Nâng cao kỹ năng AWS Console & CLI:**

  - Quản lý tài khoản, IAM credentials.
  - Điều hướng service/region thành thạo hơn.
  - Thao tác với key pair và các lệnh CLI để kiểm tra tài nguyên.

- **Tài liệu hóa UI/UX TypeRush:**

  - Review toàn bộ flow trên Figma.
  - Ghi nhận trạng thái component và câu hỏi khả thi kỹ thuật.
  - Soạn các user story và yêu cầu ban đầu.

- **Chiến lược lưu trữ TextService:**

  - Đánh giá SQL vs NoSQL.
  - Quyết định sử dụng NoSQL để tăng tính linh hoạt và khả năng mở rộng.

- **Prototype MongoDB:**
  - Dựng môi trường Docker.
  - Viết lại script seeding.
  - Refactor service sang MongoDB.
  - Kiểm thử toàn bộ luồng đọc/ghi dữ liệu.
