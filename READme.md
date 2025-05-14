# AWS VPC - Virtual Private Cloud

## Table of Contents
1. [Project Overview](#project-overview)  
    1.1 [Objectives](#objectives)  
2. [Project Steps and Commands](#project-steps-and-commands)  
    2.1 [Go to VPC Page](#21-go-to-vpc-page)  
    2.2 [Create VPC](#22-create-vpc)  
    2.3 [Configure VPC](#23-configure-vpc)  
    2.4 [Create Subnets](#24-create-subnets)  
    2.5 [Set Up Internet Gateway](#25-set-up-internet-gateway)  
    2.6 [Configure Route Tables](#26-configure-route-tables)  
    2.7 [Set Up NAT Gateway](#27-set-up-nat-gateway)  
    2.8 [VPC Peering](#28-vpc-peering)  
3. [Troubleshooting](#troubleshooting)  
    3.1 [VPC Not Connecting to Internet](#31-vpc-not-connecting-to-internet)  
    3.2 [Subnet Routing Issues](#32-subnet-routing-issues)  
    3.3 [VPC Peering Not Working](#33-vpc-peering-not-working)  
    3.4 [NAT Gateway Connectivity Issues](#34-nat-gateway-connectivity-issues)  

---

## Project Overview

This mini project demonstrates the practical implementation of a secure and scalable network using Amazon Web Services (AWS) Virtual Private Cloud (VPC). It includes the creation of a VPC, subnets, routing components, and connectivity via Internet Gateway, NAT Gateway, and VPC Peering. Each step includes visual references for better understanding.

### Objectives

**Purpose**  
Design and deploy an AWS VPC that ensures secure and efficient communication between public and private resources.

**Requirements**
- Implement a VPC with public and private subnets.
- Attach an Internet Gateway (IGW) to enable internet access for public-facing resources.
- Deploy a NAT Gateway for secure outbound communication from private subnets.
- Configure Route Tables for traffic control.
- Set up VPC Peering for cross-VPC communication.
- Follow AWS best practices for security and cost-effectiveness.

**Use Case**  
The architecture is suited for hosting applications where web servers reside in the public subnet and databases remain protected in the private subnet.

**Performance Goals**
- Achieve low-latency internal communication.
- Maintain high availability using multiple availability zones.
- Apply proper security measures (security groups, ACLs).
- Optimize costs through resource allocation strategies.

---

## Project Steps and Commands

### 2.1 Go to VPC Page

- Navigate to AWS Console and search for "VPC".
- Select the VPC dashboard.  
  ![search-VPC](images/1.png)

### 2.2 Create VPC

- Click “Create VPC”.
- Choose “VPC Only”.
- Define the IPv4 CIDR block and name.
- Click “Create VPC”.  
  ![create-VPC](images/3.png)  
  ![VPC-created](images/5.png)

### 2.3 Configure VPC

- Enable DNS hostname resolution.
- Confirm instance tenancy is default.

### 2.4 Create Subnets

- Go to “Subnets” and click “Create Subnet”.  
  ![create-subnet](images/7.png)
- Select the VPC created.
- Input subnet names, select availability zones, and assign CIDR blocks.  
  ![create-subnet](images/10.png)
- Add additional subnets and click “Create”.  
  ![subnet-created](images/12.png)

### 2.5 Set Up Internet Gateway

- Navigate to “Internet Gateways” > “Create Internet Gateway”.  
  ![create-internetgateway](images/13.png)
- Name and create the gateway.
- Attach it to your VPC.  
  ![attach-internetgateway](images/17.png)

### 2.6 Configure Route Tables

- Go to “Route Tables” > “Create Route Table”.
- Assign a name and associate it with the VPC.
- Associate public subnets to the route table.
- Edit Routes to add:  
  - Destination: 0.0.0.0/0  
  - Target: Internet Gateway  
  ![edit-route](images/24.png)

### 2.7 Set Up NAT Gateway

- Navigate to “NAT Gateways” > “Create NAT Gateway”.  
  ![create-NAT-Gateway](images/26.png)
- Name the gateway and select the private subnet.
- Click “Create”.
- Update the private subnet’s route table:  
  - Destination: 0.0.0.0/0  
  - Target: NAT Gateway  
  ![edit-route](images/32.png)

### 2.8 VPC Peering

- Create two VPCs in the same region.  
  ![two-VPC](images/36.png)
- Go to “Peering Connections” > “Create Peering Connection”.
- Fill in requester/accepter details and click “Create”.  
  ![create-peering-connection](images/39.png)
- Accept the peering request and update route tables in both VPCs for cross-VPC traffic.  
  ![create-peering-connection](images/51.png)

---

## Troubleshooting

### 3.1 VPC Not Connecting to Internet

- Ensure the Internet Gateway is attached.
- Verify route table includes `0.0.0.0/0` pointing to IGW.

### 3.2 Subnet Routing Issues

- Confirm NAT Gateway route exists for private subnets.
- Ensure subnet associations with the correct route table.

### 3.3 VPC Peering Not Working

- Check if peering connection is accepted.
- Ensure both route tables include the CIDR blocks of the peer VPC.

### 3.4 NAT Gateway Connectivity Issues

- Confirm NAT Gateway is in a public subnet.
- Ensure route table for private subnet includes the NAT Gateway.
- Confirm Elastic IP is assigned to NAT Gateway.

---

> ⚠️ Note: AWS enforces CIDR block sizes between `/16` and `/28` — ensure input values conform to this range.

