# AWS VPC Guide

## Introduction to VPC
A **Virtual Private Cloud (VPC)** is like your own private network within AWS. It lets you control networking settings, create subnets, and securely connect your cloud resources.

This guide will help you set up a VPC with **two public and two private subnets** step by step.

---

## 1. Creating a VPC
To start, create a new VPC:
- Go to the AWS **VPC Dashboard**.
- Click on **Create VPC**.
- Name your VPC and assign an IPv4 CIDR block (e.g., `10.0.0.0/16`).
- Click **Create**.

---

## 2. Adding Public and Private Subnets
After creating the VPC, add subnets:
- Create **two public subnets** (e.g., `10.0.1.0/24` and `10.0.2.0/24`).
- Create **two private subnets** (e.g., `10.0.3.0/24` and `10.0.4.0/24`).
- Assign them to different Availability Zones for high availability.

---

## 3. Setting Up an Internet Gateway (IGW)
For internet access, attach an **Internet Gateway**:
- Go to **Internet Gateways**.
- Click **Create Internet Gateway** and give it a name.
- Attach it to your VPC.

---

## 4. Configuring Route Tables
Now, configure routing:
- **Public Route Table:**
  - Add a route to `0.0.0.0/0` (all internet traffic) and point it to the **Internet Gateway**.
  - Associate this route table with **public subnets**.
- **Private Route Table:**
  - No direct internet access is needed.
  - Associate this table with **private subnets**.

---

## 5. Setting Up Security Groups
Security Groups act as firewalls for your instances:
- **Public Instance Security Group:**
  - Allow inbound SSH (`22`), HTTP (`80`), and HTTPS (`443`).
  - Outbound traffic: Allow all.
- **Private Instance Security Group:**
  - Allow only internal traffic from the public instances.

---

## 6. Launching EC2 Instances
Now, deploy servers:
- **Public Instance:** Launch an EC2 instance in a public subnet.
- **Private Instance:** Launch another EC2 instance in a private subnet.

To install Apache on the public instance:
```sh
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```
Now, your public instance can serve web pages!

---

## 7. Adding a Virtual Private Gateway (Optional)
If you need a secure connection to your on-premises network, attach a **Virtual Private Gateway**:
- Go to **VPN Gateways** and create a new one.
- Attach it to your VPC.
- Update the **private route table** to send traffic through the VPN.

---

## Final Thoughts
You now have a fully functional **AWS VPC setup** with public and private subnets, internet access, and security rules in place. You can expand it by adding load balancers, NAT gateways, or connecting it to another network!

