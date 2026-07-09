---
title: 'Network Foundation'
date: 2026-07-09
weight: 53
chapter: true
pre: '<b>5.3.</b>'
---

# Hạ tầng Mạng

Trong chương này, chúng ta sẽ xây dựng hạ tầng mạng nền tảng cho hệ thống SOC Platform trên AWS. Hạ tầng mạng được thiết kế theo mô hình Public và Private Subnets nhằm tách biệt các tài nguyên truy cập Internet với các tài nguyên nội bộ, đồng thời tạo nền tảng an toàn để triển khai các dịch vụ của hệ thống.

Sau khi hoàn thành chương này, bạn sẽ có một kiến trúc mạng hoàn chỉnh sẵn sàng cho việc triển khai Application Load Balancer, EC2, các dịch vụ giám sát và các thành phần bảo mật ở những chương tiếp theo.

## Các bước thực hiện

### Khởi tạo Amazon VPC

- Tạo Amazon VPC với dải địa chỉ IPv4 CIDR `10.0.0.0/16`.
- Bật DNS Resolution và DNS Hostnames để hỗ trợ các dịch vụ AWS hoạt động trong VPC.

### Cấu hình Internet Gateway

- Tạo Internet Gateway (IGW).
- Gắn Internet Gateway vào VPC để cho phép Public Subnet kết nối Internet.

### Khởi tạo Subnets

- Tạo Public Subnet để triển khai Application Load Balancer và NAT Gateway.
- Tạo Private Subnet để triển khai EC2 Application Server và các tài nguyên nội bộ.

### Cấu hình NAT Gateway

- Tạo Elastic IP cho NAT Gateway.
- Khởi tạo NAT Gateway trong Public Subnet.
- Cho phép các tài nguyên trong Private Subnet truy cập Internet một cách an toàn.

### Cấu hình Route Tables

- Tạo Public Route Table và định tuyến lưu lượng Internet thông qua Internet Gateway.
- Tạo Private Route Table và định tuyến lưu lượng Internet thông qua NAT Gateway.
- Liên kết Route Tables với các Subnets tương ứng.

### Bảo mật mạng với Security Groups

- Tạo Security Group cho Application Load Balancer.
- Tạo Security Group cho Application Server.
- Tạo Isolation Security Group để cô lập EC2 khi phát hiện sự cố bảo mật.

### Triển khai Application Load Balancer

- Khởi tạo Application Load Balancer (ALB).
- Tạo Target Group cho các EC2 Application Server.
- Cấu hình Listener và liên kết ALB với Target Group để phân phối lưu lượng truy cập đến ứng dụng.
