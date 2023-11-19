==Pending CleanUP==
#AWS

> [!info] Module 11: Migration Assignment - 3
> **Problem Statement:**
> You work for XYZ Corporation. Your corporation wants to move their infrastructure to the cloud to improve the performance and availability of the application hosted. You are given the opportunity to accomplish the tasks for successful migration. 
> 
> **Tasks To Be Performed:**
> 1. Launch an RDS MySQL database. Login and insert some data into it. 
> 2. Use Database Migration (DMS) System to migrate the MySQL database into an RDS PostgreSQL database.


%% Link from Intellipaat
AWS Database Migration (MySQL to PostgreSQL):
```
https://us02web.zoom.us/rec/share/iBsPg2W5MqW5mcsEOzuF4E4a1cj8EzdNklz_xZoQeIzbejXT5pf3uKAmwjhfxJUX.bt5HMVQ5vsP11Zr1
```
Passcode: 
```bash
w&Mj1tTJ
```

After Migration, Installing and Accessing Postgres database on EC2:
```
https://us02web.zoom.us/rec/share/7NK6aVsRY8hQzpSib8gOkmLeFVRpQXRcCxFS91KOI5RByAPP01v7a7JiUEpwz9J8.9PQjuzzwVkhJ4XaK
```
Passcode:
```
bs1aT2$$
```

Just Like in [[Assignment 2 – Aurora_Module7_AWS Weekday BC = 2301080808|Assignment 2 – Aurora]]
MySQL is just an instance, clouformation [[Case Study – Multi-Tier Architecture_Module8_AWS Weekday BC = 2301080808|Case Study – Multi-Tier Architecture]]
![[mysql.yaml]]
%%

### MySQL Database Setup and Data Generation

We set up an RDS instance with the MySQL Engine and an Aurora Cluster for Postgres. MySQL serves as our source database, while Postgres acts as our target.
![[Pasted image 20231018154908.png]]

I will connect to these databases using an EC2 instance by selecting the "Set up EC2 connection" option for each database.
![[Pasted image 20231017154145.png]]

#### Connecting to the MySQL Instance

The provided MySQL script will generate a database and some sample data to migrate.
```mysql
CREATE DATABASE testdb;
USE testdb;
CREATE TABLE sample (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255));
INSERT INTO sample (name) VALUES ('data1'), ('data2'), ('data3');
```

Connecting to the MySQL instance hosted on Amazon RDS.
```
mysql -h mysql.cnk8gecauqro.us-east-1.rds.amazonaws.com -P 3306 -u admin -p
```
![[Pasted image 20231018155600.png]]

### Creating a Replication Instance

To begin the data migration process using the AWS Database Migration Service (DMS), I first need to create a Replication Instance. Here's the step-by-step procedure:

1. Start by searching for "DMS" in the AWS Management Console.
2. Once inside DMS, I navigate to the `Migrate data` section.
3. Then, I choose `Replication instances`.
4. On this screen, I'll click on the button titled "Create replication instance".
%%[[createreplicationinstanceIssue.png]]%%
![[Pasted image 20231017164539.png]]

### Setting Up Source and Target Endpoints

To set up the endpoints for our migration process, here's what I do:

For the MySQL Source Endpoint: %%[[mysql_endpoint.png]]%%

1. In the AWS DMS console, I navigate to the left panel and click on `Migrate data`.
2. Next, I select `Endpoints`.
3. I then click on the "Create endpoint" button.
4. In the setup, I ensure I select MySQL as the source type and provide the necessary database details.

For the PostgreSQL Target Endpoint: %%[[postgres_endpoint.png]]%%

1. Still within the `Endpoints` section, I click on another "Create endpoint" button.
2. This time, I set it up for our PostgreSQL database, specifying it as our target.
3. I provide the required Amazon Aurora PostgreSQL details and finish the configuration.

![[Pasted image 20231018154846.png]]

### Database Migration Task
  
To initiate the actual data migration process, here's what I'm doing: %%[[Create database migration task .png]]%%

1. In the AWS DMS console, I head over to the left panel and select `Migrate data`.
2. I then choose `Database migration tasks`.
3. To kick off the migration, I click on the "Create task" button.
4. I pick the previously created replication instance
5. I ensure that the correct source (MySQL) and target (PostgreSQL) endpoints are selected.
6. With the task configured, I begin the migration. As seen in the dashboard, the task with the identifier `mysql-postgres` has successfully completed a full load, transferring 100% of the data from the MySQL source to the PostgreSQL target. This confirms our data has been moved successfully.
![[Pasted image 20231018154924.png]]

### Verifying Data Migration in PostgreSQL

To verify the data migration, I'm connecting to the PostgreSQL instance using the provided command. This will allow me to access the PostgreSQL database and inspect the tables and data to ensure everything was migrated accurately from the MySQL source.
```
psql -h postgres2-instance-1.cnk8gecauqro.us-east-1.rds.amazonaws.com -U postgres
```

> [!success]
> ![[Pasted image 20231018155052.png]]






%%
# Issues

> [!fail] Issue
> 
> ![[Pasted image 20231017160919.png]]
> `The IAM Role arn:aws:iam::838427752759:role/dms-vpc-role is not configured properly.`

> [!note] Posible solution
> 
> I can confirm that as of today `dms-vpc-role` is NOT created automatically from console. The role needs to be manually created and the `AmazonDMSVPCManagementRole` policy attached to it, as mentioned above.
> 
> `dms-vpc-role` is there with  `AmazonDMSVPCManagementRole`
> 
>
> > [!tip]
> > Clicked again and started creating it, without doing anything

> [!fail]
> ![[Pasted image 20231017165323.png]]
> ```
> SYSTEM ERROR MESSAGE:Error in mapping rules. At least one selection rule is required.
> ```
> <mark style="background: #BBFABBA6;">Just make sure have</mark>
> ![[Pasted image 20231017170357.png]]
> 





> [!NOTE]- Possible solution to using only the instance
> 
> Dear learner,
> 
> I wanted to bring to your attention some crucial information regarding the version of PostgreSQL you are using.
> Which is causing the target endpoint connection to failure.
> 
> RDS PostgreSQL Version:
> 
> It's essential to note that versions above 15 do not support AWS Database Migration Service (DMS) for migration purposes.
> 
> Therefore, if you are planning to use AWS DMS for database migration, I recommend using PostgreSQL version 14.9 or any version below 15
> to ensure compatibility with the migration process.
> 
> You can resolve this by creating a new RDS PostgreSQL database with a version below 15.
> 
> If you have any questions or need further assistance with these recommendations, please do not hesitate to reach out.


%%