# HTML Website Hosting on AWS EC2

<img width="1387" alt="Screenshot 2023-12-13 at 2 51 42 PM" src="https://github.com/bconway1906/Host-HTML-Website-on-AWS/assets/148906255/1d4316c2-a5a5-4deb-b6be-6604b724d203">

## Project Overview

In this DevOps project, I hosted an HTML website on AWS, specifically on a single EC2 instance within the default VPC. The following steps outline the process I followed, along with the associated scripts and resources.

## Steps and Explanations

### 1. Region Selection

I chose the North Virginia region (US-East-1) for its performance and availability benefits.

### 2. Security Group Configuration

To control inbound and outbound traffic, I created a security group with the following inbound rules:
- HTTP Port 80 from anywhere (IPv4): Allows web traffic.
- SSH Port 22 from MyIP: Provides secure SSH access.

### 3. EC2 Instance Launch

Launched an EC2 instance and associated it with the previously created security group.

### 4. Key Pair Creation

During EC2 instance creation, I generated a new key pair. AWS provided a private key file (.pem), which I downloaded and securely stored. This key pair is crucial for SSH access to the EC2 instance.

### 5. SSH Access

Used the terminal and the key pair to SSH into the EC2 instance, copying the Public IPv4 address.

```bash
ssh -i path/to/keypair.pem ec2-user@your-public-ipv4-address
```

### 6. HTML Website Deployment Script

Executed the following script to deploy the HTML website:

```bash
sudo su                 # Switched to the root user for necessary privileges.
yum update -y           # Updated the instance with security patches and updates.
yum install -y httpd    # Installed Apache, the web server software.
cd /var/www/html        # Changed the directory to the HTML folder.
wget https://github.com/azeezsalu/techmax/archive/refs/heads/main.zip   # Downloaded the website files.
unzip main.zip          # Unzipped the downloaded folder.
cp -r techmax-main/* /var/www/html/    # Copied files to the HTML directory.
rm -rf techmax-main main.zip           # Deleted unnecessary folders.
systemctl enable httpd  # Enabled the Apache server.
systemctl start httpd   # Started the Apache server.
```

### 7. Website Access

Copied the Public IPv4 address to access the newly hosted HTML website.

## Conclusion

The project successfully hosted an HTML website on an AWS EC2 instance in the default VPC.
