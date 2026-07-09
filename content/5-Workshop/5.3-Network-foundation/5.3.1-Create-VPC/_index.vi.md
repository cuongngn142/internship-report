---
title: 'Tạo VPC'
date: 2026-07-09
weight: 5
chapter: false
pre: ' <b> 5.3.1. </b> '
---

## Mục tiêu

Tạo VPC chuyên dụng cho workshop.

## Giải thích dịch vụ

Amazon VPC cho phép tạo môi trường mạng riêng ảo phân tách khỏi các tài nguyên khác.

## Bước 1. Mở VPC Console

1. Mở **Amazon VPC console**.
2. Trên thanh điều hướng bên trái, chọn **Your VPCs**, click **Create VPC**:

![Search VPC](/images/5-Workshop/5.3-Vpc/vpc-console.png)

## Bước 2. Nhấn Create VPC Và Điền Thông Tin

- Chọn **VPC only**
- **Name tag**: Nhập `soc-platform-vpc`
- **IPv4 CIDR block**: Nhập `10.0.0.0/16`
- **IPv6 CIDR block**: Chọn **No IPv6 CIDR block**
- **Tenancy**: Chọn **Default**
- Giữ nguyên các cấu hình mặc định khác và click **Create VPC**

![Create button](/images/5-Workshop/5.3-Vpc/create-vpc)

## Bước 3. Cấu hình nâng cao

Sau khi tạo VPC, chọn VPC vừa tạo và click **Actions** → **Edit VPC settings**:

- Tick chọn **Enable DNS hostnames**
- Tick chọn **Enable DNS resolution**
- Click **Save**

![Advanced settings](/images/5-Workshop/5.3-Vpc/vpc-setting1.png)

## Validation

- VPC `soc-platform-vpc` đã được tạo.
- Trạng thái là **Available**.

![Validation](/images/5-Workshop/5.3-Vpc/vpc-setting2.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo Internet Gateway.
