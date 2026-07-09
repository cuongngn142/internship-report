---
title: 'Step 4: Create a NAT Gateway'
date: 2026-07-09
weight: 8
chapter: false
pre: ' <b> 5.3.4. </b> '
---

## Objective

Create a NAT Gateway so that the private subnet can access the Internet without requiring a public IP address.

## Service explanation

A NAT Gateway allows resources in a private subnet to access the Internet while keeping their private IP addresses.

## Step 1. Create the NAT Gateway

In the navigation pane on the left, select **NAT Gateways**, then click **Create NAT gateway**.

![Create NAT](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

In the configuration page:

- **Name**: Enter `soc-platform-nat-gw`.
- **Subnet**: Select `soc-platform-public-subnet`.
- **Connectivity type**: Select **Public**.
- **Elastic IP allocation ID**: Click **Allocate Elastic IP** to create a new Elastic IP.
- Click **Create NAT gateway**.

![NAT form](/images/5-Workshop/placeholder.svg)

## Validation

- The NAT Gateway has been created.
- The private subnet can access the Internet through the NAT Gateway.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create route tables for the public and private subnets.