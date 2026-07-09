---
title: 'Visibility and Dashboard'
date: 2026-07-09
weight: 57
chapter: true
pre: '<b>5.7.</b>'
---

# Giám sát và Bảng điều khiển

Trong chương này, chúng ta sẽ xây dựng hệ thống giám sát tập trung cho SOC Platform bằng Amazon CloudWatch. Các chỉ số vận hành, cảnh báo bảo mật và trạng thái của các dịch vụ sẽ được trực quan hóa trên Dashboard, đồng thời hệ thống sẽ tự động tạo cảnh báo khi phát hiện các sự kiện vượt ngưỡng đã cấu hình.

Sau khi hoàn thành chương này, bạn sẽ có một bảng điều khiển tập trung để theo dõi tình trạng hoạt động của toàn bộ hệ thống và nhận thông báo kịp thời khi xảy ra các sự cố hoặc hành vi bất thường.

## Các bước thực hiện

### Tạo Amazon CloudWatch Dashboard

- Tạo CloudWatch Dashboard để giám sát hệ thống.
- Thêm các widgets hiển thị Metrics từ GuardDuty, Lambda, Application Load Balancer, Step Functions và các dịch vụ liên quan.
- Xây dựng giao diện theo dõi tập trung phục vụ việc giám sát và vận hành SOC Platform.

### Tạo Amazon CloudWatch Alarms

- Tạo CloudWatch Alarms cho các Metrics quan trọng.
- Cấu hình ngưỡng cảnh báo đối với các sự kiện bảo mật và lỗi hệ thống.
- Liên kết CloudWatch Alarms với Amazon SNS để gửi thông báo khi phát hiện sự cố.
