## Setting Up a Secure AWS VPC with Public and Private Subnets using Ubuntu

### Introduction
In this guide, we will walk through setting up a secure AWS Virtual Private Cloud (VPC) with public and private subnets using Ubuntu instances. We'll cover creating subnets, attaching an Internet Gateway (IGW), launching Ubuntu EC2 instances with Apache HTTP Server and MySQL, configuring security groups, and verifying connectivity between instances.

### Prerequisites
Before starting, ensure you have:
- An AWS account with administrative access.
- Basic familiarity with AWS Management Console.
- Understanding of networking concepts like CIDR blocks, subnets, and security groups.

### Step 1: Creating the VPC
1. **Log in to AWS Management Console:**
   - Go to [AWS Management Console](https://aws.amazon.com/console/) and log in.

2. **Navigate to VPC Dashboard:**
   - Go to Services > VPC > Your VPCs.

3. **Create a New VPC:**
   - Click on "Create VPC".
   - Enter a name (e.g., `MyVPC`) and a CIDR block (e.g., `10.0.0.0/16`).
   - Click "Create".

### Step 2: Creating Subnets
1. **Create Public Subnet:**
   - Go to Subnets > Create subnet.
   - Select your VPC (`MyVPC`).
   - Enter a name (e.g., `PublicSubnet`) and a CIDR block (e.g., `10.0.1.0/24`).
   - Click "Create".

2. **Create Private Subnet:**
   - Go to Subnets > Create subnet.
   - Select your VPC (`MyVPC`).
   - Enter a name (e.g., `PrivateSubnet`) and a CIDR block (e.g., `10.0.2.0/24`).
   - Click "Create".

### Step 3: Attaching Internet Gateway (IGW)
1. **Create Internet Gateway:**
   - Go to Internet Gateways > Create internet gateway.
   - Attach the IGW to `MyVPC`.

2. **Modify Route Table for Public Subnet:**
   - Go to Route Tables > Select the route table associated with `PublicSubnet`.
   - Edit routes to include `0.0.0.0/0` to IGW.

### Step 4: Launching Ubuntu EC2 Instances
1. **Launch Public Subnet Instance (Apache HTTP Server):**
   - Go to EC2 Dashboard > Instances > Launch Instance.
   - Select an Ubuntu Server AMI.
   - Choose `PublicSubnet`.
   - Configure security group allowing inbound HTTP (port 80) and SSH (port 22) from your IP.
   - Launch the instance, download the `.pem` key.

2. **Launch Private Subnet Instance (MySQL Database Server):**
   - Follow the same steps as above, selecting `PrivateSubnet`.
   - Configure security group allowing inbound SSH from `PublicSubnet` instance's IP only.

### Step 5: Configuring Instances
1. **Configure Public Subnet Instance (Apache HTTP Server):**
   - SSH into the instance using the `.pem` key.
   - Install Apache HTTP Server:
     ```bash
     sudo apt update
     sudo apt install apache2 -y
     sudo systemctl start apache2
     sudo systemctl enable apache2
     ```
   - Create custom HTML page (`index.html`) in `/var/www/html`.

2. **Testing Public Subnet Instance:**
   - Access the Apache server from your web browser using the public IP.

3. **Configure Private Subnet Instance (MySQL Database Server):**
   - SSH into the instance using the `.pem` key.
   - Install MySQL Server:
     ```bash
     sudo apt update
     sudo apt install mysql-server -y
     sudo systemctl start mysql
     sudo systemctl enable mysql
     ```
   - Secure MySQL installation (`mysql_secure_installation`).

### Step 6: Testing and Verification
1. **Testing Connectivity:**
   - From the public subnet instance, SSH into the private subnet instance using its private IP.
   - Test database connectivity from the public subnet instance.

### Conclusion
In this guide, we have successfully set up a secure AWS VPC with public and private subnets using Ubuntu instances. We configured Apache HTTP Server on a public subnet instance and MySQL Database Server on a private subnet instance, ensuring security through proper subnet isolation and security group configurations.

### Next Steps
- Explore further AWS VPC capabilities such as NAT Gateway for outbound internet access from private instances.
- Implement more advanced security features like AWS Security Groups and Network ACLs for fine-grained access control.

---
