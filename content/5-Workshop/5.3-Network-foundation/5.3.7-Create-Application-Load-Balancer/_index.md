---
title: 'Create an Application Load Balancer'
date: 2026-07-09
weight: 11
chapter: false
pre: ' <b> 5.3.7. </b> '
---

## Objective

Create an Application Load Balancer to distribute traffic to the application.

## Service explanation

An Application Load Balancer distributes incoming traffic to multiple targets, improving availability and scalability.

## Step 1. Create the ALB

- Open the **EC2 Console**.
- Select **Load Balancers** → **Create load balancer**.
- Select **Application Load Balancer**.
- Click **Create**.

![Create ALB](/images/5-Workshop/5.3-Vpc/alb.png)

## Step 2. Fill in the fields

**Basic configuration**:

- **Load balancer name**: Enter `soc-platform-alb`.
- **Scheme**: Select **Internet-facing**.
- **IP address type**: Select **IPv4**.

**Network mapping**:

- **VPC**: Select `soc-platform-vpc`.
- **Mappings**: Select the Availability Zone and choose `soc-platform-public-subnet`.

**Security groups**:

- Select `soc-platform-alb-sg`.

![ALB form](/images/5-Workshop/5.3-Vpc/alb-create.png)

## Step 3. Create the target group

Click **Create target group**.

- **Target type**: Select **Instances**.
- **Target group name**: Enter `soc-platform-tg`.
- **Protocol**: HTTP, **Port**: 8080.
- **VPC**: Select `soc-platform-vpc`.
- **Health check path**: Enter `/health`.
- Click **Next** → **Create target group**.

![Target group](/images/5-Workshop/5.3-Vpc/target-group.png)

## Validation

- The Application Load Balancer has been created.
- Traffic can be distributed to the target group.

![Validation](/images/5-Workshop/5.3-Vpc/created-alb.png)

## Next step

Next, you will create the storage and log collection services.
