# AWS Static Website Deployment

## Overview

This project demonstrates the deployment of a static HTML website on AWS using various services to ensure high availability, fault tolerance, and security. The infrastructure is set up in a Virtual Private Cloud (VPC) with public and private subnets across two availability zones.

## Project Architecture

![Reference_Architecture](https://github.com/bconway1906/Deploy-Static-Website-AWS/assets/148906255/8fb30e4a-0e6e-4965-96f1-ddef62aaa559)

### Components:

1. **VPC Configuration:**
   - A VPC is created with public and private subnets spread across two availability zones for high availability and fault tolerance.

2. **Internet Gateway:**
   - An Internet Gateway is utilized to allow communication between instances in the VPC and the internet.

3. **Security Groups:**
   - Security Groups are configured to act as a firewall for EC2 instances, controlling inbound and outbound traffic.

4. **Availability Zones:**
   - Resources such as Nat Gateway, Bastion Host, and Application Load Balancer (ALB) use public subnets spread across multiple availability zones.

5. **EC2 Instance Connect:**
   - EC2 Instance Connect is used for secure SSH access to resources in both public and private subnets.

6. **Private Subnets:**
   - Web servers and database servers are placed in private subnets to enhance security.

7. **Nat Gateway:**
   - The Nat Gateway allows instances in private subnets to access the internet securely.

8. **EC2 Instances:**
   - EC2 instances host the static HTML website. The instances are part of an Auto Scaling Group (ASG) for high availability.

9. **Application Load Balancer:**
   - An ALB is used to distribute web traffic across the Auto Scaling Group of EC2 instances in multiple availability zones.

10. **Auto Scaling Group:**
    - ASG dynamically creates and manages EC2 instances, ensuring the website is highly available, scalable, fault-tolerant, and elastic.

11. **Route 53:**
    - Route 53 is used to register the domain name and create a record set for the static website.

12. **GitHub:**
    - GitHub is used to store web files, allowing for version control and easy deployment.

### Deployment Script:

```bash
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
wget https://github.com/bconway1906/staticsite/raw/main/static-main.zip
unzip static-main.zip
cp -r /var/www/html/static-main/* /var/www/html
rm -rf static-main.zip static-main
systemctl enable httpd
systemctl start httpd
```

## Conclusion

This project demonstrates a comprehensive setup for hosting a static website on AWS, utilizing various services to achieve high availability, security, and scalability. The provided deployment script simplifies the process of installing and running the web application on EC2 instances. 
