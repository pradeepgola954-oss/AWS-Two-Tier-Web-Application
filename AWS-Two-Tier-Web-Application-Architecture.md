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

