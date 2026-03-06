# AWS Secure Multi-Tier Architecture

This project demonstrates a secure and scalable AWS cloud architecture built using core networking and compute services.

The architecture follows a multi-tier design separating public and private resources for improved security and scalability.

---

## Architecture Diagram

<img width="1024" height="1536" alt="architecture" src="https://github.com/user-attachments/assets/fc9bd754-18bb-47ef-9df9-102a5b792cfc" />


---

## AWS Services Used

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- NAT Gateway
- Application Load Balancer
- EC2 Instances
- Security Groups
- Route Tables
- CloudWatch Monitoring

---

## Architecture Components

### VPC
A custom VPC was created with CIDR block:

10.0.0.0/16

This VPC contains both public and private subnets.

---

### Public Subnets
Public subnets host internet-facing components:

- Application Load Balancer
- Web EC2 Instance

These subnets have route access to the Internet Gateway.

---

### Private Subnets
Private subnets host internal services:

- Application Server
- Database Layer

These resources are not accessible directly from the internet.

---

### Internet Gateway
The Internet Gateway allows public subnets to communicate with the internet.

---

### NAT Gateway
Private instances use the NAT Gateway to access the internet for updates without exposing themselves publicly.

---

### Application Load Balancer
The Application Load Balancer distributes incoming traffic across EC2 instances.

Traffic flow:

User → Load Balancer → Web EC2

---

### Security Groups

**Web-SG**

Inbound:
- HTTP (80) from 0.0.0.0/0
- SSH (22) from developer IP

**App-SG**

Inbound:
- Application traffic from Web-SG only

**DB-SG**

Inbound:
- MySQL 3306 from App-SG only

---

## Traffic Flow

1. User sends HTTP request
2. Request reaches Application Load Balancer
3. Load balancer forwards request to Web EC2 instance
4. Web server processes request
5. Application server communicates with database
6. Response returned to user

---

## Monitoring

CloudWatch is used to monitor instance performance.

Example alarm created:

CPUUtilization > 70%

This triggers alerts when the system is under heavy load.

---

## Project Screenshots

Screenshots of the AWS resources are available in the screenshots folder.

Included resources:

- VPC
- Subnets
- Route Tables
- NAT Gateway
- Security Groups
- EC2 Instance
- Application Load Balancer
- Target Group
- CloudWatch Alarm

---

## Key Learning Outcomes

- Designing secure VPC network architecture
- Implementing public and private subnet isolation
- Configuring Application Load Balancer
- Managing security using Security Groups
- Monitoring infrastructure using CloudWatch
