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
## Step 16: Managing Application Services ##

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
## Step 17: Preparing the Database Test File ##

<img width="1920" height="1080" alt="Web-Server-CMD-8" src="https://github.com/user-attachments/assets/e64b908e-bbb7-4df1-b6d8-8d79fe717aa9" />

► Finally, I navigated to the web server’s root directory and used the vi text editor to create a file named dbtest.php for testing the database connection.

```bash
cd /var/html/
vi dbtest.php
```
## Step 18: Configuring Database Connection (dbtest.php) ##

<img width="1920" height="1080" alt="Web-Server-CMD-9" src="https://github.com/user-attachments/assets/91b65c71-b811-4c47-bf18-b6657e9f1c7c" />

► Inside the /var/www/html/ directory, I created a dbtest.php file containing the required configuration to connect the frontend application to the MySQL database using PDO.

```bash
<?php
$servername = "172.31.12.178";
$username = "love";
$password = "Pradeep@123";
$database = "myDatabase";

$pdo = new PDO("mysql:host=$servername;dbname=$database", $username, $password);
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
?>
```

## Step 19: Creating the Frontend Guestbook Interface (index.php) ##

<img width="1920" height="1080" alt="Web-Server-CMD 10 -1" src="https://github.com/user-attachments/assets/6c511fae-79f6-4fed-87c0-eeb5db079c4c" />


► Next, I used the vi index.php command to create the main webpage file. This file uses the PDO database connection from dbtest.php and performs two main functions:

1. Saving Data: It accepts the user's Name and Message from the web form and securely inserts the data into the guestbook table in the MySQL database.
   
2. Displaying Data: It retrieves the saved records from the guestbook table and dynamically displays them on the webpage.

```bash
<?php
include 'dbtest.php';
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = $_POST['name'];
    $message = $_POST['message'];

    $stmt = $pdo->prepare("INSERT INTO guestbook (name, message) VALUES (?, ?)");
    $stmt->execute([$name, $message]);
}
?>

<!DOCTYPE TYPE html>
<html>
<head>
    <title>Guestbook</title>
</head>
<body>
    <h2>Guestbook</h2>
    <form method="post" action="<?php echo $_SERVER['PHP_SELF']; ?>">
        Name: <input type="text" name="name"><br><br>
        Message: <textarea name="message" rows="5" cols="40"></textarea><br><br>
        <input type="submit" name="submit" value="Submit">
    </form>

    <h2>Messages</h2>
    <?php
    $stmt = $pdo->query("SELECT name, message FROM guestbook");
    while ($row = $stmt->fetch()) {
        echo "<b>" . $row['name'] . "</b><br>";
        echo $row['message'] . "<br><br>";
    }
    ?>
</body>
</html>
```

## Step 20 : Configuring Network Security Groups ##

**1. Configuring the Web Server Security Group (Web-Server-SG)**

<img width="1920" height="1080" alt="1 SG" src="https://github.com/user-attachments/assets/833f8297-562a-42c1-9449-2f78d9af1471" />

<img width="1920" height="1080" alt="2 SG" src="https://github.com/user-attachments/assets/23434756-5340-48c4-83f2-bf3dc189b44f" />

► First, I navigated to the EC2 Dashboard, selected Security Groups, and clicked Create security group.

► I created a security group named Web-Server-SG with the description Secure-Web-Server-SG and associated it with my project VPC.

► Under Inbound rules, I configured the following rules to secure the web server:

HTTP (Port 80): The source was set to Anywhere-IPv4 (0.0.0.0/0), allowing users from the internet to access the website.
SSH (Port 22): The source was restricted to My IP, ensuring that SSH access is limited to my local computer.

► Under Outbound rules, I allowed all outbound traffic so that the web server could communicate with the required external and backend services.

► Finally, I reviewed the configuration and clicked Create security group.

**2. Configuring the Database Server Security Group (Database-Server-SG)**

<img width="1920" height="1080" alt="Screenshot (113)" src="https://github.com/user-attachments/assets/84753289-6989-48b3-b82a-aaa3e1aec481" />

<img width="1920" height="1080" alt="Screenshot (114)" src="https://github.com/user-attachments/assets/0b2e5c48-54fb-468c-a579-f80e0297ac16" />

►  I created a separate backend security group named Database-Server-SG with the description Secure-Database-Server-SG and associated it with the same VPC.

► For the Inbound rules, I implemented strict tier-to-tier access control:

MySQL/Aurora (Port 3306): The source was configured as Custom, and I selected the Web-Server-SG security group ID (sg-065765a4f4700a23). This allows MySQL traffic only from resources associated with the web server security group instead of exposing the database port directly to the internet.
SSH (Port 22): The source was restricted to My IP, allowing only my local computer to connect to the database server for administrative management.

► Finally, I reviewed the configuration and clicked Create security group, establishing a secure network-security foundation for the project.













 


