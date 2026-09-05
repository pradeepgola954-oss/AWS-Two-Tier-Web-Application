 # Step 11: Creating a New User and Granting Permissions
<img width="1920" height="1080" alt="CMD-5" src="https://github.com/user-attachments/assets/ce8f3ad5-2bd0-4d2c-a909-aa758c2467da" />

► I created a MySQL user named Prince that can connect from any host (%) and set a secure password for it.

**SSH Command:**

```bash
CREATE USER 'Prince'@'%' IDENTIFIED BY 'Pradeep@123';
```
