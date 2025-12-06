---
title: "Workshop"
date: "2025-09-15"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng và Triển khai Ứng dụng Fullstack Serverless trên AWS

## Tổng quan Workshop

Chào mừng bạn đến với workshop thực hành toàn diện về xây dựng và triển khai các ứng dụng fullstack serverless sẵn sàng cho môi trường thực tế (production-ready) trên AWS. Qua ba phần của chuỗi bài này, bạn sẽ học cách thiết kế kiến trúc, bảo mật và tự động hóa quy trình triển khai một ứng dụng web hiện đại sử dụng các dịch vụ serverless của AWS.

## Những gì bạn sẽ xây dựng

Kết thúc chuỗi bài này, bạn sẽ hoàn thiện một ứng dụng serverless bao gồm:

- **Frontend Bảo mật**: Một website tĩnh hiệu năng cao, phân phối toàn cầu và được bảo vệ bởi AWS WAF.
- **Backend Có thể mở rộng**: Các API RESTful được vận hành bởi Lambda functions với khả năng truy cập cơ sở dữ liệu bảo mật.
- **Xác thực Người dùng**: Quản lý người dùng hoàn chỉnh với các tính năng đăng ký, đăng nhập và phân quyền.
- **Triển khai Tự động**: Một quy trình CI/CD hoàn chỉnh giúp tự động build và deploy ứng dụng của bạn.

## Cấu trúc Workshop

### Phần 1: Triển khai Frontend với CloudFront, WAF và S3

Học cách triển khai và bảo mật một ứng dụng frontend tĩnh sử dụng mạng phân phối nội dung (CDN) của AWS. Bạn sẽ cấu hình CloudFront để phân phối toàn cầu, triển khai S3 để lưu trữ tin cậy và bảo vệ ứng dụng bằng các quy tắc AWS WAF.

**Các chủ đề chính:**

- Cấu hình S3 bucket để host website tĩnh
- Thiết lập và tối ưu hóa CloudFront distribution
- Cấu hình các quy tắc bảo mật với AWS WAF
- Quản lý tên miền tùy chỉnh (custom domain) và chứng chỉ SSL

### Phần 2: Triển khai Backend với API Gateway, Lambda và RDS

Xây dựng cơ sở hạ tầng backend bảo mật và có khả năng mở rộng. Bạn sẽ tạo các RESTful API, triển khai các hàm serverless, thiết lập cơ sở dữ liệu được quản lý (managed database) và tích hợp xác thực người dùng.

**Các chủ đề chính:**

- Thiết kế và triển khai API Gateway REST API
- Phát triển và cấu hình Lambda function
- Thiết lập cơ sở dữ liệu RDS và quản lý kết nối
- Bảo mật thông tin xác thực với AWS Secrets Manager
- Sử dụng Amazon Cognito để xác thực và ủy quyền
- Bảo mật API với Cognito authorizers

## Yêu cầu tiên quyết

**Kiến thức yêu cầu:**

- Hiểu biết cơ bản về kiến trúc ứng dụng web
- Quen thuộc với JavaScript/Node.js hoặc Python
- Sử dụng cơ bản dòng lệnh (command line/terminal)
- Hiểu biết về HTTP và REST API

**Công cụ yêu cầu:**

- Tài khoản AWS với quyền truy cập quản trị (administrative access)
- Đã cài đặt và cấu hình AWS CLI
- Trình soạn thảo văn bản hoặc IDE (khuyên dùng VS Code)
- Đã cài đặt Git trên máy

**Khuyến khích:**

- Hiểu biết cơ bản về SQL
- Quen thuộc với JSON
- Có kinh nghiệm với quản lý phiên bản (version control/Git)

## Tổng quan Kiến trúc

![Sơ đồ](/images/5-Workshop/diagram.png)

## Kết quả đạt được

Sau khi hoàn thành chuỗi workshop này, bạn sẽ có thể:

- Thiết kế và triển khai các kiến trúc serverless trên AWS
- Bảo mật ứng dụng web sử dụng các phương pháp tốt nhất trong ngành (best practices)
- Triển khai các luồng xác thực và ủy quyền người dùng
- Quản lý bí mật ứng dụng (secrets) và thông tin đăng nhập cơ sở dữ liệu một cách an toàn
- Xây dựng và duy trì các quy trình triển khai tự động (deployment pipelines)
- Tối ưu hóa ứng dụng về hiệu năng và chi phí
- Khắc phục các sự cố triển khai serverless thường gặp

## Lưu ý về Chi phí

Workshop này sử dụng các dịch vụ AWS có thể phát sinh chi phí. Chúng tôi sẽ tận dụng các dịch vụ thuộc AWS Free Tier (Gói miễn phí) ở những nơi có thể, nhưng bạn nên:

- Kiểm tra bảng điều khiển thanh toán (billing dashboard) AWS thường xuyên
- Xóa tài nguyên sau khi hoàn thành mỗi bài thực hành nếu không tiếp tục ngay lập tức
- Thiết lập cảnh báo thanh toán (billing alerts) để tránh các khoản phí không mong muốn

Chi phí ước tính để hoàn thành tất cả các bài workshop: $5-$15 (giả sử bạn không còn hạn mức Free Tier).

## Hỗ trợ

Trong suốt quá trình thực hành, bạn sẽ tìm thấy:

- Hướng dẫn từng bước kèm hình ảnh minh họa
- Các đoạn mã mẫu (code samples) và template cấu hình
- Các mẹo khắc phục sự cố thường gặp
- Liên kết đến tài liệu AWS để tìm hiểu sâu hơn

## Sẵn sàng bắt đầu?

Hãy bắt đầu với Phần 1: Triển khai Frontend và xây dựng nền móng cho ứng dụng serverless của bạn!

#### Nội dung

1. [Phần 1: Triển khai Frontend: Triển khai Frontend với CloudFront, WAF và S3](5.1-Frontend-deployment)
1. [Phần 2: Backend Serverless: Triển khai Backend với API Gateway, Lambda, RDS và Cognito](5.2-Serverless-backend)
