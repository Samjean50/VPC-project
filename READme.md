# Mini Project - AWS VPC - Virtual Private Cloud

## Network Mastery with AWS VPC Mini Project

### Project Overview
This project showcases practical expertise in designing and configuring a secure, scalable network infrastructure using Amazon Web Services (AWS) Virtual Private Cloud (VPC). The project includes the complete setup of VPC components such as subnets, route tables, Internet and NAT Gateways, and VPC Peering. The goal was to implement a robust cloud networking environment following AWS best practices for security, availability, and maintainability.


### Steps:
1. Setting Up a Virtual Private Cloud (VPC).
2. Configuring Subnets within the VPC.
3. Creating an Internet Gateway and attaching it to the VPC.
4. Enabling Internet Connectivity with the Internet Gateway by setting up Routing Tables.
5. Enabling Outbound Internet Access through a NAT Gateway.
6. Establishing VPC Peering Connections.

## Part 1 - Setting Up a Virtual Private Cloud (VPC)
1. Navigate to the search bar and enter "VPC", then click on the VPC icon.
   ![search-VPC](images/1.png)
2. Click on "Create VPC".
   ![click-VPC](images/2.png)
3. Select "VPC only", specify the IPv4 CIDR block, and click "Create VPC".
   ![create-VPC](images/3.png)
   ![create-VPC](images/4.png)
   ![VPC-created](images/5.png)

## Part 2 - Configuring Subnets within the VPC
1. Navigate to "Subnets" on the left sidebar and click "Create Subnet".
   ![create-subnet](images/7.png)
2. Select the VPC ID created in Part 1.
   ![create-subnet](images/8.png)
3. Enter the subnet name, choose the availability zone, and specify the IPv4 CIDR.
   ![create-subnet](images/10.png)
4. Click "Add subnet" to create another subnet and repeat the steps.
   ![create-subnet](images/9.png)
5. Click "Create" to finalize the subnet creation.
   ![create-subnet](images/11.png)
   ![subnet-created](images/12.png)

## Part 3 - Creating Internet Gateway and Attaching it to VPC
1. Navigate to "Internet Gateway" on the left sidebar and click "Create Internet Gateway".
   ![create-internetgateway](images/13.png)
2. Enter the Internet Gateway name and click "Create Internet Gateway".
   ![internetgateway-created](images/14.png)
3. Attach the Internet Gateway to the VPC.
   ![attach-internetgateway](images/15.png)
   ![attach-internetgateway](images/16.png)
   ![attach-internetgateway](images/17.png)

## Part 4 - Enabling Internet Connectivity with Routing Tables
1. Navigate to "Route Tables".
   ![route-tables](images/18.png)
2. Enter the route table name, select the VPC, and click "Create Route Table".
   ![route-tables](images/19.png)
3. Associate the public subnet with this route table.
   ![route-tables](images/20.png)
4. Click "Edit Routes" and add a route:
   - Destination: `0.0.0.0/0`
   - Target: Internet Gateway
   ![edit-route](images/24.png)

## Part 5 - Enabling Outbound Internet Access through NAT Gateway
1. Navigate to "NAT Gateways" and click "Create NAT Gateway".
   ![create-NAT-Gateway](images/26.png)
2. Enter the NAT Gateway name, select the private subnet, and set connectivity to Private.
   ![create-NAT-Gateway](images/27.png)
3. Click "Create NAT Gateway".
   ![create-NAT-Gateway](images/28.png)
4. Add a route for the private subnet:
   - Destination: `0.0.0.0/0`
   - Target: NAT Gateway
   ![edit-route](images/32.png)

## Part 6 - Establishing VPC Peering Connections
1. Create two VPCs in the same region.
   ![two-VPC](images/36.png)
   ![two-VPC](images/37.png)
2. Navigate to "Peering Connections" and click "Create Peering Connection".
   ![create-peering-connection](images/38.png)
3. Provide a name, select the requester VPC, choose "My account", select the accepter VPC, and click "Create Peering Connection".
   ![create-peering-connection](images/39.png)
4. Accept the Peering Connection request.
   ![create-peering-connection](images/40.png)
   ![create-peering-connection](images/41.png)
5. Update the route tables for both VPCs to allow communication via the Peering Connection.
   ![create-peering-connection](images/50.png)
   ![create-peering-connection](images/51.png)

### Troubleshooting
- If you encounter an error stating the CIDR block must be between `/16` and `/28`, adjust the CIDR block size accordingly.