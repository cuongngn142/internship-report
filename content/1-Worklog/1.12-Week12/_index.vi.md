---
title: 'Worklog Tuần 12'
date: 2026-07-06
weight: 12
chapter: false
pre: ' <b> 1.12. </b> '
---

### Mục tiêu tuần 12:

- Xây dựng hệ thống giám sát tập trung.
- Kiểm thử toàn bộ kiến trúc Security Operations Center.
- Đánh giá kết quả và hoàn thiện tài liệu dự án.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Xây dựng Amazon CloudWatch Dashboard <br> - Hiển thị các chỉ số bảo mật và vận hành | 06/07/2026 | 06/07/2026 | https://docs.aws.amazon.com/cloudwatch/ |
| 3 | - Cấu hình CloudWatch Alarms <br> - Kiểm tra Email Notification qua Amazon SNS | 07/07/2026 | 07/07/2026 | https://docs.aws.amazon.com/cloudwatch/ |
| 4 | - Thực hiện các kịch bản mô phỏng tấn công <br> - Kiểm tra Security Findings trên GuardDuty và Security Hub | 08/07/2026 | 08/07/2026 | https://docs.aws.amazon.com/guardduty/ |
| 5 | - Đánh giá hiệu quả quy trình Detect → Respond → Recover <br> - Tối ưu IAM Policies theo nguyên tắc Least Privilege | 09/07/2026 | 09/07/2026 | https://docs.aws.amazon.com/iam/ |
| 6 | - Hoàn thiện tài liệu triển khai <br> - Đánh giá chi phí và đề xuất hướng mở rộng hệ thống | 10/07/2026 | 10/07/2026 | https://docs.aws.amazon.com/wellarchitected/ |

### Kết quả đạt được tuần 12:

- Xây dựng thành công Amazon CloudWatch Dashboard phục vụ giám sát tập trung.

- Dashboard hiển thị các chỉ số quan trọng gồm:
  - GuardDuty Findings
  - Security Hub Findings
  - Lambda Invocations
  - Step Functions Executions
  - EC2 Health
  - WAF Blocked Requests
  - CloudFront Requests
  - ALB Request Count

- Cấu hình CloudWatch Alarms và kiểm thử thành công chức năng gửi cảnh báo qua Amazon SNS.

- Thực hiện nhiều kịch bản mô phỏng tấn công nhằm đánh giá khả năng phát hiện và phản ứng của hệ thống.

- Xác nhận toàn bộ quy trình Detect → Respond → Recover hoạt động đúng theo thiết kế.

- Tối ưu IAM Policies theo nguyên tắc Least Privilege nhằm giảm thiểu quyền truy cập không cần thiết.

- Đánh giá chi phí triển khai và đề xuất các hướng mở rộng như Multi-AZ, Multi-Account, Infrastructure as Code, Amazon Macie và Amazon Detective.

- Hoàn thiện báo cáo, tài liệu triển khai và tài liệu hướng dẫn sử dụng hệ thống.