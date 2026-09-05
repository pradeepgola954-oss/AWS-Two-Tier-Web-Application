 # Step 11: Creating a New User and Granting Permissions
<img width="1920" height="1080" alt="CMD-5" src="https://github.com/user-attachments/assets/ce8f3ad5-2bd0-4d2c-a909-aa758c2467da" />

► I created a MySQL user named Prince that can connect from any host (%) and set a secure password for it.

**SSH Command:**

```bash
CREATE USER 'Prince'@'%' IDENTIFIED BY 'Pradeep@123';
```
► I gave the new user full access to myDatabase and refreshed the permissions.

```bash
GRANT ALL PRIVILEGES ON myDatabase.* TO 'Prince'@'%';
FLUSH PRIVILEGES;
```
# Step 12: Verifying Permissions and Table Status

► I checked the new user's permissions to make sure everything was set up correctly.

```bash
SHOW GRANTS FOR 'Prince'@'%';
```
► Finally, I ran a test query to make sure the guestbook table was ready to store data.

```bash
SELECT * FROM guestbook;
```
 # Deployment Guide: AWS Two-Tier Web Application
 
 **Phase 1: Launching the Frontend Web Server**
 
<img width="1920" height="1080" alt="Web-Server-1" src="https://github.com/user-attachments/assets/540af658-bdcd-4c39-8c00-23a75c857064" />

<img width="1920" height="1080" alt="Web-Server-2" src="https://github.com/user-attachments/assets/3d278a73-a108-42c7-bbd6-b8c4ac48e9d3" />

► I opened the **EC2 Dashboard** in the AWS Management Console and clicked **“Launch Instance.”**

► I named the instance **“Web-Server”** so it could be easily identified as the frontend server.

► I selected **Amazon Linux 2023 AMI** as the operating system for the server.

► I chose **t3.micro** as the instance type to keep the project cost-effective.

► For secure SSH access, I selected the existing **“Linux-Key-pair.”**

► In the network settings, I selected the **default VPC** and attached the existing **“Web-Server-SG”** security group.

► After reviewing all the settings, I clicked **“Launch Instance”** to create and start the web server.

 ## Step 13: Connecting to the Web Server via SSH ##

 <img width="1920" height="1080" alt="Web-Server-CMD-6" src="https://github.com/user-attachments/assets/6db65077-1c64-42d8-ac09-2c0698fd5878" />
 

 ► First, I opened the local terminal, navigated to the folder containing my private key, and connected to the **Web Server** using its public IP address.

 ```bash
cd Downloads
ssh -i "Key-Pair-Project.pem" ec2-user@13.200.237.180
```
► After successfully logging in, I switched to the **root user** to gain the necessary administrative privileges for the installation.

```bash
sudo -i
```
## Step 14: Installing PHP 8.1 and Apache Web Server ##

► I used the package manager to install PHP 8.1 along with the Apache (httpd) web server.

 ```bash
dnf install php8.1 -y
```
► To verify that PHP was installed correctly, I checked the installed PHP version in the terminal.

```bash
php -v
```
## ► The output successfully showed PHP 8.1.34 was active on the server. ##

## Step 15: Installing MySQL Database Extension for PHP ##

<img width="1920" height="1080" alt="Wev-Server-CMD-7" src="https://github.com/user-attachments/assets/9a4660a4-2aa7-4abc-b915-c925f012aed2" />

► To connect the frontend application to the backend database, I installed the PHP-MySQL extension.

```bash
dnf install php8.1-mysqlnd.x86_64 -y
```
## Step 5: Managing Application Services ##

► Next, I started the PHP-FPM service and checked its status to confirm that it was running properly.

```bash
systemctl start php-fpm
systemctl status php-fpm
```
► The terminal output confirmed that the service was active (running).

► I then started the Apache (httpd) web server and enabled it to start automatically when the system boots.

```bash
systemctl start httpd
systemctl enable httpd
```




 


