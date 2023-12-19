---
tags:
  - AWS
---
==PENDING CLEANUP==
 
> [!info] Module 5: VPC Endpoints Assignment
> **Problem Statement:** 
> Working for an organization, you are required to provide them a safe and secure environment for the deployment of their resources. They might require different types of connectivity. Implement the following to fulfill the requirements of the company.
> 
> **Tasks To Be Performed:** 
> 1. Create a VPC endpoint for a S3 bucket of your choice for secure access to the files.


1. **I'll Start by Accessing the Amazon VPC Dashboard**:
    - I'll sign in to the AWS Management Console.
    - From there, I'll head over to "Services" and select "VPC".
2. **I'll Proceed to Create the VPC Endpoint**:
    - Once in the VPC Dashboard, I'll find "Endpoints" on the left sidebar.
    - I'll then click on the “Create Endpoint” button.
3. **Next, I'll Configure the Endpoint**:
    - I'll give it a name tag `S3_endpoint`.
    - In the "Service category", I'll choose "AWS services".
    - Under "Services", I'll pick the Amazon S3 service name that corresponds to my region `com.amazonaws.us-east-1.s3`.
        - When presented with the choice between "Interface" and "Gateway", I'll select "Gateway" since I'm setting up for Amazon S3.
    - I'll specify the VPC I want this endpoint in which is "My default VPC".
    - For "Route tables", I'll associate the route table "rtb-8583fbfb" .
    - In the "Policy" section, I'll give "Full access" for simplicity, but is good practice to refine it for security.
    - I'll click on "Create endpoint".
    <br>![[Pasted image 20230926130131.png]]
      





 **To verify the functionality of the VPC endpoint I set up, I followed these steps:**
 
 1. **EC2 Instance Setup**:
     - Launched an EC2 instance within a private subnet.
     - Established a connection to the instance.
 2. **AWS Configuration on EC2**:
     - Once connected, I configured the AWS CLI credentials to allow interaction with S3.
 3. **File Creation**:
     - For testing purposes, I generated a file named `test.txt` on the EC2 instance.
       `[ec2-user@ip-172-31-2-88 ~]$ echo "test" > test.txt`

> [!success] 
> 4. **S3 Bucket Creation**:
>     - I created a new S3 bucket in the `us-east-1` region.
> ```bash
> [ec2-user@ip-172-31-2-88 ~]$ aws s3api create-bucket --bucket my-test-bucket-unique-name --region us-east-1
> {
> "Location": "/my-test-bucket-unique-name"
> }
> ```
>     
> 5. **File Upload to S3**:
>     - Uploaded the `test.txt` file to the newly created S3 bucket.
> ```bash
> [ec2-user@ip-172-31-2-88 ~]$ aws s3 cp test.txt s3://my-test-bucket-unique-name/
> upload: ./test.txt to s3://my-test-bucket-unique-name/test.txt 
> ```
>     
> 6. **Bucket Content Verification**:
>     
>     - Verified that the file was successfully uploaded by listing the contents of the S3 bucket.
> ```bash
> [ec2-user@ip-172-31-2-88 ~]$ aws s3 ls s3://my-test-bucket-unique-name/
> 2023-09-26 19:52:18          5 test.txt
> ```
> <br>![[Pasted image 20230926155340.png]]
