# Auto-Healing-Production-Web-Application-with-Real-Time-Incident-Detection-Recovery
Deployed a highly available, fault-tolerant web application on AWS simulating a production environment. Implemented auto-healing and real-time incident detection by leveraging AWS Auto Scaling and Load Balancer health checks.

Tools/Technologies: AWS EC2, Launch Template, Auto Scaling Group (ASG), Application Load Balancer (ALB), Target Groups, Security Groups, VPC, Public Subnets, Nginx Web Server, Health Checks

Step-by-Step Workflow(Hands on).

1️⃣ Launch EC2 Instances
Launched EC2 instances in public subnet (subnet-092f6bbcb6fd73e8f)
Installed Nginx Web Server
Created /usr/share/nginx/html/index.html with content:
Hello from EC2 Web Server

Verified locally:
curl http://localhost
curl http://<private-EC2-IP>

2️⃣ Create Launch Template
Standardized instance configuration for Auto Scaling
Key configurations:
AMI ID, Instance Type
Security Group: HTTP/80 + SSH/22
User Data: install Nginx (optional)

3️⃣ Setup Auto Scaling Group
Linked Launch Template → Auto Scaling Group
Configured subnets in same VPC (vpc-0cf815af83c8054be)
Scaling Policies:
Minimum instances: 1
Maximum instances: 3
Ensured auto-healing: unhealthy instance replaced automatically

4️⃣ Create Target Group
Target Type: Instance
Protocol: HTTP, Port 80
Health Check:
Protocol: HTTP
Path: /index.html
VPC: same as EC2 instances

5️⃣ Register Targets
Registered running EC2 instances in the target group
Verified health: status changed from Unused → Initial → Healthy

6️⃣ Setup Application Load Balancer (ALB)
Created ALB in same VPC
Configured public subnets for high availability
Created Listener (HTTP 80)
Forwarded traffic to Target Group (tg-web)

7️⃣ Test the Setup
Copied ALB DNS name:
http://alb-web-468469989.ap-south-1.elb.amazonaws.com

Browser displayed:
Hello from EC2 Web Server

Verified Nginx status on EC2:
sudo systemctl status nginx

8️⃣ Test Auto-Healing
Terminated an instance manually via EC2 console
Auto Scaling automatically launched a new instance
ALB continued serving traffic to healthy instance(s) → No downtime

Key Learnings
*Hands-on experience with EC2, ALB, Target Groups, Auto Scaling, Security Groups, VPC
*Implemented auto-healing & real-time incident recovery


<img width="1919" height="781" alt="image" src="https://github.com/user-attachments/assets/962c2422-0b1d-40e4-ae3a-eff87eff8b00" />
<img width="1919" height="649" alt="image" src="https://github.com/user-attachments/assets/9540a3b3-d6bd-4e87-968a-048edb8ebfde" />
<img width="1919" height="756" alt="image" src="https://github.com/user-attachments/assets/8f017359-582a-4467-a811-598ce8aed622" />
<img width="1495" height="809" alt="image" src="https://github.com/user-attachments/assets/b6521555-8239-4f2d-9df6-983292ad68a8" />
<img width="1919" height="626" alt="image" src="https://github.com/user-attachments/assets/b6a60a2b-cd70-4fd2-839b-11adf1f99944" />
<img width="1453" height="787" alt="image" src="https://github.com/user-attachments/assets/31e0aa8a-52a6-4491-9f30-2e4b84ad0fdd" />
<img width="1904" height="829" alt="image" src="https://github.com/user-attachments/assets/3e0b9bfa-041d-4669-9528-4980787d3b16" />
<img width="860" height="315" alt="image" src="https://github.com/user-attachments/assets/a8952b64-e6ff-45f6-aa89-b63d60dcb9ea" />






Validated production-ready cloud infrastructure workflow

Learned end-to-end troubleshooting for health checks, security, and networking
