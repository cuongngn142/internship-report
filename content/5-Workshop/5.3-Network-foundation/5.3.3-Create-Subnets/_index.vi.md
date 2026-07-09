---
title: 'Tạo subnet'
date: 2026-07-09
weight: 7
chapter: false
pre: ' <b> 5.3.3. </b> '
---

## Mục tiêu

Tạo subnet public và private cho môi trường SOC Platform.

## Giải thích dịch vụ

Subnet chia VPC thành các vùng mạng nhỏ hơn. Public subnet dùng cho traffic từ Internet, private subnet dùng cho tài nguyên nội bộ.

## Bước 1. Tạo public subnet

Trên thanh điều hướng bên trái, chọn **Subnets**, click **Create subnet**:

Trong giao diện cấu hình:

- **VPC ID**: Chọn `soc-platform-vpc`
- **Subnet name**: Nhập `soc-platform-public-subnet`
- **Availability Zone**: Chọn một AZ (ví dụ: `ap-southeast-1a`)
- **IPv4 CIDR block**: Nhập `10.0.1.0/24`
- Click **Create subnet**

![Public subnet form](/images/5-Workshop/5.3-Vpc/create-subnet.PNG)

## Bước 2. Bật public IPv4

- Chọn subnet public vừa tạo.
- Chọn **Actions** → **Edit subnet settings**.
- Bật **Auto-assign public IPv4 address**.
- Click **Save**

![Public subnet settings](/images/5-Workshop/5.3-Vpc/enable-ipv4.png)

## Bước 3. Tạo private subnet

Click **Create subnet**:

- **VPC ID**: Chọn `soc-platform-vpc`
- **Subnet name**: Nhập `soc-platform-private-subnet`
- **Availability Zone**: Chọn cùng AZ với public subnet
- **IPv4 CIDR block**: Nhập `10.0.10.0/24`
- Click **Create subnet**

![Private subnet form](/images/5-Workshop/5.3-Vpc/create-private-subnet.png)

## Validation

- Public subnet và private subnet đã được tạo.
- Public subnet có thể nhận public IP.

![Validation](/images/5-Workshop/5.3-Vpc/subnet-created.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo NAT Gateway.
