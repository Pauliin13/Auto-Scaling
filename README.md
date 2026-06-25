# Auto-Scaling
🚀 AWS Auto Scaling Lab (EC2 + ALB + AMI)










📖 Project Overview

This project demonstrates the implementation of a scalable and highly available web architecture on AWS using:

Amazon EC2
Custom AMI creation
Application Load Balancer (ALB)
Auto Scaling Group (ASG)
AWS CLI automation

The system automatically scales EC2 instances based on CPU utilization, ensuring performance and availability under variable workloads.

🎯 Objectives
Launch EC2 instances using AWS CLI
Create a custom Amazon Machine Image (AMI)
Configure Application Load Balancer (ALB)
Create Launch Template for Auto Scaling
Configure Auto Scaling Group (ASG)
Implement automatic scaling policies based on CPU usage
Distribute traffic across multiple Availability Zones
🏗 Architecture
                Users
                  │
                  ▼
      ┌─────────────────────────┐
      │   Application Load      │
      │     Balancer (ALB)      │
      └──────────┬──────────────┘
                 │
     ┌───────────┴───────────┐
     ▼                       ▼
 EC2 Instance 1        EC2 Instance 2
 (Auto Scaling)        (Auto Scaling)
     │                       │
     └───────────┬───────────┘
                 ▼
        Auto Scaling Group
                 │
                 ▼
         Custom AMI (WebServer)
⚙️ AWS Services Used
Service	Purpose
Amazon EC2	Virtual servers
Amazon Machine Image (AMI)	Custom server image
Application Load Balancer	Traffic distribution
Auto Scaling Group	Automatic scaling
AWS CLI	Automation commands
Amazon VPC	Network isolation
🔧 Environment Configuration
EC2 Command Host
Parameter	Value
Instance Type	t3.micro
OS	Amazon Linux
Access	AWS CLI
Key Lab Resources
Resource	Value
AMI ID	ami-0549cb03a33d34ee8
Security Group	sg-056f9eb185a9e49f5
Subnet ID	subnet-07d56fcab8a7cba48
Key Pair	vockey
🛠 Implementation Steps
Step 1 - Launch EC2 via AWS CLI
aws ec2 run-instances \
--key-name vockey \
--instance-type t3.micro \
--image-id ami-0549cb03a33d34ee8 \
--user-data file:///home/ec2-user/UserData.txt \
--security-group-ids sg-056f9eb185a9e49f5 \
--subnet-id subnet-07d56fcab8a7cba48 \
--associate-public-ip-address \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=WebServer}]'

✔ Result: WebServer instance created successfully

Step 2 - Wait for Instance
aws ec2 wait instance-running --instance-ids i-xxxxxxxx
Step 3 - Get Public DNS
aws ec2 describe-instances \
--instance-ids i-xxxxxxxx \
--query 'Reservations[0].Instances[0].PublicDnsName'

✔ Web application accessible via:

http://PUBLIC-DNS/index.php
Step 4 - Create AMI
aws ec2 create-image \
--name WebServerAMI \
--instance-id i-xxxxxxxx

✔ Custom AMI created successfully

Step 5 - Create Application Load Balancer
Type: Application Load Balancer
Name: WebServerELB
VPC: Lab VPC
Subnets: Public Subnet 1 & 2
Target Group: webserver-app
Health Check: /index.php

✔ ALB active and distributing traffic

Step 6 - Create Launch Template
Name: web-app-launch-template
AMI: WebServerAMI
Instance Type: t3.micro
Security Group: HTTPAccess

✔ Launch Template created successfully

Step 7 - Create Auto Scaling Group

Configuration:

Parameter	Value
Desired Capacity	2
Minimum	2
Maximum	4
Subnets	Private Subnet 1 & 2
Policy	Target Tracking
Metric	CPU Utilization
Target	50%

✔ Auto Scaling Group active

Step 8 - Load Test
Access ALB DNS
Trigger CPU stress test
Monitor scaling activity

✔ New instances automatically launched when CPU > 50%

📊 Results
✔ EC2 launched via CLI
✔ AMI created successfully
✔ ALB distributing traffic
✔ Auto Scaling working
✔ Multi-AZ deployment active
✔ Automatic scaling validated
📚 Skills Demonstrated
AWS EC2 Management
AWS CLI Automation
AMI Creation
Load Balancer Configuration
Auto Scaling Policies
Cloud Architecture Design
High Availability Systems
🎓 Learning Outcomes

This project demonstrates:

How to build scalable cloud infrastructure
How AWS Auto Scaling reacts to demand
How Load Balancers distribute traffic
How AMIs are used for scaling templates
How CLI can automate AWS infrastructure
📂 Repository Structure
aws-auto-scaling-lab-175
│
├── README.md
├── scripts
│   ├── create-instance.sh
│   ├── create-ami.sh
│   └── describe-instances.sh
│
└── docs
    └── lab-notes.md
👤 Author

Paulo Henrique

Cloud Computing Student | AWS | DevOps | Infrastructure Enthusiast
