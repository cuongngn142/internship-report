---
title: 'Automated Response'
date: 2026-07-09
weight: 56
chapter: true
pre: '<b>5.6.</b>'
---

# Tự động Ứng phó Sự cố

Trong chương này, chúng ta sẽ xây dựng cơ chế ứng phó sự cố tự động cho hệ thống SOC Platform bằng cách kết hợp các dịch vụ serverless của AWS. Khi các dịch vụ phát hiện mối đe dọa tạo ra Security Findings, hệ thống sẽ tự động kích hoạt quy trình xử lý, gửi thông báo và thực hiện các hành động phản ứng phù hợp nhằm giảm thiểu thời gian xử lý sự cố.

Sau khi hoàn thành chương này, hệ thống sẽ có khả năng tự động nhận các sự kiện bảo mật, điều phối quy trình xử lý và thực hiện các hành động phản ứng mà không cần sự can thiệp thủ công.

## Các bước thực hiện

### Tạo Amazon SNS Topics

- Tạo các SNS Topics để gửi thông báo bảo mật.
- Cấu hình Subscription nhận cảnh báo qua Email.
- Chuẩn bị các kênh thông báo cho các mức độ sự cố khác nhau.

### Tạo AWS Lambda Functions

- Tạo các Lambda Functions thực hiện các tác vụ phản ứng tự động.
- Cấu hình IAM Execution Role và Environment Variables.
- Triển khai mã nguồn cho các chức năng gửi thông báo và xử lý sự cố.

### Tạo AWS Step Functions State Machine

- Khởi tạo State Machine điều phối quy trình ứng phó.
- Xây dựng workflow thực thi các Lambda Functions theo từng mức độ cảnh báo.
- Cấu hình IAM Role cho Step Functions.

### Tạo Amazon EventBridge Rules

- Tạo EventBridge Rules để lắng nghe Security Findings từ các dịch vụ AWS.
- Cấu hình Event Pattern cho GuardDuty và Security Hub.
- Liên kết EventBridge với Step Functions để tự động kích hoạt quy trình ứng phó khi phát hiện sự cố.
