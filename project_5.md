## IMPLEMENT A CLIENT SERVER ARCHITECTURE USING MYSQL DATABASE MANAGEMENT SYSTEM (DBMS).
---
1. ### **Create and configure two Linux-based virtual servers (EC2 instances in AWS).**
Server A name - `mysql server`

Server B name - `mysql client`

![EC2](./images-project5/EC2.PNG)

1. On mysql server Linux Server install `MySQL Server software`.
   
   ```
   sudo apt update
   sudo apt upgrade
   sudo apt install mysql-server
   ```
   sudo systemctl status mysql

   ![Mysql-server](./images-project5/mysql-server-status.PNG)

sudo mysql_secure_installation

sudo systemctl enable mysql

**create a new user:**

sudo mysql

mysql> `CREATE USER 'billy'@'%' IDENTIFIED WITH mysql_native_password BY 'Password1';`

![create-user](./images-project5/create-user.PNG)

**Create a Database and Grant permitions**

mysql> `CREATE DATABASE test_db;`

mysql> `GRANT ALL ON test_db.* TO 'billy'@'%' WITH GRANT OPTION;`

![create-database](./images-project5/create-database.PNG)

**To reload Grant table:**

mysql> `FLUSH PRIVILEGES;`

2. On mysql client Linux Server install `MySQL Client software`.

```
   sudo apt update
   sudo apt upgrade
   sudo apt install mysql-client
   ```
   **check the version of mysql-client**
   
   `mysql -V` 
   
   "Notice it is a captal V"

   ![Mysql-client](./images-project5/mysql-client-status.PNG)


### **3. Configure MySQL server to allow connections from remote hosts.**


`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:


![config](./images-project5/config.PNG)



![updated-config](./images-project5/update-config.PNG)

### **4. Configur the mysql-server security group**

MySQL server uses `TCP port 3306` by default`, so we will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups

- Open port 3306 and limite access only to client ip

![open-port3306](./images-project5/security-group.PNG)


### **5. Connect to mysql server from from mysql client**

Use `mysql server's local IP address to connect` from mysql client.

Syntax:

`sudo mysql -u username -h mysql_server_ip -p`


$ `mysql -u billy -h 172.31.84.84 -p`


![sclient-connection](./images-project5/sclient-connection.PNG)

 
### **6. Test:**

mysql> `Show databases;`

![tet](./images-project5/test.PNG)
