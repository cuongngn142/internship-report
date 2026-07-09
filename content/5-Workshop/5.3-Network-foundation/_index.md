---
title: 'Network Foundation'
date: 2026-07-09
weight: 53
chapter: true
pre: '<b>5.3.</b>'
---

# Network Foundation

In this chapter, you will build the foundational network infrastructure for the SOC Platform on AWS. The network is designed using a Public and Private Subnet architecture to separate Internet-facing resources from internal resources, providing a secure foundation for deploying the platform's services.

After completing this chapter, you will have a complete network architecture ready for deploying the Application Load Balancer, EC2 instances, monitoring services, and security components in the following chapters.

## Implementation steps

### Create an Amazon VPC

- Create an Amazon VPC with the IPv4 CIDR block `10.0.0.0/16`.
- Enable DNS Resolution and DNS Hostnames to support AWS services running inside the VPC.

### Configure an Internet Gateway

- Create an Internet Gateway (IGW).
- Attach the Internet Gateway to the VPC to allow the Public Subnet to access the Internet.

### Create Subnets

- Create a Public Subnet for deploying the Application Load Balancer and NAT Gateway.
- Create a Private Subnet for deploying the EC2 Application Server and other internal resources.

### Configure a NAT Gateway

- Allocate an Elastic IP for the NAT Gateway.
- Create the NAT Gateway in the Public Subnet.
- Allow resources in the Private Subnet to securely access the Internet.

### Configure Route Tables

- Create a Public Route Table and route Internet traffic through the Internet Gateway.
- Create a Private Route Table and route Internet traffic through the NAT Gateway.
- Associate the Route Tables with their corresponding Subnets.

### Secure the network with Security Groups

- Create a Security Group for the Application Load Balancer.
- Create a Security Group for the Application Server.
- Create an Isolation Security Group to isolate EC2 instances when a security incident is detected.

### Deploy an Application Load Balancer

- Create an Application Load Balancer (ALB).
- Create a Target Group for the EC2 Application Servers.
- Configure a Listener and associate the ALB with the Target Group to distribute incoming traffic to the application.
