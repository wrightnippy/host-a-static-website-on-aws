![Alt text](/Host_a_Static_Website_on_AWS.png).
# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on **AWS** using a secure, scalable, and highly available architecture. It leverages multiple AWS services such as EC2, VPC, Route 53, and Auto Scaling to deploy and manage the website infrastructure.

---

## 📖 Project Overview

The goal of this project was to design and deploy a static website hosted on **EC2 instances** in a private subnet, behind an **Application Load Balancer (ALB)**, while ensuring high availability, scalability, and fault tolerance.

A reference architecture diagram and deployment scripts are included in this repository.

---

## 🏗️ Architecture Components

1. **VPC Configuration**

   * Public and private subnets across **two Availability Zones**.
   * **Internet Gateway** for public internet access.
   * **NAT Gateway** in public subnets for outbound internet access from private instances.

2. **Security**

   * Security Groups configured as firewalls to control inbound and outbound traffic.
   * EC2 Instance Connect Endpoint for secure access.

3. **Compute & Scaling**

   * Web servers deployed on **EC2 instances** in private subnets.
   * **Application Load Balancer (ALB)** to distribute traffic evenly.
   * **Auto Scaling Group (ASG)** for elasticity, fault tolerance, and high availability.

4. **Networking & DNS**

   * Route 53 used for domain registration and DNS record management.
   * SSL/TLS encryption configured with **AWS Certificate Manager**.

5. **Monitoring & Alerts**

   * **SNS (Simple Notification Service)** configured to send notifications for Auto Scaling Group activities.

6. **Version Control**

   * Website source code stored in **GitHub** for collaboration and versioning.

---

## ⚙️ Deployment Script (User Data)

The following script installs and configures Apache, pulls the static site from GitHub, and serves it on EC2:

```bash
#!/bin/bash
# Switch to root
sudo su

# Update installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change directory to Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy files to Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository
rm -rf host-a-static-website-on-aws

# Enable and start Apache
systemctl enable httpd
systemctl start httpd
```

---

## 🚀 How to Deploy

1. Launch an **EC2 instance** in the private subnet with the above **user data script**.
2. Attach the instance to an **Auto Scaling Group** behind an **Application Load Balancer**.
3. Ensure the ALB security group allows inbound HTTP/HTTPS traffic.
4. Configure **Route 53** to point your domain to the ALB’s DNS name.
5. Access your website using your registered domain name.

---

## 📂 Repository Contents

* **/diagrams** → Architecture diagrams
* **/scripts** → Deployment scripts
* **README.md** → Project documentation

---

## ✅ Key Benefits

* High availability across multiple Availability Zones.
* Fault tolerance with Auto Scaling and Load Balancing.
* Secure infrastructure with private subnets and SSL/TLS.
* Automated deployments with GitHub version control.

---

## 🌐 Live Demo

[Visit Website](http://your-domain.com) (replace with your actual domain or ALB DNS)

---

Would you like me to also **include the architecture diagram directly inside the README** (as an embedded image) so it looks professional on GitHub?

