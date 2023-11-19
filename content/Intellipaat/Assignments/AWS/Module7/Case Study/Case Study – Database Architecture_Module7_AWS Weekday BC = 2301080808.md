---
tags:
  - AWS
---
==PENDING CLEANUP==
 

> [!info] Module 7: Case Study - 1
> **Problem Statement:** 
> You work for XYZ Corporation. Your company has multiple branch offices all over the country. They want to deploy their application on AWS that reads data from the users’ devices and sends reports to all the branches. The application also requires executing complex relational joins and updates. They want high availability for their application. 
> 
> **Tasks To Be Performed:** 
> 1. Build a highly scalable database and make sure that it's always available and accessible. Manage automated backup for this database with retention period of 2 days. 
> 2. Build a database architecture which lets your application read data from different regions. 
> 3. Establish a database architecture to process the data collected for near real-time analysis. 
> 
> As the user base of the application increases, your corporation observed a significant latency in the transfer of data to the branches. Your company realized that most of the time, the same kind of data is being fetched and sent to the branches. 
> 
> **You are asked to:** 
> 1. Find and implement the solution in order to resolve the latency issues.

%%
Used
**[Database Case Study zoom recording](https://us02web.zoom.us/rec/share/8CnudwHGDodePh3F6VtG111H8tP1CGytoAJLUnYMFfVYP79rWd6KZR11FIN-KftA.e6oOFxcRvCRRzWzq?startTime=1682039418000)**
Passcode: P1Ax6#UI
%%

---
## Step 1: Created Aurora DB

1. **Access AWS Management Console**:

- I logged into my AWS account.
- Once in, I headed over to the AWS RDS (Relational Database Service) section.

2. **Create Aurora Database**:

- To create an Aurora database, I clicked the "Create database" button.
- I chose the "Standard create" option for more control.

3. **Engine Choice**:

- I selected "Aurora with MySQL compatibility" as the database engine.

4. **Choose Template**:

- I opted for the "Production" template for a robust setup.

5. **Configuration Settings**:

- For the **DB cluster identifier**, I provided the name "database-1."
- I specified the **Master username and password** for database access.

6. **Ensure Availability and Durability**:

- To ensure high availability, I chose "Create an Aurora Replica in a different Availability Zone" for "Multi-AZ deployment."

7. **Set Up Connectivity**:

- I selected the appropriate **Virtual Private Cloud (VPC)** for the database.
- I chose a suitable **Subnet group**, or created a new one if necessary.
- To enhance security, I set "Publicly accessible" to “No” to prevent external internet access.

8. **VPC Security Groups**:
   
- To allow incoming traffic within the VPC, I opened port 3306 (MySQL's default port) and specified the VPC CIDR range in the security group rules, restricting access to resources within the VPC.
          
9. **Additional configuration**:
    
    - For a robust backup strategy, I set the "Backup retention period" to 2 days, which retains automated backups for two days.
      
      <br>![[Pasted image 20231003103152.png]]


<br>![[Pasted image 20231003104510.png]]
<br>![[Pasted image 20231007125643.png]]

10. **Validating RDS Connectivity via EC2 Instance**:

- I created an Ubuntu EC2 instance in the same VPC and enabled SSH access. After setting up the instance, I installed SQL on Ubuntu using the commands `sudo apt-get update -y` and `sudo apt-get install mysql-server -y`. To connect to the database, I used the RDS endpoint writer from this EC2 instance. It's important to note that writers have full database access and can modify content, while readers can only view data. ^787ee9

> [!success] Was able to connect to writer
> ```bash
> ubuntu@ip-172-31-2-77:~$ sudo mysql -h database-1.cluster-c5aoaorpxy3j.us-east-2.rds.amazonaws.com -u admin -p
> Enter password: 
> Welcome to the MySQL monitor.  Commands end with ; or \g.
> Your MySQL connection id is 276
> Server version: 8.0.28 Source distribution
> 
> Copyright (c) 2000, 2023, Oracle and/or its affiliates.
> 
> Oracle is a registered trademark of Oracle Corporation and/or its
> affiliates. Other names may be trademarks of their respective
> owners.
> 
> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
> 
> mysql>
> ```


%%
> [!help]- Old Steps which are now just Creatint redshift
> ### 3. Near Real-Time Analysis:
> 
> **Amazon Kinesis**: This service is ideal for real-time data processing.
> 
> **Setup**:
> 
> - Stream the data from Aurora to Amazon Kinesis using triggers or custom logic.
> - Process the streamed data in near real-time using Kinesis Data Analytics.
> - Store the analyzed results back in Aurora or in a data warehouse like Amazon Redshift for further BI operations.
> ---
> 1. **Set Up Amazon Kinesis**:
>     
>     - I'll navigate to the Amazon Kinesis service.
>     - I'll click on "Create Data Stream" 
>     - I'll provide a descriptive name for the stream "MyDataStream"
>     - With the name set and default configurations in place, I'll simply click on the "Create data stream" button.
>       <br>![[Pasted image 20231003122541.png]]
> 1. **Integrate Aurora with Kinesis**:
>     
>     - I'll go back to the RDS dashboard and select my Aurora cluster, "database-1".
>     - In the "Actions" dropdown, I'll find an option to integrate or stream data to Kinesis and select it.
>     - I'll link the Aurora cluster with the Kinesis data stream I just created.
>       <br>![[Pasted image 20231003124233.png]]
>       <br>![[Pasted image 20231003124610.png]]
>       create a new AWS KMS key name RDS_key
>       
>       1. **AWS KMS key**: Choose an existing AWS KMS (Key Management Service) key for encrypting the data stream. If you don't have one, you can easily create a new one by clicking on "Create an AWS KMS key". This key ensures that your database activity data is encrypted for security purposes.
>     
> 2. **Database activity stream mode**:
>     
>     - **Asynchronous**: This mode captures and delivers the activity stream records asynchronously. This generally has minimal impact on database performance.
>     - **Synchronous**: In this mode, each database activity waits for the corresponding activity stream record to be written to the Kinesis stream. It provides the highest guarantee that activity stream records are written, but it can have a performance impact.
>     
>     For most use-cases, especially if you're just getting started or are concerned about performance, I'd recommend going with "Asynchronous".
>     
> 3. **Scheduling**:
>     
>     - **During the next maintenance window**: This option will start the activity stream during your next scheduled maintenance window.
>     - **Immediately**: This starts capturing database activity as soon as you confirm.
>     
>     If you're ready to start monitoring immediately and understand the implications (like possible short disruptions or performance implications), choose "Immediately".
>     
> 4. Finally, after configuring your desired settings, click on the "Start database activity stream" button to initiate the stream.
> 
> Once started, all database activities will be streamed to the Kinesis data stream, allowing you to monitor and analyze the activities in near real-time.
> <br>![[Pasted image 20231003124838.png]]
> 
> 
> 3. **Set Up Amazon Redshift for Analysis**:
>     
>     - I'll navigate to the Amazon Redshift service from the AWS console.
>     - I'll click on "Create cluster" and configure it according to my data size and query requirements, giving it an appropriate name `redshift-cluster-1` and specifying other parameters.
>     - Once set up, I'll ensure it has the necessary permissions to read from the Kinesis data stream.
> 4. **Stream Data from [[Amazon Kinesis#From Case Study – Database Architecture_Module7_AWS Weekday BC = 2301080808 Case Study – Database Architecture_Module7|Kinesis]] to Redshift**:
>     
>     - I'll go to the Kinesis dashboard and select my data stream.
>     - I'll set up a delivery stream to push data from Kinesis to my Redshift cluster.
>     - I'll configure any necessary transformations on the data before it gets loaded to Redshift.
> 5. **Run Near Real-Time Queries**:
>     
>     - With data now streaming into Redshift, I'll use the Redshift Query Editor (or a SQL client of my choice) to run analysis queries on the data.
>     - Since the data is updated in near real-time from Aurora through Kinesis, my analysis will reflect the latest state of the data.
> 6. **Monitor and Optimize**:
>     
>     - I'll keep an eye on the Kinesis dashboard to ensure data is flowing smoothly and monitor the Redshift console for query performance.
>     - If I notice any bottlenecks or performance issues, I'll make necessary adjustments, such as increasing shard count in Kinesis or optimizing my Redshift cluster.
> ### 4. Resolve Latency Issues:
> 
> **Amazon ElastiCache**: For data that is frequently accessed, you can use ElastiCache which is a web service that makes it easy to deploy and run an in-memory cache in the cloud.
> 
> **Benefits**:
> 
> - Improves the performance of web applications by retrieving information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.
> - Supports both Redis and Memcached.
> 
> **Setup**:
> 
> 1. Identify the frequently accessed queries/data.
> 2. Cache the results of these queries in ElastiCache.
> 3. Modify the application logic to first check the cache before hitting the database.
> 
> ### 5. Data Transfer to Branches:
> 
> **Amazon CloudFront**: It's a content delivery network (CDN) service that can be used to deliver your application data to the branches efficiently.
> 
> **Benefits**:
> 
> - Distributes content globally with low latency.
> - Integrated with other Amazon Web Services.
> 
> **Setup**:
> 
> 1. Set up CloudFront to cache the application data.
> 2. Branches will access the data via CloudFront, which fetches the data from your centralized location and caches it at an edge location closer to the branch.
> 3. On subsequent requests, CloudFront serves the cached data from the edge location, thus reducing latency.
> 
> ### In Summary:
> 
> - Use **Amazon Aurora** for a highly scalable and available database.
> - Expand read capabilities with **Aurora Global Database**.
> - Implement near real-time analysis with **Amazon Kinesis**.
> - Use **Amazon ElastiCache** to cache frequently accessed data and reduce database load.
> - Distribute data efficiently to branches with **Amazon CloudFront**.
> 
> Always remember to monitor and adjust based on the specific needs and usage patterns of the corporation. AWS provides numerous tools and services like Amazon CloudWatch to help with monitoring and fine-tuning your architecture.

%%
%%
> [!NOTE]- Notes: From Recording
> 1. Multi AZ=hihg availability, so needs to be production
> 2. create read replica of the database in another region, cuse we need readign only not writing
> 3. key word "database architecture"
>    For 3 DynamoDB, ==Redshift== and athena
> 
> elasticcache for same queries, we used Redshiftt comes with elasticacche pre-assiingt to it
> 
> **Step 1**
> - we will use auroa cuse at any point we can change from mysql to prostress
> - we cant use Dev/test cuse we need high availability
> - So doesnt charge you if less than 4 hours
>   <br>![[Pasted image 20231006201838.png]]
> 
> - will not make public,
> - security goroup incoming port 3306 0.00.0.0 or VPC CIDR
> - *make sure deletion  protection is not on so you can get rid of it.*

%%



## Step 2: Setting Up Cross-Region Data Access

%% #question Explore more how Redshift and RDS work together%%

1. **Go to my RDS Dashboard**:
    - I'll open up my AWS RDS dashboard.
2. **Choose My Aurora Cluster**:
    - I'll locate and select the Aurora cluster named "database-1", identified as a "Regional cluster".
3. **Access the 'Actions' Menu**:
    - With "database-1" selected, I'll click on the "Actions" dropdown menu at the top.
4. **Initiate Creation of Cross-Region Read Replica**:
    - I'll select the option "Create cross-Region read replica". !<br>![[Pasted image 20231007131931.png]]
5. **Configure the Read Replica**:
    - I'll provide the "DB instance identifier" as `myinstancerds`.
      %% at some point was RDSReplica, images from different trys %%
    - I'll select the destination region, choosing `US West (Oregon)` as it's closer to the other branch offices I intend to serve.
6. **Complete the Replica Setup**:
    - I'll proceed through any remaining AWS prompts to complete the setup of this cross-region read replica.

%%
After clicking "Create cross-region read replica"
I might have changed the "name identifier"
[[FireShot Capture 016 - RDS - us-east-2 - us-east-2.console.aws.amazon.com.png]]
%%

> [!fail] I stumbled upon error:
> **Your request to create DB cluster RDSreplica and instance RDSreplica has failed**.
> 
> Source cluster arn:aws:rds:us-east-2:838427752759:cluster:database-1 doesn't have binlogs enabled.

%%
[[modify database full page.png]]
%%

> [!todo] Fix: Modifying the DB cluster parameter
> 1. **Identifying the Current DB Cluster Parameter**:
>     - The database is currently using the `default.aurora-mysql8.0` DB cluster parameter group.
>       <br>![[Pasted image 20231007133239.png]]
>       
> 2. **Creating New Parameter Groups**:
>     - Default parameter groups cannot be modified, so I need to create custom ones.
>     - I've created two new parameter groups:
>         - `myclusterparametergroup` for the cluster parameter group.
>           <br>![[Pasted image 20231007135813.png]]
> 3. **Modifying Cluster Parameter Group**:
>     - I selected `myclusterparametergroup` and clicked "edit".
>     - Located `binlog_format` and set its value to `MIXED`.
>       <br>![[Pasted image 20231007140003.png]]
> 4. **Applying the New Cluster Parameter Group to the Database**:    
>     - For the `database-1` cluster, I changed its parameter group to the newly created `myclusterparametergroup`.
>       <br>![[Pasted image 20231007140614.png]]
>       <br>![[Pasted image 20231007142026.png]]
>     - The modifications are applied after the database is rebooted.
> 

> [!success] Replication now functioning. 
> <br>![[Pasted image 20231007141952.png]]  

In the Oregon region, which we selected, we observe the replica:  
<br>![[Pasted image 20231007142741.png]]



## Step 3: Setting Up Amazon Redshift for Data Analysis:
%% We could reuse data from [[Assignment 4 – Redshift_Module7_AWS Weekday BC = 2301080808#**1. Setting up a Redshift Cluster **|Assignment 4 – Redshift]]%%
**Initiate the Redshift Setup**:
1. I navigate to the **Amazon Redshift** service on my AWS console.
2. I click on "Create cluster".
3. I configure it according to my data size and query needs.
4. I name my cluster `redshift-cluster-1` and adjust other parameters as necessary.
5. I ensure "Sample data" is checked during the setup.

<br>![[Pasted image 20231007122509.png]]

I open the **Redshift query editor v2**.
<br>![[Pasted image 20231007124500.png]]

 - I navigate to the `category` table, found under `dev` > `public`.
 - I execute my sample query: `SELECT * FROM "dev"."public"."category"`.

<br>![[Pasted image 20231007125130.png]]

**Evaluating Query Performance**:
I monitor the query's performance, noting the elapsed time for each run.

> [!success]
> I observe the reduction in query execution time over multiple runs, which indicates effective caching by Redshift.
> <br>![[elapse1.png]]
> <br>![[elapse2.png]]
> <br>![[elapse3.png]]
> 



