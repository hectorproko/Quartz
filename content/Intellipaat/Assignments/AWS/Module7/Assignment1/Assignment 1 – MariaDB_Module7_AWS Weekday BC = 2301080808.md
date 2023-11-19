==Pending CleanUP==
#AWS

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
%%  Had to create a VPC just for this as per issue below and had to put Internet Gateway in the Route table %%

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
%%
```
ubuntu@ip-10-0-2-77:~$ mysql -h database-1.cnk8gecauqro.us-east-1.rds.amazonaws.com -u admin -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 98
Server version: 5.5.5-10.6.14-MariaDB-log managed by https://aws.amazon.com/rds/

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```
%%
<br>![[Pasted image 20230928213300.png]]
After hitting enter, I was prompted to enter my password.

**Step 5:** I entered my password, and just like that, I was connected to my RDS instance from my EC2 machine.

---

After these steps, I had a MariaDB RDS instance up and running, and I could connect to it both from my Windows machine and from a Linux-based EC2 instance. Success!





%%

Reference from [[Amazon RDS (Relational Database Service)#Demo 1 – RDS ( MySQL )]]

> [!fail] ISSUE
> 
> <br>![[Pasted image 20230928143047.png]]
> 
> > [!success] Solution
> > Created a new VPC with  10.0.0.0/16
> > subnets
> > 10.0.1.0/24
> > 10.0.2.0/24
> > 10.0.3.0/24
> > 10.0.4.0/24

%%

^41cbaa

%%
```
Setting environment for using XAMPP for Windows.
Hecti@DESKTOP-7SBLCCA c:\xampp
# mysql -h database-1.cnk8gecauqro.us-east-1.rds.amazonaws.com -u admin -p
Enter password: ********
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.14-MariaDB-log managed by https://aws.amazon.com/rds/

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```
%%