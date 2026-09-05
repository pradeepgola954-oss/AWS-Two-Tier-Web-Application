# AWS-Two-Tier-Web-Application
A two-tier web application deployed on AWS using separate EC2 instances for the Apache/PHP web server and MySQL database, featuring secure connectivity and a PHP-based guestbook application.
# Project Objectives

<img width="1536" height="1024" alt="ChatGPT Image Aug 30, 2026, 12_50_18 PM" src="https://github.com/user-attachments/assets/56076e7e-39e2-46c4-b8ff-b8d5e58aa80e" />

.To deploy a two-tier web application using two separate AWS EC2 instances.

.To configure one EC2 instance as an Apache/PHP Web Server.

.To configure another EC2 instance as a MySQL Database Server.

.To establish secure communication between the Web Server and Database Server.

.To develop a PHP-based Guestbook application that allows users to submit messages.

.To store and retrieve user records from the remote MySQL database.

.To configure AWS Security Groups to control HTTP and MySQL access.

.To understand the benefits of separating the web server and database server in a real-world cloud environment.

.To gain practical experience in AWS EC2, Apache, PHP, MySQL, networking, and database connectivity.

# Step 1: Create the Database Server EC2 Instance

<img width="1920" height="1080" alt="Database-Server-1" src="https://github.com/user-attachments/assets/5773cf45-f5b7-4af8-89a2-323110db2d35" />

<img width="1920" height="1080" alt="Database-Server-2" src="https://github.com/user-attachments/assets/cf2139da-02c6-4d9e-868d-b9dfe60762e4" />

► First, I went to the EC2 Dashboard in the AWS Management Console and clicked on ‘Launch Instance’.

► Then, I gave the instance a name, ‘Database-Server’, so that I could easily identify it.

► I selected Amazon Linux 2023 AMI as the operating system.

► For the instance type, I selected t3.micro, which is suitable for this project and helps reduce costs.

► I selected the ‘Key-Pair-Project’ key pair for secure SSH access.

► Finally, I selected my project VPC, configured the required subnet, selected ‘Database-Server-SG’, and clicked ‘Launch instance’.

# Step 2: Connecting to the Server
<img width="1920" height="1120" alt="CMD-1" src="https://github.com/user-attachments/assets/ff30c5c3-da67-476e-8f8f-02efdc1d92a9" />

**SSH Command:**

► Once the server was ready, I opened my terminal and connected to it using the SSH command.

```bash
ssh -i "Linux-key-pair.pem" ec2-user@<PUBLIC-IP>
```
```bash
sudo -i
```

# Step 3: Downloading MySQL Repository
<img width="1920" height="1080" alt="CMD-2" src="https://github.com/user-attachments/assets/1f6b1bd4-4ab5-464d-84d5-7b75a6fdef52" />

**SSH Command:**

► After logging in, I switched to the root user to get full administrative rights.

```bash
sudo -i
```

















