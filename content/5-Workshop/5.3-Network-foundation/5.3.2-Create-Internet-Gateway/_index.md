---
title: 'Create an Internet Gateway'
date: 2026-07-09
weight: 6
chapter: false
pre: ' <b> 5.3.2. </b> '
---

## Objective

Allow the VPC to connect to the Internet.

## Service explanation

An Internet Gateway is the connection point between the VPC and the Internet.

## Step 1. Open Internet Gateways

In the navigation pane on the left, select **Internet Gateways**, then click **Create internet gateway**.

![Internet Gateways](/images/5-Workshop/placeholder.svg)

## Step 2. Create the IGW

In the configuration page:

- **Name tag**: Enter `soc-platform-igw`.
- Click **Create internet gateway**.

![Create IGW](/images/5-Workshop/placeholder.svg)

## Step 3. Attach it to the VPC

After the Internet Gateway has been created, click **Actions** → **Attach to VPC**.

- Select the VPC `soc-platform-vpc`.
- Click **Attach internet gateway**.

![Attach IGW](/images/5-Workshop/placeholder.svg)

## Validation

- The Internet Gateway has been attached to the VPC.
- The VPC can connect to the Internet.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create public and private subnets.