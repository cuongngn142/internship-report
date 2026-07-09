---
title: 'Create Security Groups'
date: 2026-07-09
weight: 10
chapter: false
pre: ' <b> 5.3.6. </b> '
---

## Objective

Create security groups to control inbound and outbound network traffic.

## Service explanation

A security group acts as an instance-level firewall. You need to configure appropriate rules for the Application Load Balancer and the application tier.

## Step 1. Create the security group for the ALB

Open the **EC2 Console**. In the navigation pane on the left, select **Security Groups**, then click **Create security group**.

In the configuration page:

- **Security group name**: Enter `soc-platform-alb-sg`.
- **Description**: Enter `Security group for Application Load Balancer`.
- **VPC**: Select `soc-platform-vpc`.

![ALB SG](/images/5-Workshop/placeholder.svg)

## Step 2. Add rules for the ALB security group

Under **Inbound rules**, click **Add rule**.

| Type  | Protocol | Port Range | Source    | Description           |
| ----- | -------- | ---------- | --------- | --------------------- |
| HTTPS | TCP      | 443        | 0.0.0.0/0 | HTTPS from CloudFront |
| HTTP  | TCP      | 80         | 0.0.0.0/0 | HTTP redirect         |

Click **Create security group**.

![ALB SG rules](/images/5-Workshop/placeholder.svg)

## Step 3. Create the security group for the application

Click **Create security group**.

- **Security group name**: Enter `soc-platform-app-sg`.
- **Description**: Enter `Security group for SOC Application Server`.
- **VPC**: Select `soc-platform-vpc`.

Under **Inbound rules**, click **Add rule**.

| Type       | Protocol | Port Range | Source              | Description               |
| ---------- | -------- | ---------- | ------------------- | ------------------------- |
| Custom TCP | TCP      | 8080       | soc-platform-alb-sg | Application port from ALB |

Under **Outbound rules**, delete the default rule and add the following rule.

| Type  | Protocol | Port Range | Destination | Description       |
| ----- | -------- | ---------- | ----------- | ----------------- |
| HTTPS | TCP      | 443        | 0.0.0.0/0   | HTTPS to AWS APIs |

Click **Create security group**.

![App SG](/images/5-Workshop/placeholder.svg)

## Step 4. Create the Isolation Security Group

Click **Create security group**.

- **Security group name**: Enter `soc-platform-isolation-sg`.
- **Description**: Enter `Isolation security group - no traffic allowed`.
- **VPC**: Select `soc-platform-vpc`.

Delete all **Inbound rules** and **Outbound rules** to completely isolate the resources.

Click **Create security group**.

![App SG](/images/5-Workshop/placeholder.svg)

## Validation

- The ALB security group allows traffic from the Internet.
- The application security group only allows traffic from the ALB.
- The `soc-platform-isolation-sg` security group has been created successfully.
- `soc-platform-alb-sg` allows HTTP (80) and HTTPS (443) traffic from `0.0.0.0/0`.
- `soc-platform-app-sg` only allows HTTP (80) traffic from `soc-platform-alb-sg`.
- `soc-platform-isolation-sg` has no inbound rules and no outbound rules.
- All three security groups belong to the `soc-platform-vpc` VPC.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create an Application Load Balancer.
