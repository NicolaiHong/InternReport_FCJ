---
title: "Nhật ký công việc Tuần 11"
date: "2025-12-05"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu Tuần 11:

- Tham gia sự kiện cộng đồng AWS để thu thập thông tin về các kiến trúc đám mây tiên tiến và các tiêu chuẩn ngành.
- Xây dựng backend serverless cho dịch vụ văn bản, tập trung vào thiết kế schema DynamoDB và bảo mật vai trò IAM.
- Lập trình logic truy xuất cơ sở dữ liệu hiệu quả với phân trang và các biểu thức lọc phức tạp.
- Kiến trúc chiến lược bộ nhớ đệm (caching) trong bộ nhớ và cơ chế xác thực yêu cầu API mạnh mẽ.
- Tích hợp khả năng AI tạo sinh (Generative AI) sử dụng Amazon Bedrock Agents để tạo nội dung động.
- Triển khai khả năng quan sát và gỡ lỗi toàn diện cho khối lượng công việc serverless.
- Xây dựng các GraphQL API có khả năng mở rộng sử dụng AWS AppSync và DynamoDB resolvers.

### Các nhiệm vụ đã thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                                                                                            |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 2    | - **Tham gia sự kiện "AWS Cloud Mastery Series #2"**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | 11/17/2025   | 11/17/2025      |                                                                                                                                               |
| 3    | - **Cung cấp Hạ tầng Serverless cho Dịch vụ Văn bản:** <br>&emsp; + Triển khai bảng DynamoDB `wordsntexts` với khóa phân vùng dạng chuỗi để lưu trữ <br>&emsp; + Cấu hình vai trò thực thi IAM cho phép `dynamodb:Scan`, `dynamodb:Query`, và ghi log <br>&emsp; + Khởi tạo khung Lambda handler và thiết lập kết nối cơ sở dữ liệu `boto3` <br><br> - **Phát triển Thuật toán Truy xuất Dữ liệu:** <br>&emsp; + Thực hiện `fetch_words_from_db` sử dụng thao tác scan với phân trang `LastEvaluatedKey` <br>&emsp; + Tạo `fetch_paragraph_from_db` áp dụng lọc thuộc tính cho loại nội dung và độ dài                                                                                                                                                                                                                              | 11/18/2025   | 11/18/2025      |                                                                                                                                               |
| 4    | - **Triển khai Logic Caching và Xử lý Dữ liệu:** <br>&emsp; + Kiến trúc bộ nhớ đệm toàn cục (global in-memory cache) với TTL 300 giây để tối ưu chi phí đọc <br>&emsp; + Viết mã `get_random_words` để lấy mẫu dữ liệu từ nguồn cache hoặc cơ sở dữ liệu <br>&emsp; + Viết mã `get_paragraph` để xử lý giới hạn số lượng (1-3) và logic tách văn bản <br><br> - **Xây dựng Xác thực API và Định dạng Phản hồi:** <br>&emsp; + Phát triển lớp `Decimal_encoder` để tuần tự hóa các kiểu số của DynamoDB cho JSON <br>&emsp; + Thực hiện xác thực cho các tham số truy vấn `type` và `count` để bắt lỗi `TypeError`/`ValueError` <br>&emsp; + Chuẩn hóa phản hồi JSON với các tiêu đề HTTP và mã trạng thái chính xác                                                                                                                 | 11/19/2025   | 11/19/2025      |                                                                                                                                               |
| 5    | - **Tích hợp Amazon Bedrock Agent cho GenAI:** <br>&emsp; + Cập nhật chính sách IAM để cho phép `bedrock:InvokeAgent` trên Agent ID `HUEBUXSALX` <br>&emsp; + Khởi tạo client `bedrock-agent-runtime` và quản lý các phiên `invoke_agent` <br>&emsp; + Lập trình logic để giải mã các đoạn byte streaming thành chuỗi phản hồi liền mạch <br><br> - **Thực hiện Kỹ thuật Prompt và Kiểm thử Mô hình:** <br>&emsp; + Tinh chỉnh prompt kích hoạt để đảm bảo định dạng đầu ra cụ thể (ba đoạn văn có dấu phân cách) <br>&emsp; + Đánh giá các mô hình nền tảng về tính nhất quán trong định dạng <br>&emsp; + Triển khai logic phân tích cú pháp để phân đoạn văn bản do AI tạo ra                                                                                                                                                    | 11/20/2025   | 11/20/2025      |                                                                                                                                               |
| 6    | - **Giám sát và Gỡ lỗi qua CloudWatch và X-Ray** <br>&emsp; + Kiểm tra log Lambda trong CloudWatch để chẩn đoán lỗi thực thi <br>&emsp; + Định nghĩa các chỉ số (metrics) tùy chỉnh để theo dõi hiệu suất ứng dụng cụ thể <br>&emsp; + Thiết lập CloudWatch Alarms để cảnh báo về các ngưỡng chỉ số quan trọng <br>&emsp; + Kích hoạt AWS X-Ray tracing để lập bản đồ phụ thuộc dịch vụ và độ trễ <br><br> - **Xây dựng GraphQL API với AWS AppSync** <br>&emsp; + Cung cấp instance AppSync và liên kết DynamoDB làm nguồn dữ liệu <br>&emsp; + Phát triển resolvers cho các thao tác Ghi và Đọc đơn lẻ <br>&emsp; + Thực hiện resolvers Cập nhật và Xóa cho quản lý vòng đời dữ liệu <br>&emsp; + Cấu hình resolvers Scan/Query cho truy xuất hàng loạt <br>&emsp; + Thiết kế resolvers phức tạp cho các trường dữ liệu lồng nhau | 11/21/2025   | 11/21/2025      | CloudWatch and X-Ray Monitoring: <br> <https://000085.awsstudygroup.com/> <br> AppSync GraphQL APIs: <br> <https://000086.awsstudygroup.com/> |

### Thành tựu Tuần 11:

- Tham gia chuỗi sự kiện "AWS Cloud Mastery Series #2" để tiếp thu kiến thức về các dịch vụ AWS nâng cao và các mẫu kiến trúc.

- Xây dựng hạ tầng serverless cho ứng dụng luyện gõ văn bản:

  - Cung cấp bảng DynamoDB `wordsntexts` để chứa ~64,726 mục sử dụng khóa phân vùng dạng chuỗi.
  - Bảo mật backend với các vai trò IAM chi tiết cho quyền truy cập DynamoDB và ghi log CloudWatch.
  - Cấu hình các Lambda handler tối ưu (128 MB, timeout 15s) với kết nối `boto3` bền vững.

- Lập trình các thuật toán truy xuất dữ liệu nâng cao:

  - Thực hiện `fetch_words_from_db` sử dụng phân trang hiệu quả qua `LastEvaluatedKey`.
  - Xây dựng `fetch_paragraph_from_db` sử dụng biểu thức lọc cho các danh mục độ dài (Ngắn: 10-25, Trung bình: 25-60, Dài: 60+).

- Tối ưu hóa hiệu suất và xử lý yêu cầu:

  - Triển khai cơ chế bộ nhớ đệm (TTL 300s) để giảm thiểu việc đọc DB dưới tải ~500 yêu cầu/giờ.
  - Thực hiện các hàm lấy mẫu dữ liệu `get_random_words` và `get_paragraph` với giới hạn đầu vào.
  - Tạo lớp `Decimal_encoder` tùy chỉnh cho tuần tự hóa JSON và xác thực đầu vào mạnh mẽ để ngăn chặn lỗi runtime.
  - Chuẩn hóa phản hồi API với mã trạng thái HTTP và cấu trúc chính xác.

- Tích hợp AI tạo sinh thông qua Amazon Bedrock Agents:

  - Cấu hình quyền truy cập IAM cho `bedrock:InvokeAgent` nhắm mục tiêu Agent ID `HUEBUXSALX`.
  - Phát triển client runtime để xử lý lời gọi dựa trên phiên và giải mã luồng (stream decoding).
  - Thiết kế prompt để tạo nội dung có cấu trúc (ba đoạn văn tách biệt) cho các thử thách hàng ngày.
  - Triển khai logic phân tích cú pháp để xử lý mượt mà đầu ra do AI tạo.

- Thiết lập giám sát và gỡ lỗi toàn diện:

  - Sử dụng CloudWatch Logs để phân tích lỗi và định nghĩa metrics tùy chỉnh để theo dõi hiệu suất.
  - Cấu hình CloudWatch Alarms cho các ngưỡng quan trọng và kích hoạt X-Ray cho distributed tracing.

- Phát triển lớp GraphQL API mạnh mẽ sử dụng AWS AppSync:
  - Tích hợp nguồn dữ liệu DynamoDB và thực hiện đầy đủ các resolvers CRUD.
  - Cho phép truy cập dữ liệu hàng loạt qua resolvers Scan/Query và xử lý cấu trúc lồng nhau với resolvers đối tượng phức tạp.
