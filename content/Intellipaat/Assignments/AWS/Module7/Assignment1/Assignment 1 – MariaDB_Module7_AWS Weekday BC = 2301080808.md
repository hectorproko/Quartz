---
tags:
  - AWS
---
==PENDING CLEANUP==
 

> [!info] Module 7: MariaDB Assignment
> **Problem Statement:** 
> You work for XYZ Corporation. Their application requires a SQL service that can store data which can be retrieved if required. Implement a suitable RDS engine for the same. 
> 
> **While migrating, you are asked to perform the following tasks:** 
> 1. Create a MariaDB Engine based RDS Database. 
> 2. Connect to the DB using the following ways: 
>    a. SQL Client for Windows 
>    b. Linux based EC2 Instance


### **1. Setting Up the MariaDB RDS Database:**

**Step 1:** I logged into my AWS Management Console and headed straight to the RDS service.

**Step 2:** I spotted the "Create database" button and clicked on it.

**Step 3:** I chose the "Standard Create" method. In the engine options, MariaDB was my choice.

**Step 2:** In "Templates" I chose "Free tier"

**Step 4:** Under the DB instance settings, I specified:

- The DB instance size that felt right for our needs.
- Left default instance identifier `database-1` and set up my master username and password.

**Step 5:** In the advanced settings, I configured:

- The VPC, ensured the subnet was correctly set, and decided to allow public access (so I could connect from my external SQL client).
- Picked an appropriate security group *(opening port 3306)* and gave the database a name.

**Step 6:** Feeling confident with my settings, I clicked "Create database". I waited a bit as AWS set things up for me.
<br>![[Pasted image 20230928155537.png]]

<br>![[Pasted image 20230928205153.png]]

---

### **2. Making the Connection to the MariaDB Database:**

#### **a. Through a SQL Client on my Windows Machine (using MySQL Workbench):**

**Step 1:** I had XAMPP Installed
<br>![[XAMPP.png]]

**Step 2:** I started MySQL and launched Shell

**Step 3:** For the hostname, I entered the endpoint of the MariaDB RDS instance (found in the RDS dashboard). I also added my username and password.
<br>![[Pasted image 20230928204804.png]]
**Step 4:** Once everything looked good, I tested the connection. I was connected to my MariaDB RDS instance.

#### **b. From a Linux-based EC2 Instance:**

**Step 1:** I hopped over to the EC2 dashboard and launched a new Linux instance (or used an existing one).

**Step 2:** Once the EC2 instance was up and running, I SSH'd into it.

**Step 3:** I installed the MySQL client on the EC2 instance with:

**Step 4:** Using the MariaDB client, I connected to my RDS instance with:
```bash
mysql -h [RDS_ENDPOINT] -u [USERNAME] -p
```

<br>![[Pasted image 20230928213300.png]]
After hitting enter, I was prompted to enter my password.

**Step 5:** I entered my password, and just like that, I was connected to my RDS instance from my EC2 machine.

---

After these steps, I had a MariaDB RDS instance up and running, and I could connect to it both from my Windows machine and from a Linux-based EC2 instance. Success!

