---
title: 'Edge Protection'
date: 2026-07-09
weight: 58
chapter: true
pre: '<b>5.8.</b>'
---

# Bảo vệ Biên Hệ thống

Trong chương này, chúng ta sẽ triển khai lớp bảo vệ đầu tiên của SOC Platform tại Edge bằng Amazon CloudFront và AWS WAF. Các yêu cầu từ Internet sẽ được kiểm tra, lọc và bảo vệ trước khi chuyển tiếp đến Application Load Balancer, đồng thời toàn bộ lưu lượng bị chặn sẽ được ghi nhận để phục vụ công tác giám sát và điều tra bảo mật.

Sau khi hoàn thành chương này, hệ thống sẽ có khả năng phân phối nội dung an toàn, giảm thiểu các cuộc tấn công phổ biến trên nền tảng web và ghi nhận các sự kiện bảo mật phát sinh tại lớp biên.

## Các bước thực hiện

### Tạo AWS WAF Web ACL

- Khởi tạo AWS WAF Web ACL để bảo vệ ứng dụng.
- Thêm các AWS Managed Rule Groups và Rate-based Rule.
- Cấu hình Web ACL để lọc và ngăn chặn các yêu cầu độc hại trước khi truy cập vào hệ thống.

### Tạo Amazon CloudFront Distribution

- Khởi tạo CloudFront Distribution sử dụng Application Load Balancer làm Origin.
- Cấu hình HTTPS, Cache Behavior và các thiết lập phân phối nội dung.
- Liên kết CloudFront với AWS WAF để bảo vệ lưu lượng truy cập từ Internet.

### Cấu hình WAF Logging

- Bật tính năng ghi log cho AWS WAF.
- Lưu các WAF Logs vào Amazon S3.
- Thu thập các yêu cầu bị chặn để phục vụ giám sát, phân tích và điều tra các sự kiện bảo mật.
