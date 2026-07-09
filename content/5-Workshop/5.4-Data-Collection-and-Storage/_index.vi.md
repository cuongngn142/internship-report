---
title: "Data Collection and Storage"
date: 2026-07-09
weight: 54
chapter: true
pre: "<b>5.4.</b>"
---

# Thu thập và Lưu trữ Dữ liệu

Trong chương này, chúng ta sẽ triển khai các dịch vụ thu thập và lưu trữ dữ liệu phục vụ cho hệ thống SOC Platform trên AWS. Toàn bộ log từ hạ tầng và các dịch vụ sẽ được tập trung về Amazon S3, mã hóa bằng AWS KMS và sẵn sàng cho việc phân tích, truy vấn cũng như điều tra sự cố bảo mật.

Sau khi hoàn thành chương này, hệ thống sẽ có khả năng thu thập, lưu trữ và quản lý tập trung các nhật ký hoạt động để phục vụ cho các dịch vụ phát hiện mối đe dọa và giám sát bảo mật ở các chương tiếp theo.

## Các bước thực hiện

### Khởi tạo AWS KMS Key

- Tạo khóa mã hóa KMS cho hệ thống.
- Cấu hình quyền sử dụng khóa cho các dịch vụ AWS.
- Sử dụng khóa KMS để mã hóa dữ liệu và log.

### Tạo S3 Bucket lưu trữ Logs

- Khởi tạo Amazon S3 Bucket làm nơi lưu trữ tập trung các log.
- Bật Versioning và Server-side Encryption (SSE-KMS).
- Cấu hình Bucket Policy và Lifecycle Rules để quản lý dữ liệu lâu dài.

### Cấu hình AWS CloudTrail

- Tạo CloudTrail để ghi lại các hoạt động API trong tài khoản AWS.
- Lưu log CloudTrail vào Amazon S3.
- Bật mã hóa và kiểm tra tính toàn vẹn của log.

### Cấu hình VPC Flow Logs

- Tạo VPC Flow Logs để ghi nhận lưu lượng mạng trong VPC.
- Lưu Flow Logs vào Amazon S3.
- Thu thập thông tin phục vụ việc giám sát và điều tra các sự kiện mạng.

### Thiết lập Athena Workgroup và AWS Glue Database

- Tạo Athena Workgroup để thực hiện truy vấn dữ liệu log.
- Tạo AWS Glue Database quản lý metadata của dữ liệu.
- Chuẩn bị môi trường phục vụ phân tích và truy vấn log bằng Amazon Athena.