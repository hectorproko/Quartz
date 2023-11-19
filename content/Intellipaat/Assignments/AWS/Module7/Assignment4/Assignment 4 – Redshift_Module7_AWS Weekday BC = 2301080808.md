---
tags:
  - AWS
---
==Pending CleanUP==
 

> [!info] Module 7: Redshift Assignment
> **Problem Statement:** 
> You work for XYZ Corporation. Their application requires a database service that can store data which can be retrieved if required. Implement suitable service for the same. 
> 
> **While migrating, you are asked to perform the following tasks:** 
> 1. Create a Redshift data warehouse. 
> 2. Using the query editor: 
>    a. Load some data 
>    b. Query the data



### **1. Setting up a Redshift Cluster:**

**Step 1:** I logged into the AWS Management Console and navigated to the Amazon Redshift service.

**Step 2:** On the Redshift dashboard, I clicked on the "Create cluster" button.

**Step 3:** I followed the setup wizard, providing the necessary details:

- **Cluster Identifier:** A unique name for my cluster `redshift-cluster-1`.
- **Database Name, User & Password:** As required for my application.
- **Node Type & Number:** Based on the size and performance needs.

**Step 4:** After configuring additional settings like VPC, IAM roles, etc., I clicked on the "Create cluster" button.

**Step 5:** I waited a few minutes for AWS to provision and set up the Redshift cluster. Once the status changed to "Available," the cluster was ready to use.
<br>![[Pasted image 20230929214439.png]]
<br>![[Pasted image 20230929214458.png]]
### **2. Using the Query Editor:**

**Step 1:** From the Redshift dashboard, I clicked on my newly created cluster's name.

**Step 2:** I clicked on the "Go to query editor" option.
<br>![[Pasted image 20230929214840.png]]
**Step 3:** Before executing any queries, I had to connect to my database. I entered the database name, database user, and the password that I specified during the cluster creation.
<br>![[Pasted image 20230929215112.png]]
<br>![[Pasted image 20230929215206.png|]]

**Step 4: Loading Data from Local Workstation:**
%% Comment

> [!info]- Issue Info
> The error message you're seeing, "A staging Amazon S3 bucket is required and is not configured. Go to account settings to configure a staging S3 bucket.", indicates that while you're attempting to load data directly from your local machine, Redshift still requires an intermediate S3 bucket to stage the data before loading it into your Redshift cluster.
> 
> This is a unique aspect of Redshift's architecture. Even when loading from a local file, the data is first uploaded to this staging S3 bucket, then Redshift loads the data from this bucket.
> 
> Remember, while you're uploading from a local source, the data first goes to this S3 bucket and then into Redshift. Ensure the appropriate permissions are set so that Redshift can access and load data from this bucket.

%%

> [!tip] Prerequisite
> **Step 1:** **Create an S3 Bucket:** I realized I needed an S3 bucket to stage my data for Redshift. So, I headed over to the S3 console and used old bucket `my-test-bucket-unique-name`. This would be used for staging my data before it's loaded into Redshift.
> 
> **Step 2:** **Configure the Staging Bucket in My Redshift Settings:**
> 
> - I went to the account settings in my Redshift console.  
>     <br>![[Pasted image 20230929220726.png]]
>     
> - From there, I searched for the section that lets me set up or configure a staging S3 bucket.
>     
> - I then entered the name of the S3 bucket I just created. <br>![[Pasted image 20230929220830.png]]
> 
> > [!fail] Otherwise we get error:
> > <br>![[Pasted image 20230929220154.png]]
> 

Within the Query Editor, I noticed an "Load data".

1. I clicked on the "Load data" button.
2. A file picker dialog appeared, allowing me to select a file from my local workstation.
3. I selected the desired CSV file from my local machine.
4. I clicked on "Next".  
<br>![[Pasted image 20230929215523.png|]]

File `data.csv` contains:
```bash
id,name,age,city
1,Alice,25,New York
2,Bob,30,London
3,Carol,35,Paris
4,Dave,40,Tokyo
5,Eve,45,Sydney
```

<br>![[Pasted image 20230929221024.png]]

**Step 5: Querying Data:**

With the data now loaded into Redshift, I executed my query:

```sql
SELECT * FROM my_table LIMIT 4;
```

<br>![[Pasted image 20230929221542.png]]
This fetches the first 4 rows from the "my_table" table.

---



  



