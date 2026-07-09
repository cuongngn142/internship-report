---
title: 'Worklog Tuần 11'
date: 2026-06-29
weight: 11
chapter: false
pre: ' <b> 1.11. </b> '
---

### Mục tiêu tuần 11:

- Hoàn thiện quy trình phản ứng sự cố tự động.
- Tích hợp các dịch vụ serverless thành một quy trình xử lý thống nhất.
- Kiểm thử các kịch bản phản ứng đối với nhiều loại Security Findings.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                              |
| --- | ----------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------- |
| 2   | - Hoàn thiện AWS Step Functions điều phối quy trình phản ứng <br> - Kết nối EventBridge với Step Functions                    | 29/06/2026   | 29/06/2026      | https://docs.aws.amazon.com/step-functions/ |
| 3   | - Phát triển Lambda cô lập EC2 bằng Isolation Security Group <br> - Kiểm thử quy trình cô lập EC2                             | 30/06/2026   | 30/06/2026      | https://docs.aws.amazon.com/ec2/            |
| 4   | - Phát triển Lambda vô hiệu hóa IAM Access Key <br> - Chặn đăng nhập Console của IAM User khi phát hiện Credential Compromise | 01/07/2026   | 01/07/2026      | https://docs.aws.amazon.com/iam/            |
| 5   | - Lưu lịch sử xử lý sự cố vào Amazon S3 <br> - Ghi log thực thi lên Amazon CloudWatch Logs                                    | 02/07/2026   | 02/07/2026      | https://docs.aws.amazon.com/s3/             |
| 6   | - Kiểm thử toàn bộ quy trình Detect → Respond bằng GuardDuty Sample Findings và Security Hub Findings                         | 03/07/2026   | 03/07/2026      | https://docs.aws.amazon.com/guardduty/      |

### Kết quả đạt được tuần 11:

- Hoàn thiện quy trình phản ứng sự cố tự động bằng AWS Step Functions.

- Amazon EventBridge tự động kích hoạt Step Functions khi AWS Security Hub tạo Security Findings.

- Phát triển Lambda Function tự động cô lập EC2 thông qua Isolation Security Group.

- Hoàn thành chức năng tự động vô hiệu hóa IAM Access Key và chặn quyền đăng nhập Console của IAM User khi phát hiện nguy cơ lộ thông tin xác thực.

- Lưu lịch sử xử lý sự cố trên Amazon S3 phục vụ kiểm toán và điều tra.

- Ghi nhận toàn bộ log thực thi của Lambda và Step Functions trên Amazon CloudWatch Logs.

- Kiểm thử thành công quy trình phản ứng tự động từ Security Hub → EventBridge → Step Functions → Lambda → SNS.
