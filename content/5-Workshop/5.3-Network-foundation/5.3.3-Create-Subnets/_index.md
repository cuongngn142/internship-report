---
title: 'Create subnets'
date: 2026-07-09
weight: 7
chapter: false
pre: ' <b> 5.3.3. </b> '
---

## Objective

Create public and private subnets for the SOC Platform environment.

## Service explanation

Subnets divide a VPC into smaller network segments. Public subnets are used for Internet traffic, while private subnets are used for internal resources.

## Step 1. Create the public subnet

In the navigation pane on the left, select **Subnets**, then click **Create subnet**.

In the configuration page:

- **VPC ID**: Select `soc-platform-vpc`.
- **Subnet name**: Enter `soc-platform-public-subnet`.
- **Availability Zone**: Select an Availability Zone (for example: `ap-southeast-1a`).
- **IPv4 CIDR block**: Enter `10.0.1.0/24`.
- Click **Create subnet**.

![Public subnet form](/images/5-Workshop/5.3-Vpc/create-subnet.PNG)

## Step 2. Enable public IPv4

- Select the newly created public subnet.
- Choose **Actions** → **Edit subnet settings**.
- Enable **Auto-assign public IPv4 address**.
- Click **Save**.

![Public subnet settings](/images/5-Workshop/5.3-Vpc/enable-ipv4.png)

## Step 3. Create the private subnet

Click **Create subnet**.

- **VPC ID**: Select `soc-platform-vpc`.
- **Subnet name**: Enter `soc-platform-private-subnet`.
- **Availability Zone**: Select the same Availability Zone as the public subnet.
- **IPv4 CIDR block**: Enter `10.0.10.0/24`.
- Click **Create subnet**.

![Private subnet form](/images/5-Workshop/5.3-Vpc/create-private-subnet.png)

## Validation

- The public subnet and private subnet have been created.
- The public subnet can receive a public IP address.

![Validation](/images/5-Workshop/5.3-Vpc/subnet-created.png)

## Next step

Next, you will create a NAT Gateway.
