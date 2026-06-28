---
title: 'Worklog Tuần 10'
date: 2026-06-22
weight: 10
chapter: false
pre: ' <b> 1.10. </b> '
---

---

### Mục tiêu tuần 10:

- Xây dựng hệ thống phản ứng sự cố tự động bằng các dịch vụ serverless của AWS.
- Phát triển các Lambda Function để xử lý cảnh báo bảo mật và tự động thực hiện các hành động khắc phục.
- Tích hợp Amazon EventBridge để kích hoạt quy trình phản ứng sự cố tự động.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ------------------------------------------- |
| 2   | - Tạo SNS Topic phục vụ gửi cảnh báo bảo mật <br> - Đăng ký email nhận thông báo                                                                       | 22/06/2026   | 22/06/2026      | https://docs.aws.amazon.com/sns/            |
| 3   | - Phát triển Lambda Function #1 để xử lý GuardDuty Findings <br> - Phân tích mức độ nghiêm trọng và gửi cảnh báo qua SNS                               | 23/06/2026   | 23/06/2026      | https://docs.aws.amazon.com/lambda/         |
| 4   | - Phát triển Lambda Function #2 để tự động chặn địa chỉ IP đáng ngờ bằng cách cập nhật Security Group của EC2                                          | 24/06/2026   | 24/06/2026      | https://docs.aws.amazon.com/ec2/            |
| 5   | - Tạo EventBridge Rule để kích hoạt Lambda khi GuardDuty phát hiện cảnh báo mức High <br> - Kiểm thử toàn bộ quy trình từ GuardDuty đến email cảnh báo | 25/06/2026   | 25/06/2026      | https://docs.aws.amazon.com/eventbridge/    |
| 6   | - Phát triển Lambda Function #3 để tự động thu hồi IAM Access Key bị lộ <br> - Thiết kế quy trình phản ứng sự cố nhiều bước bằng AWS Step Functions    | 26/06/2026   | 26/06/2026      | https://docs.aws.amazon.com/step-functions/ |

### Kết quả đạt được tuần 10:

- Cấu hình thành công Amazon SNS để gửi cảnh báo bảo mật qua email.

- Phát triển các Lambda Function sử dụng Python 3.12 để tự động xử lý GuardDuty Findings.

- Xây dựng chức năng tự động gửi email cảnh báo dựa trên mức độ nghiêm trọng của sự kiện bảo mật.

- Hoàn thành chức năng tự động cập nhật EC2 Security Group để chặn các địa chỉ IP đáng ngờ.

- Cấu hình Amazon EventBridge để tự động kích hoạt Lambda khi GuardDuty phát hiện mối đe dọa mức High.

- Kiểm thử thành công toàn bộ quy trình phản ứng sự cố:
  - GuardDuty Sample Finding
  - EventBridge Rule
  - AWS Lambda
  - Amazon SNS Email Notification

- Triển khai chức năng tự động thu hồi IAM Access Key khi GuardDuty phát hiện thông tin xác thực bị lộ.

- Thiết kế workflow bằng AWS Step Functions để điều phối quy trình xử lý sự cố nhiều bước.

- Áp dụng các thực hành bảo mật theo khuyến nghị của AWS:
  - Sử dụng IAM Role thay cho việc lưu Access Key trong mã nguồn
  - Xử lý ngoại lệ bằng try/except
  - Ghi log thực thi vào Amazon CloudWatch Logs
