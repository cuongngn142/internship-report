---
title: 'Detection and Compliance'
date: 2026-07-09
weight: 55
chapter: true
pre: '<b>5.5.</b>'
---

# Phát hiện Mối đe dọa và Tuân thủ

Trong chương này, chúng ta sẽ triển khai các dịch vụ bảo mật của AWS nhằm phát hiện các mối đe dọa, giám sát cấu hình tài nguyên và đánh giá mức độ tuân thủ theo các tiêu chuẩn bảo mật. Các dịch vụ này sẽ thu thập, phân tích và tổng hợp các phát hiện bảo mật từ nhiều nguồn khác nhau để hỗ trợ việc giám sát và ứng phó sự cố.

Sau khi hoàn thành chương này, hệ thống SOC Platform sẽ có khả năng phát hiện các hành vi bất thường, kiểm tra cấu hình tài nguyên, đánh giá quyền truy cập và tổng hợp các cảnh báo bảo mật trên một giao diện quản lý tập trung.

## Các bước thực hiện

### Bật Amazon GuardDuty

- Kích hoạt Amazon GuardDuty để phát hiện các mối đe dọa trong tài khoản AWS.
- Cấu hình các tính năng bảo vệ như S3 Protection và Malware Protection.
- Thu thập và tạo các Security Findings phục vụ giám sát.

### Tạo IAM Access Analyzer

- Khởi tạo IAM Access Analyzer.
- Phân tích các chính sách IAM và Resource-based Policies.
- Phát hiện các tài nguyên có khả năng bị truy cập ngoài phạm vi tài khoản AWS.

### Bật AWS Config

- Kích hoạt AWS Config để ghi nhận cấu hình của các tài nguyên AWS.
- Cấu hình Delivery Channel và Configuration Recorder.
- Áp dụng các AWS Managed Rules để đánh giá mức độ tuân thủ của hệ thống.

### Bật AWS Security Hub

- Kích hoạt AWS Security Hub.
- Bật các tiêu chuẩn bảo mật như AWS Foundational Security Best Practices và CIS AWS Foundations Benchmark.
- Tổng hợp các Security Findings từ GuardDuty, AWS Config và các dịch vụ bảo mật khác vào một bảng điều khiển thống nhất.
