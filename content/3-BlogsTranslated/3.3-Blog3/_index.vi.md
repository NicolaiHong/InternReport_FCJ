---
title: "Blog 3"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Nâng cao trải nghiệm kiểm thử cục bộ cho các ứng dụng serverless với LocalStack

> by Patrick Galvin and Debasis Rath

Bài viết này giới thiệu và giải thích các khả năng mới được thiết kế để đơn giản hóa trải nghiệm kiểm thử cục bộ cho ứng dụng serverless. Thông qua tích hợp với **AWS Partner**, **LocalStack**, **AWS Toolkit for Visual Studio Code** nay cung cấp một cách tinh gọn hơn để developer build, test và debug ứng dụng serverless mà không phải rời môi trường phát triển.

---

## Thách thức với phát triển Local Serverless

Mặc dù kiến trúc serverless nhìn chung đơn giản trong vận hành và mở rộng, quá trình phát triển và kiểm thử có thể tạo ra ma sát làm chậm vòng lặp code–test–debug. Developer thường gặp một số trở ngại phổ biến:

- **Slow Iteration from Cloud-Based Validation:** Trước đây phải deploy các template AWS Serverless Application Model (AWS SAM) lên cloud chỉ để test thay đổi, làm chậm đáng kể vòng phản hồi.
- **Friction from Tool Context Switching:** Việc phải chuyển đổi liên tục giữa IDE, CLI và các resource emulator như LocalStack dẫn đến quy trình phân mảnh, kém hiệu quả.
- **Complex Manual Setup:** Cấu hình thủ công port mapping và sửa code để chạy integration test cục bộ có thể tạo ra sai khác giữa môi trường local và cloud.
- **Limited Service Integration Debugging:** Việc khắc phục sự cố Lambda tương tác với dịch vụ AWS khác (như DynamoDB hoặc Amazon SQS) truyền thống đòi hỏi cấu hình thủ công phức tạp, kéo dài thời gian xử lý lỗi.

---

## Quy trình thiết lập tự động

Extension LocalStack cho VS Code có thể cài trực tiếp từ AWS Toolkit, cung cấp một wizard thông minh cho quy trình thiết lập tinh gọn. Wizard tự phát hiện LocalStack đã được cấu hình chưa và hướng dẫn người dùng qua các bước. Nó cũng xử lý authentication bằng luồng duyệt web và lưu trữ token an toàn. Thêm nữa, wizard kiểm tra và tạo các AWS CLI profile cần thiết cho LocalStack, giúp developer dễ dàng chuyển đổi giữa môi trường local và cloud.

![First](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/12/ComputeBlog-2372-image-4.gif)

---

## Kiểm thử một ứng dụng serverless

Bài viết minh họa các khả năng này qua ví dụ thực tế: hệ thống xử lý đơn hàng event-driven dùng API Gateway, Amazon SQS, Lambda và Amazon Simple Notification Service (Amazon SNS).

![Second](/images/Blog3img1.png)

Với tích hợp mới, toàn bộ workflow có thể được kiểm thử cục bộ:

- **Deploy Locally:** Ứng dụng AWS SAM được deploy vào môi trường LocalStack local qua LocalStack AWS profile.
  ![Third](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/13/ComputeBlog-2372-build-deploy-3.gif)
- **Debug Locally:** Developer đặt breakpoint trong mã Lambda trực tiếp trong VS Code và dùng debugger tích hợp để step qua thực thi khi nó tương tác với các dịch vụ giả lập cục bộ khác.
  ![Fourth](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/13/ComputeBlog-2372-debug-2.gif)
- **Validate End-to-End:** Hoàn chỉnh workflow, từ ingestion message tại API Gateway tới notification cuối cùng từ Amazon SNS, có thể test để xác nhận mọi integration hoạt động đúng trước khi deploy lên cloud.

> Để biết thông tin kỹ thuật chi tiết về tích hợp LocalStack này, hãy tham khảo video trên youtube này.

{{< youtube e2mokcAzDCY >}}

---

## Best Practices cho kiểm thử cục bộ

Để tận dụng tối đa workflow mới, bài viết khuyến nghị cách tiếp cận phân lớp và chiến lược. Bắt đầu với unit test nhanh, độc lập để xác nhận core logic, rồi mở rộng dần sang integration và system-level validation.

Chiến lược kiểm thử đề xuất gồm bốn bước chính:

1. Bắt đầu với unit test cục bộ tập trung vào logic hàm độc lập.
2. Chuyển sang integration test cục bộ dùng LocalStack để xác nhận tương tác giữa các dịch vụ AWS.
3. Sau khi validation cục bộ xong, kiểm thử trong môi trường AWS thật để lộ các vấn đề không thể giả lập (ví dụ: sai lệch IAM permissions hoặc thách thức networking VPC).
4. Cuối cùng, thực hiện performance & load test trên AWS để đánh giá ứng dụng xử lý traffic thực tế.

---

## Khi nào dùng kiểm thử cục bộ so với trên cloud

Mặc dù kiểm thử cục bộ mang lại lợi thế về tốc độ và chi phí, cần hiểu giới hạn và biết khi nào phải test trên cloud. Bảng sau liệt kê các kịch bản sử dụng tiềm năng cho mỗi chiến lược.

| Testing Scenario                        | Local Testing | Cloud Testing | Reason                                                  |
| --------------------------------------- | ------------- | ------------- | ------------------------------------------------------- |
| Function logic validation               | ✓             |               | Fast feedback for core business logic                   |
| Service integration testing             | ✓             |               | Quick validation of AWS service interactions            |
| Rapid iteration during development      | ✓             |               | Immediate feedback without deployment overhead          |
| Cost-sensitive development environments | ✓             |               | Minimizes cloud resource costs during development       |
| Offline development scenarios           | ✓             |               | No internet connectivity required                       |
| Performance and scalability testing     |               | ✓             | Requires actual AWS infrastructure for accurate results |
| IAM permission validation               |               | ✓             | LocalStack doesn't fully replicate IAM behavior         |
| VPC networking scenarios                |               | ✓             | Network configurations can't be accurately emulated     |
| Production-like load testing            |               | ✓             | Real performance metrics only available in AWS          |
| Final validation before deployment      |               | ✓             | Supports compatibility with actual AWS environment      |

---

## Kết luận

Việc tích hợp LocalStack vào AWS Toolkit for VS Code nâng cao đáng kể trải nghiệm phát triển cục bộ cho ứng dụng serverless. Bằng cách cho phép developer chạy và debug các ứng dụng đa dịch vụ phức tạp ngay trong IDE, khả năng mới này giúp giảm chuyển ngữ cảnh, phát hiện lỗi sớm hơn và hạ chi phí phát triển. Điều này dẫn tới chu kỳ kiểm thử nhanh hơn và triển khai chất lượng cao hơn, đồng thời vẫn giữ developer kiểm soát đầy đủ môi trường cục bộ.
