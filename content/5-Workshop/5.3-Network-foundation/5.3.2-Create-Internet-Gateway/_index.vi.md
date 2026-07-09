---
title: 'Tạo Internet Gateway'
date: 2026-07-09
weight: 6
chapter: false
pre: ' <b> 5.3.2. </b> '
---

## Mục tiêu

Cho phép VPC kết nối ra Internet.

## Giải thích dịch vụ

Internet Gateway là điểm kết nối giữa VPC và Internet.

## Bước 1. Mở Internet Gateways

Trên thanh điều hướng bên trái, chọn **Internet Gateways**, click **Create internet gateway**:

![Internet Gateways](/images/5-Workshop/5.3-Vpc/igw.png)

## Bước 2. Tạo IGW

Trong giao diện cấu hình:

- **Name tag**: Nhập `soc-platform-igw`
- Click **Create internet gateway**

![Create IGW](/images/5-Workshop/5.3-Vpc/create-igw.png)

## Bước 3. Gắn vào VPC

Sau khi tạo, click **Actions** → **Attach to VPC**:

- Chọn VPC `soc-platform-vpc`
- Click **Attach internet gateway**

![Attach IGW](/images/5-Workshop/5.3-Vpc/attach-to-vpc.PNG)

## Validation

- Internet Gateway đã được gắn vào VPC.
- VPC có thể kết nối tới Internet.

![Validation](/images/5-Workshop/5.3-Vpc/attach-to-vpc1.PNG)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo subnet public và private.
