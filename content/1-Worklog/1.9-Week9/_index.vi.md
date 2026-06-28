---
title: 'Worklog Tuần 9'
date: 2026-06-15
weight: 9
chapter: false
pre: ' <b> 1.9. </b> '
---

### Mục tiêu tuần 9:

- Xây dựng môi trường giám sát bảo mật cơ bản trên AWS.
- Cấu hình các dịch vụ ghi log, giám sát và phát hiện mối đe dọa để theo dõi hệ thống.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                             | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                           |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------------- |
| 2   | - Tạo AWS Account và bật MFA cho Root User <br> - Tạo IAM User có quyền AdministratorAccess để sử dụng hằng ngày                                                                      | 15/06/2026   | 15/06/2026      | https://docs.aws.amazon.com/iam/         |
| 3   | - Bật AWS CloudTrail để ghi nhận toàn bộ API Call <br> - Cấu hình VPC Flow Logs và gửi log về CloudWatch Logs                                                                         | 16/06/2026   | 16/06/2026      | https://docs.aws.amazon.com/cloudtrail/  |
| 4   | - Bật AWS Config để theo dõi thay đổi cấu hình tài nguyên <br> - Cấu hình AWS Budgets và tạo cảnh báo chi phí hàng tháng                                                              | 17/06/2026   | 17/06/2026      | https://docs.aws.amazon.com/config/      |
| 5   | - Bật Amazon GuardDuty tại region ap-southeast-1 <br> - Bật AWS Security Hub với tiêu chuẩn NIST 800-53 <br> - Tích hợp GuardDuty Findings vào Security Hub                           | 18/06/2026   | 18/06/2026      | https://docs.aws.amazon.com/securityhub/ |
| 6   | - Bật IAM Access Analyzer <br> - Tạo CloudWatch Alarm cho các sự kiện failed login và root account usage <br> - Sinh GuardDuty Sample Findings và kiểm tra cảnh báo trên Security Hub | 19/06/2026   | 19/06/2026      | https://docs.aws.amazon.com/guardduty/   |

### Kết quả đạt được tuần 9:

- Thiết lập các biện pháp bảo mật IAM cơ bản bằng cách bật MFA cho Root User và sử dụng IAM User Administrator để quản trị hằng ngày.

- Bật AWS CloudTrail để ghi lại toàn bộ API Call trong tài khoản AWS.

- Cấu hình VPC Flow Logs để thu thập log lưu lượng mạng và gửi về Amazon CloudWatch Logs.

- Bật AWS Config nhằm theo dõi và ghi nhận các thay đổi cấu hình của tài nguyên AWS.

- Tạo AWS Budgets cùng cảnh báo chi phí hàng tháng để kiểm soát ngân sách sử dụng dịch vụ.

- Kích hoạt Amazon GuardDuty để phát hiện các hoạt động bất thường và các mối đe dọa bảo mật.

- Bật AWS Security Hub và tích hợp các GuardDuty Findings vào bảng điều khiển bảo mật tập trung.

- Cấu hình IAM Access Analyzer để phát hiện các tài nguyên được chia sẻ ra bên ngoài tài khoản AWS.

- Tạo CloudWatch Alarm để giám sát các sự kiện quan trọng như đăng nhập thất bại và sử dụng Root User.

- Sinh GuardDuty Sample Findings và xác nhận các cảnh báo đã được hiển thị chính xác trên AWS Security Hub.
