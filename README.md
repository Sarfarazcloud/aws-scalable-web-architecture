# AWS Scalable Web Architecture

## 1. What I built

I built a highly available and fault-tolerant web architecture using AWS services. The system serves a web page through a load balancer and automatically handles failures and scaling.

---

## 2. Architecture (in words)

Users access the application through a public Application Load Balancer.  
The load balancer routes traffic to EC2 instances running in private subnets.  
These instances are managed by an Auto Scaling Group, which ensures availability.  
The system is stateless, and logs are sent to CloudWatch.

## Architecture Flow

User → Load Balancer → EC2 Instance → Response

- User sends request  
- ALB receives traffic  
- ALB forwards to healthy EC2  
- EC2 serves nginx page  

---

## 3. Key components

- VPC (network isolation)
- Public and Private Subnets
- Application Load Balancer (ALB)
- EC2 Instances
- Auto Scaling Group (ASG)
- S3 (for storage)
- CloudWatch (for logs)

---

## 4. How scaling works

- Auto Scaling Group maintains a desired capacity of 2 instances  
- When an instance is terminated, ASG automatically launches a new one  
- During testing, I manually terminated an instance and observed automatic recovery  
---

## 5. How failure is handled

If an EC2 instance is terminated:

- ASG launches a new instance automatically  
- ALB routes traffic only to healthy instances  
- Users do not experience downtime  

---

## 6. What I learned

- How to design a stateless architecture  
- Importance of load balancing and auto scaling  
- How to handle failures automatically  
- Basics of cloud monitoring using CloudWatch  

---

## 7. Security Considerations

- EC2 instances are in private subnets (not publicly accessible)  
- Only ALB is exposed to the internet
  
---

## 8. Testing & Observations

- Verified load balancing by displaying instance IDs on the webpage  
- Observed different instance IDs on refresh → confirms traffic distribution  
- Simulated failure by terminating an instance  
- Observed ASG launching replacement automatically  
- No downtime observed during failure  
  
---

## Key Design Decisions

- Used private EC2 instances to improve security and reduce direct exposure  
- Used Application Load Balancer as a single entry point for users  
- Designed system to be stateless so instances can be replaced easily  
- Used Auto Scaling Group for automatic recovery and scaling  
  
---

## Problem Solved

A single EC2-based system can fail and cause downtime.  
This architecture solves that by introducing load balancing, auto scaling, and stateless design.