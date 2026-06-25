
🚀 AWS Auto Scaling Lab (EC2 + ALB + AMI)

<img width="86" height="20" alt="image" src="https://github.com/user-attachments/assets/7c3cccbd-cc48-4ebd-a37c-ed5bd1ea6610" />
<img width="146" height="20" alt="image" src="https://github.com/user-attachments/assets/09a19e66-16ba-4066-a7a3-59286767e9a1" />

📖 Project Overview

This project demonstrates the implementation of a scalable and highly available architecture on AWS using:

Amazon EC2
Custom AMI
Application Load Balancer (ALB)
Auto Scaling Group (ASG)

The system automatically adjusts the number of EC2 instances based on CPU usage, ensuring performance, fault tolerance, and elasticity.

🎯 Objectives
Launch EC2 instances using AWS CLI
Create a custom Amazon Machine Image (AMI)
Configure an Application Load Balancer (ALB)
Deploy a Launch Template for EC2 provisioning
Create an Auto Scaling Group (ASG)
Configure dynamic scaling policies based on CPU utilization
Ensure high availability across multiple Availability Zones

🏗 Solution Architecture
                    Users
                      │
                      ▼
        ┌─────────────────────────────┐
        │ Application Load Balancer   │
        │          (ALB)              │
        └────────────┬────────────────┘
                     │
     ┌───────────────┴───────────────┐
     │                               │
     ▼                               ▼
 EC2 Instance 1                EC2 Instance 2
 (Auto Scaling)               (Auto Scaling)
     │                               │
     └───────────────┬───────────────┘
                     ▼
           Auto Scaling Group (ASG)
                     │
                     ▼
          Launch Template + AMI
                     │
                     ▼
            Amazon Linux 2023

| Service                   | Purpose                |
| ------------------------- | ---------------------- |
| Amazon EC2                | Virtual servers        |
| Amazon AMI                | Custom machine image   |
| Application Load Balancer | Traffic distribution   |
| Auto Scaling Group        | Automatic scaling      |
| Launch Template           | Instance configuration |
| AWS CLI                   | Automation             |
| Amazon Linux 2023         | Operating system       |

🛠 Implementation Steps
Step 1 – Launch EC2 via AWS CLI

An EC2 instance (Command Host) was used to execute AWS CLI commands.

aws ec2 run-instances \
--key-name vockey \
--instance-type t3.micro \
--image-id ami-XXXXXXXXX \
--user-data file:///home/ec2-user/UserData.txt \
--security-group-ids sg-XXXXXXXXX \
--subnet-id subnet-XXXXXXXXX \
--associate-public-ip-address \
--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=WebServer}]'

Step 2 – Create Custom AMI
aws ec2 create-image \
--name WebServerAMI \
--instance-id i-XXXXXXXXX
Step 3 – Create Application Load Balancer

Configuration:
| Parameter    | Value                     |
| ------------ | ------------------------- |
| Name         | WebServerELB              |
| Type         | Application Load Balancer |
| Target Group | webserver-app             |
| Health Check | /index.php                |
| Protocol     | HTTP                      |

Step 4 – Create Launch Template
| Parameter      | Value                   |
| -------------- | ----------------------- |
| Name           | web-app-launch-template |
| AMI            | WebServerAMI            |
| Instance Type  | t3.micro                |
| Security Group | HTTPAccess              |

Step 5 – Create Auto Scaling Group

Configuration:
| Parameter        | Value                      |
| ---------------- | -------------------------- |
| Name             | Web App Auto Scaling Group |
| Min Capacity     | 2                          |
| Desired Capacity | 2                          |
| Max Capacity     | 4                          |
| Subnets          | Private Subnet 1 & 2       |
| Scaling Policy   | Target Tracking            |
| Metric           | CPU Utilization (50%)      |

📊 Auto Scaling Behavior
Normal Load
2 EC2 Instances running
High Load
Auto Scaling adds new EC2 instances
Low Load
Instances are terminated automatically
🧪 Validation

✔ Target Group health checks passed
✔ ALB DNS successfully reachable
✔ EC2 instances registered automatically
✔ Auto Scaling policies triggered correctly
✔ CPU-based scaling verified

📚 Skills Demonstrated
AWS EC2
AWS CLI Automation
Amazon Machine Images (AMI)
Application Load Balancer (ALB)
Auto Scaling Groups (ASG)
Launch Templates
Cloud Architecture Design
High Availability Systems
Scalability Engineering
🎓 Learning Outcomes

This project demonstrates:

How to build elastic cloud infrastructure
How to automate EC2 provisioning
How to design fault-tolerant systems
How AWS handles auto scaling under load
How to implement real production-like architecture

📊 Auto Scaling Behavior
Normal Load
2 EC2 Instances running
High Load
Auto Scaling adds new EC2 instances
Low Load
Instances are terminated automatically
🧪 Validation

✔ Target Group health checks passed
✔ ALB DNS successfully reachable
✔ EC2 instances registered automatically
✔ Auto Scaling policies triggered correctly
✔ CPU-based scaling verified

📚 Skills Demonstrated
AWS EC2
AWS CLI Automation
Amazon Machine Images (AMI)
Application Load Balancer (ALB)
Auto Scaling Groups (ASG)
Launch Templates
Cloud Architecture Design
High Availability Systems
Scalability Engineering
🎓 Learning Outcomes

📌 Author

Paulo Henriue

AWS Cloud Practitioner Candidate | Cloud & DevOps Enthusiast
