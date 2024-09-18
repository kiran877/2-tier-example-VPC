AWS 2-Tier VPC Architecture

Overview
This README outlines the setup of a 2-tier VPC architecture on AWS. The architecture is designed to separate the presentation layer (frontend) from the application layer (backend), enhancing security and scalability.

Architecture Diagram

![Alt text]()

Components

1.VPC (Virtual Private Cloud): A logically isolated network for resources.
2.Public Subnet: Hosts the frontend resources (e.g., web servers).
3.Private Subnet: Hosts the backend resources (e.g., application servers, databases).
4.Internet Gateway: Allows communication between resources in the public subnet and the internet.
5.NAT Gateway: Allows outbound internet access for resources in the private subnet.
5.Security Groups: Acts as a virtual firewall for your instances.

Prerequisites

AWS Account
AWS CLI installed and configured
IAM permissions to create VPCs, subnets, security groups, etc.

Architecture Setup

Step 1: Create the VPC
1.Navigate to the VPC dashboard in the AWS Management Console.
2.Click on "Create VPC".
3.Specify the CIDR block (e.g., 10.0.0.0/16).

Step 2: Create Subnets

Public Subnet
1.Click on "Subnets" and then "Create subnet".
2.Select your VPC and specify a CIDR block (e.g., 10.0.1.0/24).
3.Enable auto-assign public IPv4 address.

Private Subnet
1.Create another subnet with a CIDR block (e.g., 10.0.2.0/24).

Step 3: Set Up Internet Gateway
1.In the VPC dashboard, click on "Internet Gateways" and create a new gateway.
2.Attach the internet gateway to your VPC.

Step 4: Configure Route Tables
1.Create a route table for the public subnet and add a route to the internet (destination 0.0.0.0/0 via the internet gateway).
2.Create a route table for the private subnet and configure it to use the NAT Gateway for outbound traffic.

Step 5: Set Up Security Groups
1.Create a security group for the public subnet allowing HTTP/HTTPS traffic.
2.Create a security group for the private subnet allowing traffic only from the public subnet security group.

Step 6: Launch Resources
Deploy your web servers in the public subnet and your application servers/database in the private subnet.

Configuration
Ensure that your instances are properly configured with the appropriate security group rules.
Set up IAM roles and policies for your resources as necessary.

Testing
Access the application via the public IP of the web servers.
Ensure that the backend services are reachable from the frontend.

Cleanup
To avoid incurring charges, remember to delete the VPC and all associated resources when you're done testing.

References
AWS VPC Documentation
AWS Security Groups