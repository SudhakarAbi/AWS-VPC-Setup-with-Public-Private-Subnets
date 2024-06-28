# AWS-VPC-Setup-with-Public-Private-Subnets

## Title: Setting Up a Secure AWS VPC with Public and Private Subnets

### Introduction
- Overview of AWS Virtual Private Cloud (VPC) and its importance
- Objective of the lab: Setting up a secure VPC with public web servers and private database servers

### Prerequisites
- AWS account with necessary permissions (IAM roles)
- Basic familiarity with AWS Management Console
- Understanding of networking concepts (CIDR blocks, subnets, routing)

### Step 1: Creating the VPC
- Walkthrough of creating a new VPC in AWS Management Console
- Selection of IPv4 CIDR block for the VPC (e.g., `10.0.0.0/16`)
- Naming conventions and tags for the VPC

### Step 2: Creating Subnets
#### Public Subnet
- Purpose: Hosting Apache web server accessible from the internet
- Steps to create a public subnet within the VPC
- Selection of IPv4 CIDR block for the public subnet (e.g., `10.0.1.0/24`)
- Association with Internet Gateway (IGW) for internet access
- Configuration of route table for the public subnet to route traffic through the IGW

#### Private Subnet
- Purpose: Hosting MySQL database server with restricted access
- Steps to create a private subnet within the VPC
- Selection of IPv4 CIDR block for the private subnet (e.g., `10.0.2.0/24`)
- Configuration of route table for the private subnet:
  - No direct route to the IGW for enhanced security
  - Route for SSH access from specific IP ranges (e.g., public subnet instance IPs)

### Step 3: Instance Deployment and Configuration
#### Public Subnet Instance (Apache Web Server)
- Deployment of an EC2 instance in the public subnet
- Installation of Apache HTTP Server with custom design
- Verification of Apache web server functionality

#### Private Subnet Instance (MySQL Database Server)
- Deployment of an EC2 instance in the private subnet
- Installation and configuration of MySQL database server
- Testing connectivity from the public subnet instance to the private subnet instance

### Step 4: Security Configuration
- Configuration of Security Groups:
  - Public subnet security group allowing inbound HTTP/HTTPS (optional SSH)
  - Private subnet security group allowing inbound SSH from specific IP ranges only
- Overview of Network ACLs:
  - Default and custom Network ACL rules for inbound and outbound traffic control

### Step 5: Testing and Verification
- Testing access to the Apache web server from the internet
- SSH access from the public subnet instance to the private subnet instance using private IP
- Verification of MySQL connectivity and database operations from the public subnet instance

### Conclusion
- Summary of key steps and configurations for a secure AWS VPC setup
- Importance of implementing AWS security best practices for VPCs
- Next steps for further enhancing VPC security and scalability

### References
- Links to official AWS documentation and resources
- Additional reading materials on AWS VPC design and security best practices
