---
title: "Blog 1"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Cách chúng tôi xây dựng một "flywheel" để cải thiện bảo mật liên tục cho Amazon RDS

> bởi Joshua Brindle

Bài viết này mô tả quy trình mà một nhóm bảo mật AWS đã thực hiện để bảo vệ một tính năng mới, **PL/Rust**, trên **Amazon Relational Database Service (Amazon RDS)**. Tác giả (principal security engineer) giải thích cách nhóm vượt ra ngoài triển khai tối thiểu để xây dựng một hệ thống bảo mật toàn diện, tự cải thiện – một "flywheel" – kết hợp công nghệ, quy trình và kiểm thử nhằm bảo vệ khách hàng.

---

## Các thành phần của hệ thống

Trung tâm của dự án là **PL/Rust**, một extension cho phép người dùng viết các hàm PostgreSQL tùy chỉnh bằng **Rust**, sau đó được biên dịch thành native machine code hiệu năng cao. Lõi của extension này là thư viện có tên **postgrestd**, được thiết kế để ngăn việc "thoát" khỏi phạm vi cơ sở dữ liệu (database escape). Tuy nhiên, tại thời điểm đó, thư viện còn mới và chưa được "harden" cho thực tế môi trường production quy mô lớn.
<br><br>
Thách thức bảo mật chính xuất phát từ việc PL/Rust biên dịch các extension này trực tiếp trên chính database instance. Thiết kế này yêu cầu toàn bộ development toolchain phải sẵn có cục bộ, làm tăng đáng kể rủi ro tiềm ẩn. Một extension được xây kém có thể làm mất ổn định database hoặc host instance của nó, và attacker có thể dùng nhiều kỹ thuật để tìm cách vượt qua các kiểm soát bảo mật như mô hình **viết hoặc loại trừ thực hiện [write xor execute] (W^X)**. Bối cảnh đó cho thấy cần một chuỗi các biện pháp giảm thiểu (mitigations) vững chắc để cung cấp tính năng này một cách an toàn cho khách hàng.

---

## Thách thức cách tiếp cận

Văn hóa AWS đề cao operational excellence – tập trung vào automation, resilience và simplicity – đã ảnh hưởng mạnh mẽ đến quá trình tìm giải pháp. Nhóm đã cân nhắc **SELinux (Security-Enhanced Linux)**, được mô tả là một lựa chọn từng tranh luận lâu dài. SELinux là tập hợp các kernel features thực thi **mandatory access control (MAC)**, bổ sung một lớp bảo vệ mạnh phía trên hệ thống authorization tiêu chuẩn. Với SELinux policies, administrator có thể đặc tả cực kỳ chi tiết những gì được phép trên hệ thống; ví dụ: ngăn một process ghi vào file ngay cả khi quyền sở hữu thông thường cho phép.
<br><br>
Mức độ kiểm soát tất định (deterministic control) này có thể nâng cao đáng kể bảo mật của hệ điều hành. Đổi lại là giảm tính linh hoạt và nỗ lực đáng kể để cấu hình các access controls đáp ứng yêu cầu bảo mật cụ thể. Sau một cuộc tranh luận nội bộ kỹ lưỡng (senior leaders thách thức ý tưởng để dự đoán vấn đề tương lai), nhóm thống nhất rằng cho trường hợp sử dụng PL/Rust, lợi ích của SELinux vượt trội so với hạn chế. Quyết định được đưa ra để tiếp tục theo hướng này.

---

## Xây dựng "Security Flywheel"

Chỉ triển khai một công cụ là chưa đủ; nhóm đã xây dựng một quy trình hoàn chỉnh, liên tục cải tiến quanh nó.

1. **Enforce & Monitor**: Xây dựng môi trường SELinux và tạo policies để "lock down" hệ thống. Điểm then chốt: cấu hình các policy gửi mọi **tin nhắn từ chối (denial messages)** đến hệ thống telemetry nội bộ để phân tích.
2. **Respond**: Phối hợp với internal blue team, họ phát triển các **incident response playbooks** cụ thể cho đội Amazon RDS điều tra các denial messages này.
3. **Test & Refine**: Bắt đầu chạy hàng quý các **"game days"**. Trong các bài diễn tập này, red team dàn dựng exploit nhắm vào hệ thống, và service team phản hồi bằng playbook. Sau đó tất cả các đội phân tích phản hồi để tìm bottlenecks và vùng cần cải thiện.

Chu trình enforcement → monitoring → response → testing tạo nên một cỗ máy bảo mật nhịp nhàng, chắc chắn.

---

## Flywheel vận hành: Ví dụ thực tế

Hiệu quả của hệ thống được kiểm chứng trong môi trường production. Một SELinux denial message tự động tạo một ticket mức độ nghiêm trọng cao cho service team. Hệ thống hoạt động đúng kỳ vọng: chặn thành công một hoạt động không được phép, đóng vai trò như một proactive intrusion detection system.
<br><br>
Dù rủi ro tức thời đã bị vô hiệu hóa, quy trình của nhóm yêu cầu phải điều tra root cause để xem hệ thống còn cải thiện được không. Cuộc điều tra cuối cùng cho thấy hoạt động được khởi xướng bởi nhóm nghiên cứu tại Varonis Threat Labs. Đội bảo mật AWS sau đó liên hệ để hợp tác, minh họa cách một security event có thể dẫn tới tương tác tích cực với cộng đồng nghiên cứu. Sự cố này cung cấp một ví dụ cụ thể và đáng giá về việc công việc chủ động của nhóm đã trực tiếp mang lại lợi ích cho khách hàng.

> Đối với các security engineers tham gia, đây là sự xác nhận sâu sắc vì nó đưa ra ví dụ cụ thể về cách nỗ lực chủ động của họ đã ngăn ngừa một vấn đề tiềm ẩn, mang lại lợi ích trực tiếp cho khách hàng.
