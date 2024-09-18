AWS 2-Tier VPC Architecture

Overview
- This README outlines the setup of a 2-tier VPC architecture on AWS. The architecture is designed to separate the presentation layer (frontend) from the application layer (backend), enhancing security and scalability.

Architecture Diagram

![Alt text](https://github.com/kiran877/2-tier-example-VPC/blob/main/architecture-vpc.png)

Components

- VPC (Virtual Private Cloud): A logically isolated network for resources.
- Public Subnet: Hosts the frontend resources (e.g., web servers).
- Private Subnet: Hosts the backend resources (e.g., application servers, databases).
- Internet Gateway: Allows communication between resources in the public subnet and the internet.
- NAT Gateway: Allows outbound internet access for resources in the private subnet.
- Security Groups: Acts as a virtual firewall for your instances.

Prerequisites

- AWS Account
- AWS CLI installed and configured
- IAM permissions to create VPCs, subnets, security groups, etc.

Architecture Setup

Step 1: Create the VPC
- Navigate to the VPC dashboard in the AWS Management Console.
- Click on "Create VPC".
- Specify the CIDR block (e.g., 10.0.0.0/16).

Step 2: Create Subnets

Public Subnet
- Click on "Subnets" and then "Create subnet".
- Select your VPC and specify a CIDR block (e.g., 10.0.1.0/24).
- Enable auto-assign public IPv4 address.

Private Subnet
- Create another subnet with a CIDR block (e.g., 10.0.2.0/24).

Step 3: Set Up Internet Gateway
- In the VPC dashboard, click on "Internet Gateways" and create a new gateway.
- Attach the internet gateway to your VPC.

Step 4: Configure Route Tables
- Create a route table for the public subnet and add a route to the internet (destination 0.0.0.0/0 via the internet gateway).
- Create a route table for the private subnet and configure it to use the NAT Gateway for outbound traffic.

Step 5: Set Up Security Groups
- Create a security group for the public subnet allowing HTTP/HTTPS traffic.
- Create a security group for the private subnet allowing traffic only from the public subnet security group.

Step 6: Launch Resources
- Deploy your web servers in the public subnet and your application servers/database in the private subnet.

Configuration
- Ensure that your instances are properly configured with the appropriate security group rules.
- Set up IAM roles and policies for your resources as necessary.

Testing
- Access the application via the public IP of the web servers.
- Ensure that the backend services are reachable from the frontend.

Cleanup
- To avoid incurring charges, remember to delete the VPC and all associated resources when you're done testing.

References
- AWS VPC Documentation
- AWS Security Groups