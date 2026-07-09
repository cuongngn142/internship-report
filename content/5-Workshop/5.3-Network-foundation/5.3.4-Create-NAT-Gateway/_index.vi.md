---
title: 'Tạo NAT Gateway'
date: 2026-07-09
weight: 8
chapter: false
pre: ' <b> 5.3.4. </b> '
---

## Mục tiêu

Tạo NAT Gateway để subnet private có thể đi ra Internet mà không cần public IP trực tiếp.

## Giải thích dịch vụ

NAT Gateway cho phép tài nguyên trong subnet private truy cập Internet nhưng giữ private IP.

## Bước 1. Tạo NAT Gateway

Trên thanh điều hướng bên trái, chọn **NAT Gateways**, click **Create NAT gateway**

![Create NAT](/images/5-Workshop/placeholder.svg)

## Bước 2. Điền thông tin

Trong giao diện cấu hình:

- **Name**: Nhập `soc-platform-nat-gw`
- **Subnet**: Chọn `soc-platform-public-subnet`
- **Connectivity type**: Chọn **Public**
- **Elastic IP allocation ID**: Click **Allocate Elastic IP** để tạo mới
- Click **Create NAT gateway**

![NAT form](/images/5-Workshop/placeholder.svg)

## Validation

- NAT Gateway đã được tạo.
- Subnet private có thể đi ra Internet qua NAT.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo route table cho public và private subnet.
