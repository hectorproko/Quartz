==Pending CleanUP==
#AWS

> [!info] Module 6: Case Study - 1 
> **Problem Statement:** 
> You work for XYZ Corporation. Their application requires a storage service that can store files and publicly share them if required. Implement S3 for the same. 
> 
> **While migrating, you are asked to perform the following tasks:** 
> 1. Ensure that any amount of data can be stored on the cloud and can be retrieved at any time from anywhere on the web. 
> 2. Manage the lifecycle of data that is being stored on the cloud so that it gets automatically deleted after 75 days. 
> 3. Retrieve the old version of a file if the content of the current version of that file is compromised accidently. 
> 4. Host your static website on the AWS cloud using the domain name created in Module 3 assignment. 
> 5. Display an error page if proper domain name is not used while attempting to access the company’s website. 

### **1. Storing and Retrieving Data:**

**Steps I Followed to Create the S3 Bucket:**

1. **Accessing S3**:
- I logged into the AWS Management Console.
- I navigated to the "S3" service under the storage section.
  
2. **Starting the Bucket Creation Process**:
- I clicked on the "Create bucket" button.
  
3. **Configuring General Settings**:
- **Bucket Name**: I designated it as `temp.hectorproko.com`.

> [!tip]
>   When using S3 for static website hosting and Route 53, the bucket name should match the domain/subdomain name you're trying to associate with it.

%%[[Case Study – S3 Versioning And Website Hosting_Module6_AWS Weekday BC = 2301080808#^921623|You had issues with this]]%%

- **AWS Region**: Retained the default, which was "US East (N. Virginia) us-east-1".
  
4. **Object Ownership Configuration**:
- I selected the "ACLs enabled" option. By enabling ACLs, I granted the flexibility to specify access permissions for the bucket, allowing for actions like "Make public using ACL" at the object level later on.
  
5. **Public Access Configuration**:
- I deselected the "Block all public access" choice.
- I acknowledged the associated warnings by marking the checkbox that reads, "I acknowledge that the current settings might result in this bucket and the objects within becoming public."
  
6. **Activating Bucket Versioning**:
- I turned on "Bucket Versioning". This permits the maintenance of multiple variants of an object within the same bucket.

After ensuring all the settings met my requirements, I finalized by clicking on the "Create bucket" button.

%% Full picture, name of bucket had to change
[[FireShot Capture 015 - S3 bucket - s3.console.aws.amazon.com (1).png]]
%%

---

### **2. Managing Lifecycle of Data:**

**Setting Up Auto-Deletion in S3 Bucket:**

**Step 1:** Logged in to AWS, navigate to S3, and selected the desired bucket.

**Step 2:** Clicked the "Management" tab, then "Create lifecycle rule".

**Step 3:** Name the rule "AutoDeleteAfter75Days".

**Step 4:** Choose "Expire current versions of objects" and set to 75 days.
<br>![[Pasted image 20231005212125.png]]
**Step 5:** Save the rule.

---

### **3. Versioning for File Retrieval:**

When I created the bucket, I enabled "Versioning" 

<br>![[Pasted image 20231005212945.png]]

**Demonstrating Versioning in Amazon S3:**

1. Initial Upload:
I created a `.txt` file named `Hello World.txt` with the content "Hello World" and uploaded it to the S3 bucket.

2. Modify and Re-upload:
I then edited the content of the same `.txt` file to "Hello World 2" and uploaded it again.

3. Viewing Versions:
Inside the S3 bucket, I toggled the "Show versions" option. This revealed both the initial and modified versions of the file, each with its unique version ID.

4. Retrieving Content:
By selecting and opening each version, I confirmed that the content corresponds to its respective upload: the older version displays "Hello World" and the newer version displays "Hello World 2".
<br>![[Pasted image 20231005213953.png]]


---

### **4. Hosting Static Website with Custom Domain:**

**Step 1:** Navigated to the "Properties" tab in your S3 bucket.

**Step 2:** Clicked "Edit" next to  "Static website hosting" .

**Step 3:** Set 'index.html' as the Index document and 'error.html' as the Error document.
<br>![[Pasted image 20230927223731.png]] ^d9a6c3

**Step 5:** Uploaded `index.htm` and `error.html` with the following content:
`index.html`
```html
<h1>Index Page</h1>
```
`error.html`
```html
<h1>Error Page</h1>
```

**Step 5:** Made the static site available to the public, I clicked on 'Actions' and then select 'Make public using ACL'.

<br>![[Pasted image 20231005220106.png]]

**Step 6: Configuring Route 53 to Point to the S3 Static Website**

1. I returned to the **AWS Route 53** service, recalling the setup from [[Assignment 3 – Route 53_Module4_AWS Weekday BC = 2301080808|Assignment 3 – Route 53]].
2. Within Route 53, I navigated to the hosted zone for "temp.hectorproko.com".
3. Here, I initiated the process to define a simple record that would route traffic to the S3 bucket.
4. I left the subdomain field empty to target the root domain.
5. I set the record type as "A" and enabled the alias option.
6. For the "Route traffic to" section, I chose the S3 website endpoint associated with my static site's bucket.
7. After ensuring all details were accurate, I saved my configuration.

With this configuration in place, any visits to "temp.hectorproko.com" will be routed to the static site I've set up in my S3 bucket.

<br>![[Pasted image 20231005223916.png]]

<br>![[Pasted image 20231005224147.png]]
%%
> [!fail]- Issue pointing to bucket
> When i tried to point to the S3 bucket got this error
> <br>![[Pasted image 20231005222809.png]]
> 
> Seems like I need to reanme the bucke to 
> **Bucket Name and Domain Name Matching**: When using S3 for static website hosting and Route 53, the bucket name should match the domain/subdomain name you're trying to associate with it. If your bucket's name is `bucketforcasestudy`, but you're trying to point it to a domain/subdomain like `example.com`, Route 53 won't recognize the S3 website endpoint because of this mismatch.
> 
> For the domain `temp.hectorproko.com`, you should name the S3 bucket exactly as:
> 
> `temp.hectorproko.com`
> 
> This ensures that the S3 bucket's website endpoint can be correctly mapped to that domain using Route 53.

%%

^921623


**Step 7: Site Testing:**

1. I accessed `temp.hectorproko.com` and was correctly presented with the **Index Page**.

> [!success]
>    <br>![[Pasted image 20231005225206.png]]

 
2. To simulate an error, I navigated to `temp.hectorproko.com/test` and was appropriately directed to the **Error Page**.

> [!success]
>    <br>![[Pasted image 20231005225134.png]]









%%
> [!fail]- S3 Static Website Hosting: Case Sensitivity Issue
> **Issue:** When accessing the static website via the S3 endpoint, the error page was displayed by default.
> 
> **Root Cause:** The specified default index document in the S3 bucket's static website hosting configuration was "index.html". However, the actual file uploaded to the bucket was named "Inde.html". S3 treats filenames as case-sensitive, thus it couldn't locate the correct index file.
>  [[Case Study – S3 Versioning And Website Hosting_Module6_AWS Weekday BC = 2301080808#^d9a6c3|Mistake made here]]
> 
> **Solution:** Ensure that the file names, especially those specified in configurations, match the actual uploaded file names exactly, taking into account case sensitivity.
> 
> **Note:** Always be mindful of file naming conventions and case sensitivity when working with AWS S3 and similar services.

%%

---

Once you've completed these steps, XYZ Corporation's requirements will be fully implemented. The data will be stored securely on AWS, with a lifecycle rule ensuring automatic deletion after 75 days. Additionally, the website will be hosted on AWS, with proper error handling in place.



