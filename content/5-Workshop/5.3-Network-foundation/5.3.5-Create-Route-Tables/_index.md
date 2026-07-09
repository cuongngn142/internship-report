---
title: 'Create route tables'
date: 2026-07-09
weight: 9
chapter: false
pre: ' <b> 5.3.5. </b> '
---

## Objective

Configure route tables so that network traffic is routed correctly.

## Service explanation

A route table determines how traffic leaves the VPC.

## Step 1. Create the public route table

In the navigation pane on the left, select **Route Tables**, then click **Create route table**.

In the configuration page:

- **Name**: Enter `soc-platform-public-rt`.
- **VPC**: Select `soc-platform-vpc`.
- Click **Create route table**.

![Public route table](/images/5-Workshop/placeholder.svg)

## Step 2. Add a route to the Internet Gateway

Select the newly created route table, then open the **Routes** tab and click **Edit routes**.

- Click **Add route**.
- **Destination**: `0.0.0.0/0`.
- **Target**: Select **Internet Gateway** → `soc-platform-igw`.
- Click **Save changes**.

![Route entry](/images/5-Workshop/placeholder.svg)

## Step 3. Associate the public subnet

Open the **Subnet associations** tab, then click **Edit subnet associations**.

- Select `soc-platform-public-subnet`.
- Click **Save associations**.

![Associate subnet](/images/5-Workshop/placeholder.svg)

## Step 4. Create the private route table

Click **Create route table**.

- **Name**: Enter `soc-platform-private-rt`.
- **VPC**: Select `soc-platform-vpc`.
- Click **Create route table**.

Select the newly created route table, then open the **Routes** tab and click **Edit routes**.

- Click **Add route**.
- **Destination**: `0.0.0.0/0`.
- **Target**: Select **NAT Gateway** → `soc-platform-nat-gw`.
- Click **Save changes**.

Open the **Subnet associations** tab, then click **Edit subnet associations**.

- Select `soc-platform-private-subnet`.
- Click **Save associations**.

![Private route table](/images/5-Workshop/placeholder.svg)

## Validation

- The public subnet can access the Internet through the Internet Gateway.
- The private subnet can access the Internet through the NAT Gateway.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create a security group.