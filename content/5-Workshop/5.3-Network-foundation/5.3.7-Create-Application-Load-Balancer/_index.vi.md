---
title: 'Tạo Application Load Balancer'
date: 2026-07-09
weight: 11
chapter: false
pre: ' <b> 5.3.7. </b> '
---

## Mục tiêu

Tạo ALB để phân phối traffic tới ứng dụng.

## Giải thích dịch vụ

Application Load Balancer phân phối traffic tới nhiều target và tăng tính sẵn sàng.

## Bước 1. Tạo ALB

- Mở EC2 Console.
- Chọn **Load Balancers** → **Create load balancer**.
- Chọn **Application Load Balancer**.
- Chọn **Application Load Balancer**, click **Create**:

![Create ALB](/images/5-Workshop/5.3-Vpc/alb.png)

## Bước 2. Điền thông tin

**Basic configuration**:

- **Load balancer name**: Nhập `soc-platform-alb`
- **Scheme**: Chọn **Internet-facing**
- **IP address type**: Chọn **IPv4**

**Network mapping**:

- **VPC**: Chọn `soc-platform-vpc`
- **Mappings**: Tick chọn AZ và chọn `soc-platform-public-subnet`

**Security groups**: Chọn `soc-platform-alb-sg`

![ALB form](/images/5-Workshop/5.3-Vpc/alb-create.png)

## Bước 3. Tạo target group

Click **Create target group**

- **Target type**: Chọn **Instances**
- **Target group name**: Nhập `soc-platform-tg`
- **Protocol**: HTTP, **Port**: 8080
- **VPC**: Chọn `soc-platform-vpc`
- **Health check path**: Nhập `/health`
- Click **Next** → **Create target group**

![Target group](/images/5-Workshop/5.3-Vpc/target-group.png)

## Validation

- ALB đã được tạo.
- Traffic có thể được phân phối tới target group.

![Validation](/images/5-Workshop/5.3-Vpc/created-alb.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo các dịch vụ lưu trữ và thu thập log.
