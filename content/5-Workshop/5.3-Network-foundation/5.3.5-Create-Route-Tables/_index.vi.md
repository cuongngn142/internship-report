---
title: 'Tạo route table'
date: 2026-07-09
weight: 9
chapter: false
pre: ' <b> 5.3.5. </b> '
---

## Mục tiêu

Cấu hình route table để traffic đi đúng hướng.

## Giải thích dịch vụ

Route table quyết định lưu lượng đi ra khỏi VPC.

## Bước 1. Tạo public route table

Trên thanh điều hướng bên trái, chọn **Route Tables**, click **Create route table**

Trong giao diện cấu hình:

- **Name**: Nhập `soc-platform-public-rt`
- **VPC**: Chọn `soc-platform-vpc`
- Click **Create route table**

![Public route table](/images/5-Workshop/5.3-Vpc/rt-create.png)

## Bước 2. Thêm route tới Internet Gateway

Chọn route table vừa tạo, tab **Routes**, click **Edit routes**:

- Click **Add route**
- **Destination**: `0.0.0.0/0`
- **Target**: Chọn **Internet Gateway** → `soc-platform-igw`
- Click **Save changes**

![Route entry](/images/5-Workshop/5.3-Vpc/add-route.png)

## Bước 3. Gắn subnet public

Tab **Subnet associations**, click **Edit subnet associations**:

- Tick chọn `soc-platform-public-subnet`
- Click **Save associations**

![Associate subnet](/images/5-Workshop/5.3-Vpc/association-public.png)

## Bước 4. Tạo private route table

Click **Create route table**:

- **Name**: Nhập `soc-platform-private-rt`
- **VPC**: Chọn `soc-platform-vpc`
- Click **Create route table**
![Private route table](/images/5-Workshop/5.3-Vpc/rt-create1.png)

Chọn route table vừa tạo, tab **Routes**, click **Edit routes**:

- Click **Add route**
- **Destination**: `0.0.0.0/0`
- **Target**: Chọn **NAT Gateway** → `soc-platform-nat-gw`
- Click **Save changes**
![Route entry private](/images/5-Workshop/5.3-Vpc/add-route1.png)

Tab **Subnet associations**, click **Edit subnet associations**:

- Tick chọn `soc-platform-private-subnet`
- Click **Save associations**

![Associate subnet private](/images/5-Workshop/5.3-Vpc/association-private.png)

## Validation

- Public subnet đi ra Internet qua IGW.
- Private subnet đi ra Internet qua NAT Gateway.

![Validation](/images/5-Workshop/5.3-Vpc/valid-rt.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo security group.
