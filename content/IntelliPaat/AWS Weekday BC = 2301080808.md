# SELF-PACED

# Module 1 - Introduction To Cloud Computing And AWS

### Lecture 1 – Introduction To Cloud Computing

#### The "NET"
**What is Internet/lntranet**
- A global computer network using standardized communication protocols (e.g. UDP, TCP/IP) Providing information and communication facilities, consisting of interconnected networks ^652c81
- Intranet is a local private network created usingWorld Wide Web.

#### Virtualization
- Virtualization is the primary technology that supports cloud computing.
- A service that results from virtualization, which is software that modifies hardware, is referred to as cloud computing. Virtualization is necessary for cloud computing to exist.

### Lecture 2 – Deployment And Service Models

#### Models & Deployments

[[Cloud Service Models]]
- [[IaaS (Infrastructure as a Service)]]: AWS, Rackspace, MS Azure etc.
- [[PaaS (Platform as Service)]]: AWS Elastic Beanstalk, Heroku etc.
- [[SaaS (Software as a Service)]]: Google drive, docs, MS Office 365 etc.

Cloud Deployment Models
- Public Cloud (AWS, MS Azure, Google Platform, IBM Bluemix etc.)
- Private Cloud (HPE, VMware, RedHat OpenStack, Dell EMC etc.)
- Hybrid Cloud

### Lecture 3 – AWS Suite

### Lecture 4 – Virtualization In AWS

![[Types of Hypervisor.png]]
What is [[hypervisor]]
Disadvanate of TYPE-1 is that you need seprate machine for instructions

#### [[XEN Hypervisor]]

### Lecture 5 – AWS Vs Azure Vs GCP

### <mark style="background: #FFB8EBA6;">Introduction To Cloud Computing And AWS – Quiz</mark>

> [!NOTE]- Introduction to Cloud Computing and AWS – Quiz
> 
> 
> ### 1. Which is the hypervisor software used by AWS for virtualization?
> - **Marked Answer:** Xen Server
> - **Correct Answer:** XEN SERVER  
> **TOTAL MARKS: 1 | OBTAINED: 1**
> 
> ### 2. What kind of service is AWS RDS?
> - **Marked Answer:** PaaS
> - **Correct Answer:** PAAS  
> **TOTAL MARKS: 1 | OBTAINED: 1**
> 
> ### 3. What is the name of AWS’s object based storage service?
> - **Marked Answer:** S3
> - **Correct Answer:** S3  
> **TOTAL MARKS: 1 | OBTAINED: 1**
> 
> ### 4. “Cloud” in cloud computing represents what?
> - **Marked Answer:** Internet
> - **Correct Answer:** INTERNET  
> **TOTAL MARKS: 1 | OBTAINED: 1**
> 
> ### 5. What type of hypervisor is used in AWS?
> - **Marked Answer:** Type 1
> - **Correct Answer:** TYPE 1  
> **TOTAL MARKS: 1 | OBTAINED: 1**
> 
> ---
> **Total Marks:** 5/5

# Module 2 - Introduction To EC2, EBS, EFS And Amazon FSx

## Chapter 1 - EC2 And EBS

### Module Agenda

### Lecture 1 – EC2 Introduction

![[EC2 (Elastic Compute Cloud)#Features of EC2|Features of EC2]]


Elastic: It is the level at which a system is able to adapt to workload changes by provisioning and de-provisioning resources such that the resources meet the current demand as closely as possible

### Lecture 2 – Region And Availability Zones
[[region_aws]]
[[AZ (Availability Zone)_aws]]

### Lecture 4 – EC2 [[AMI (Amazon Machine Image)|AMI]]

![[AMI (Amazon Machine Image)#What is an AMI?]]

![[AMI (Amazon Machine Image)#Creating and Copying an AMI]]


### Lecture 5 – Public IP vs Elastic IP

Public IP
• It is not associated with an AWS account
• No charges for the public IP, even if it is not being used while the instance is running
• Whenever the instance is re-launched, the public IP changes

Elastic IP
• It is associated with the AWS account
• Charges will be applied if the same is done with the elastic IP
• The elastic IP is the same and static for every launch until we manually release it

Elastic Network Interface
A network interface is the interface between a computer and an Internet network. The network IO happens through network interface cards

Network interfaces contain:
- [[AWS_Elastic IP|Elastic IP]]
- Public IP
- Private IP
- [[sg (Security Group)|Security Groups]]


### Demo 1 – Creating Ubuntu Instance
#miniProject #pendingvideotrancript
### Demo 2 – EC2 Connect Via [[PuTTY]]  
Need to convert the key from .pem to something putty uses 
#miniProject #pendingvideotrancript
### Demo 3 – Creating Windows Instance 
#miniProject #pendingvideotrancript
### Demo 4 – Connecting Windows EC2
You upload a .pem, to decrypt using Tab RDP, shows a password then you log in. You can also use Remote Desktop program
#miniProject #pendingvideotrancrip

### Lecture 6 – AMI Creation And Copy 
#miniProject 

#chat  <mark style="background: #FFF3A3A6;">Video Transcript</mark>
> [!NOTE]- How to Create and Copy an AMI to Another Region
> 
> **Introduction:**
> 
> - Welcome to this session!
> - We'll learn how to create an Amazon Machine Image (AMI) and copy it to another region.
> 
> ---
> 
> **Steps to Create an AMI:**
> 
> 1. **Launch an Instance:**
>     
>     - Navigate to "launch instance".
>     - Choose a machine of the Ubuntu type.
>     - Name the instance "Ubuntu".
>     - For naming, select the "Ubuntu AMI".
>     - Choose your key (previously created).
>     - Make no further changes.
>     - Click on "launch instance".
>     - Wait for the instance to change from "pending" to "running".
> 2. **Why Copy an AMI?:**
>     
>     - Directly moving a machine from one region to another isn't possible.
>     - If we copy the OS or AMI, we can replicate the machine in another region.
> 3. **Create an Image of the Machine:**
>     
>     - Select your running machine.
>     - Go to "action" > "image and template" > "create image".
>     - Name the image (e.g., "Ubuntu AMI copy").
>     - Optionally, provide a description (e.g., "Ubuntu AMI").
>     - Click on "create image".
>     - Navigate to AMIs. The new image should be visible in "pending" state.
> 
> ---
> 
> **Steps to Copy AMI to Another Region:**
> 
> 1. **Copy the AMI:**
>     
>     - Once the AMI status is "available", select it.
>     - Click on "copy AMI".
>     - The source AMI will be auto-filled.
>     - Choose the destination region (e.g., "OREGON").
>     - Click on "copy".
>     - The copying might take a few minutes.
> 2. **Check in the New Region:**
>     
>     - Navigate to the OREGON region.
>     - Your copied AMI should be visible, initially in "pending" state.
>     - Rename it if needed (e.g., "Ubuntu AMI").
>     - Wait until the AMI status changes to "available".
> 3. **Launch an Instance from the Copied AMI:**
>     
>     - With the available AMI, you can launch an instance.
>     - Note: You won't have to select an AMI since one is already chosen.
>     - Choose the rest of your configurations.
>     - Select the available key in this region.
>     - Launch the instance.
> 
> ---
> 
> **Conclusion:**
> 
> - We've successfully created an AMI, copied it to another region, and launched an instance using that AMI.
> - Join us in the next session for more insights! Thank you.


### Lecture 7 – EBS Introduction

![[EBS (Elastic Block Store)#What is EBS|What is EBS]]

#chat <mark style="background: #FFF3A3A6;">from transcript</mark>
[[EBS (Elastic Block Store)#Introduction to Elastic Block Store (EBS)]]

### Lecture 8 – EBS Concept

![[EBS (Elastic Block Store)#EBS Concepts]]



### Demo 5 – EBS For Ubuntu 
#miniProject 
#chat 
> [!NOTE]- Demo 5 – EBS For Ubuntu Steps
> It seems like you've provided a detailed walkthrough on creating, attaching, formatting, and using an Amazon Elastic Block Store (EBS) volume with an EC2 instance. Here's a summarized version of the steps for clarity:
> 
> **Attaching and Using Amazon EBS with EC2 Instance:**
> 
> 1. **Create an EBS Volume**:
>     
>     - Navigate to the EBS section in the AWS console.
>     - Click "Create Volume".
>     - Specify the desired size (e.g., 5GB) and select the availability zone corresponding to your EC2 instance.
>     - Name the volume (e.g., 0.2EBS).
> 2. **Attach the Volume**:
>     
>     - In the EBS section, choose "Attach Volume" from the "Actions" menu.
>     - Select the target EC2 instance and specify the device name (e.g., /dev/sdf).
>     - Confirm and attach the volume.
> 3. **Connect to Your EC2 Instance**:
>     
>     - Navigate to the EC2 dashboard and click "Connect".
>     - Use EC2 Instance Connect or SSH to access the machine.
> 4. **Identify the New Volume**:
>     
>     - Execute `lsblk` to view all block devices. Identify your new EBS volume (e.g., xvdf).
> 5. **Check and Format the EBS Volume**:
>     
>     - Use `file -s` to check if the volume is formatted.
>     - If not, format the EBS volume using the `mkfs` command, e.g., `sudo mkfs -t ext4 /dev/xvdf`.
> 6. **Mount the EBS Volume**:
>     
>     - Create a new directory to mount the volume, e.g., `sudo mkdir /ebs1`.
>     - Mount the EBS volume: `sudo mount /dev/xvdf /ebs1`.
> 7. **Verify the Mount**:
>     
>     - Check mounted filesystems using `df -h`.
>     - To utilize the full storage size, you can optionally resize using `resize2fs`.
> 8. **Unmounting the Volume**:
>     
>     - When you want to detach the EBS volume or stop using it temporarily, unmount it using `sudo umount /dev/xvdf`.
> 
> Remember to regularly back up your data and ensure EBS volumes are detached properly before terminating EC2 instances to avoid data loss.
> 
> The guide you've provided is comprehensive and offers users a clear path to integrating EBS volumes with their EC2 instances. Well done!

### Demo 6 – EBS For Windows
#miniProject 
#chat 
> [!NOTE]- EBS For Windows Steps
> Thank you for the detailed step-by-step guide on attaching an EBS (Elastic Block Store) volume to a Windows EC2 instance in AWS. It's evident you've provided a hands-on approach to this process.
> 
> To summarize:
> 
> 1. **Verify Availability Zone**: Before creating an EBS volume, always ensure it's in the same availability zone as your EC2 instance.
>     
> 2. **Create EBS Volume**: Navigate to the EBS dashboard and create a volume, specifying the desired size and the availability zone, matching that of your EC2 instance.
>     
> 3. **Name and Attach the Volume**: After the EBS volume is created and available, give it a meaningful name. Then, select the volume, navigate to 'Actions', and select 'Attach Volume'. Choose the desired EC2 instance and confirm the attachment.
>     
> 4. **Access EC2 Instance via RDP**: Download the RDP file for the EC2 instance, get the necessary credentials, and access the instance.
>     
> 5. **Initialize and Format the EBS Volume**: Once connected to the EC2 instance, the EBS volume will not be immediately visible in 'This PC'. You need to go to Disk Management (`diskmgmt.msc`), bring the disk online, and create a simple volume on it. Assign a drive letter and format it as NTFS.
>     
> 6. **Access the New Volume**: Post-formatting, the EBS volume should be accessible from 'This PC' as a new drive.
>     
> 
> Always remember, EBS volumes act like raw, unformatted block devices. To start using an EBS volume with an EC2 instance, you must first initialize it, which you demonstrated excellently.
> 
> The guide you've shared is clear and will be useful for AWS beginners and intermediate users looking to understand the process of EBS attachment and initialization on Windows.





  
### Lecture 9 – EBS Snapshot

Created a snapshot from EBS and they after deleting EBS, recreated it using snapshot

#chat 
1. Creating an EBS Volume in AWS
2. Encrypting EBS Volumes
3. Creating a Snapshot of an EBS Volume
4. Restoring an EBS Volume from a Snapshot

**Pre-requisites:**
- A running instance in AWS (for this tutorial, I am using an Ubuntu instance).
- AWS console access with appropriate permissions.

> [!NOTE]- Steps
> ### Step 1: Create an EBS Volume
> 
> 1. **Navigate to the EC2 Dashboard** and click on 'Volumes' under the 'Elastic Block Store' section.
> 2. **Click 'Create Volume'** and select the following options:
> 
> - Volume Type: General Purpose
> - Size: 6 GiB
> - Availability Zone: Choose the same zone where your instance is running (e.g., US-H1C).
> 
> #### To Encrypt the EBS Volume
> 
> - Click on 'Encrypt this volume'
> - You will be prompted to choose a [[KMS (Key Management Service)]] key. You can either select the default AWS KMS key or provide a custom KMS key.
> 
> ---
> 
> ### Step 2: Attach the EBS Volume to an Instance
> 
> 1. Select the created volume.
> 2. Click on 'Actions' and then 'Attach Volume'.
> 3. Choose your instance and click 'Attach'.
> 
> ---
> 
> ### Step 3: Modifying the EBS Volume Size
> 
> 1. Go to 'Volumes' and select your EBS volume.
> 2. Click on 'Actions' and then 'Modify Volume'.
> 3. Note: You cannot reduce the size, only increase it.
> 
> ---
> 
> ### Step 4: Create a Snapshot
> 
> 1. Select your EBS volume.
> 2. Click on 'Actions' and then 'Create Snapshot'.
> 3. Provide a description and name for the snapshot.
> 
> Snapshots serve as backups for your volumes. If you lose your EBS volume, you can restore it from a snapshot.
> 
> ---
> 
> ### Step 5: Restore EBS Volume from a Snapshot
> 
> 1. Go to 'Snapshots' and select the snapshot you created.
> 2. Click on 'Actions' and then 'Create Volume from Snapshot'.
> 3. Choose the same settings as your original volume, including the availability zone.

**Conclusion**
In this session, we covered how to create, modify, and encrypt EBS volumes as well as how to create and restore from snapshots. This is essential for managing your AWS resources efficiently and securely. See you in the next session!


## Chapter 2 - EFS And Amazon FSx

### Lecture 1 – EFS Concepts And EBS
![[EFS (Elastic File System)#What is EFS?]]

![[EFS (Elastic File System)#Why do we need EFS]]

![[EFS (Elastic File System)#Features of EFS]]

![[EBS vs EFS]]

### Lecture 2 – EFS Creation

![[EFS (Elastic File System)#Creating and Mounting an EFS on AWS]]


### Lecture 3 – [[FSx|FSx]] Introduction

![[FSx#What is Fsx?]]

![[FSx#Use cases of Fsx]]

![[FSx#File Systems Provided]]

![[FSx#Why use FSx]]

### Lecture 4 – Features Of FSx

![[FSx#Features of FSx]]


### Lecture 5 – Amazon FSx For Windows File Server

*Expand in the note we embedded*

![[FSx for Windows File Server]]




what is directory service


### [[FSx for Windows File Server#Creating an Amazon FSx for Windows File Server on AWS|Demo 1 – Amazon FSx For Windows Creation]]

### Lecture 6 – [[FSx for Lustre|Amazon FSx For Lustre]]

### Demo 2 – [[FSx for Lustre#FSx For Lustre Creation|Amazon FSx For Lustre Creation]]

### Lecture 7 – Amazon FSx Pricing
[[FSx for Lustre#Calculating Pricing|FSx For Lustre]]
[[FSx for Windows File Server#Pricing|FSx For Windows]]


### Lecture 8 – Instance Tenancy And Reserved Spot Instances

#### Tenancy Types: Who Owns the Resource?

#### Shared or Default Tenancy

- **Definition**: Multiple customers share the same underlying hardware.
- **Hypervisor**: Uses Zen Hypervisor, as implemented by AWS.
- **Usage**: Suitable for general workloads that don't require isolation at the hardware level.

#### Dedicated Tenancy

- **Definition**: Single customer uses the underlying hardware.
- **Usage**: Suitable for workloads that require isolation for security or compliance reasons.

---

#### Placement Groups: How Are Instances Arranged?

#### Function
- **Role**: Determines how instances are spatially arranged on the underlying hardware.
- **Goal**: To minimize failure rate and optimize performance based on workload requirements.

#### Types of Placement Groups
- **Cross-Platform**: Ensures high availability across multiple availability zones and regions.

---

#### Instance Buying Options: How to Pay for What You Use?

#### Reserved Instances
- **What Is It?**: A pre-booked contract to reserve instances for a set period.
- **Benefits**:
    - **Cost Savings**: Discounted rates compared to on-demand pricing.
    - **Hardware Options**: Potentially better hardware at cheaper rates.

#### Spot Instances
- **What Is It?**: Bidding on unused EC2 instances.
- **How It Works**:
    - Bid for an instance at your chosen price.
    - If the spot price is below your bid, you get the instance.
    - If the spot price goes above, the instance is terminated.
- **Benefits**:
    - **Cost Savings**: Often cheaper than on-demand pricing.
    - **Best for Temporary Workloads**: Ideal for workloads that are not time-sensitive.

[[EC2 (Elastic Compute Cloud)#EC2 Pricing]]

#### On-Demand vs. Reserved Instances
- On-demand pricing for `m5.xlarge` is $0.192 per hour.
- Reserved instances offer cost savings if reserved for 1 to 3 years.

[[EBS (Elastic Block Store)#EBS Pricing]]


### Introduction To EC2, EBS And EFS – Quiz
> [!summary]- Quiz
> 1. Which instance type is free tier eligible?
> 
> - The `t2.micro` instance type is generally the one that is free tier eligible.
> 
> 2. How is Elastic IP different from Public IP?
> 
> - `EIP is static even when rebooted` is the correct answer. Elastic IPs are static IP addresses allocated to your account that you can attach to instances. They remain associated with your instances even when they're stopped or rebooted, whereas public IPs can change under those circumstances.
> 
> 3. What types of EBS volume can be used in multi-attach?
> 
> - `IO1` is the EBS volume type that can be used in multi-attach configurations. As of my last update in September 2021, only the `io1` and `io2` types support multi-attach.
> 
> 4. EFS can be concurrently connected to hundreds of instances?
> 
> - `TRUE`. Amazon EFS is designed to be a highly scalable file storage that can be concurrently connected to multiple EC2 instances.
> 
> 5. What tool should be used to create a clone of an EC2 instance?
> 
> - `AMI` (Amazon Machine Image) is the right tool for creating a clone of an EC2 instance. You can create an AMI of your instance and then launch other instances from that AMI.





# Module 3 - Introduction To IAM And CloudWatch

## Module Agenda

## Lecture 1 – IAM Introduction


[[IAM (Identity and Access Management)#Lecture 1 – IAM Introduction]]


[[ARN (Amazon Resource Name)#Lecture 1 – IAM Introduction]]


### Demo 1 – Users And Groups Creation
[[IAM (Identity and Access Management)#Demo 1 – Users And Groups Creation|Steps to follow the Demo]]

### Lecture 3 – Policies And Permissions
[[IAM (Identity and Access Management)#Lecture 3 – Policies And Permissions]]

### Demo 2 – Attaching Policies To Users And Groups
[[IAM (Identity and Access Management)#Demo 2 – Attaching Policies To Users And Groups]]

### Lecture 4 – Roles
[[IAM (Identity and Access Management)#Lecture 4 – Roles]]

### Demo 3 – Using Roles In IAM
[[IAM (Identity and Access Management)#Demo 3 – Using Roles In IAM]]

### Lecture 5 – Identity Federation
[[IAM (Identity and Access Management)#Lecture 5 – Identity Federation]]

  
### Lecture 6 – Introduction To CloudWatch

[[CloudWatch_aws#Lecture 6 – Introduction To CloudWatch]] 


  
### Lecture 7 – CloudWatch Dashboard And IAM
[[CloudWatch_aws#Lecture 7 – CloudWatch Dashboard And IAM]]

### Demo 4 – Creating CloudWatch Dashboard
[[CloudWatch_aws#Demo 4 – Creating CloudWatch Dashboard]]

  
### Demo 5 – Creating CloudWatch Alarm

### Demo 6 – Creating Billing Alarm
Same thing


### Lecture 8 – IAM Access Analyzer

[[IAM (Identity and Access Management)#Lecture 8 – IAM Access Analyzer]]


### Demo 7 – IAM Access Analyzer
[[IAM (Identity and Access Management)#Demo 7 – IAM Access Analyzer]]


### Lecture 9 – Policy Simulator And EventBridge
[[Policy Simulator_aws#Lecture 9 – Policy Simulator And EventBridge]]


### Demo 8 – Policy Simulator
[[Policy Simulator_aws#Demo 8 – Policy Simulator]]

### Lecture 10 – CloudTrail
- [[CloudTrail_aws#Lecture 10 – CloudTrail]]
- [[AWS Config_aws#Lecture 10 – CloudTrail|AWS Config]]



### INTRODUCTION TO IAM AND CLOUDWATCH – QUIZ

> [!NOTE]-
> - What is the full form of ARN?
>     **Marked Answer :**
>     Amazon Resource Name
>     
>     **Correct Answer :
>     AMAZON RESOURCE NAME
>     
>     **TOTAL MARKS : 1MARKS OBTAINED  1
> - You are asked to create 10 users and provide EC2 permissions to 5 users and EC2, S3 permissions to 7 of the users. What is the best way to do this?
>     
>     **Marked Answer :**
>     Create 10 users. Create 2 groups, add 5 users who need only EC2 permissions and attach EC2 policy to the group. Add 7 users who need EC2 and S3 permissions to the second group and attach EC2, S3 policies to the group.
>     
>     **Correct Answer :
>     CREATE 10 USERS. CREATE 2 GROUPS, ADD 5 USERS WHO NEED ONLY EC2 PERMISSIONS AND ATTACH EC2 POLICY TO THE GROUP. ADD 7 USERS WHO NEED EC2 AND S3 PERMISSIONS TO THE SECOND GROUP AND ATTACH EC2, S3 POLICIES TO THE GROUP.
>     
>     **TOTAL MARKS : 1MARKS OBTAINED  1
> - IAM Roles provide temporary access to the attached permissions.
>     
>     **Marked Answer :**
>     TRUE
>     **Correct Answer :
>     TRUE
>     
>     **TOTAL MARKS : 1MARKS OBTAINED  1
> - Which is NOT a CloudWatch alarm state?
>     
>     **Marked Answer :**
>     OKAY
>     **Correct Answer :
>     OKAY
>     
>     **TOTAL MARKS : 1MARKS OBTAINED  1
> - How much does one alarm cost per month?
>     
>     **Marked Answer :**
>     0.10 $
>     **Correct Answer :
>     0.10 $
>     
>     **TOTAL MARKS : 1MARKS OBTAINED  1
> 
> Total Marks**5 / 5**



# Module 4 - Introduction To Elastic Load Balancer And Auto Scaling

## Module Agenda

## Lecture 1 – ELB Introduction

[[ELB (Elastic Load Balancer)#Lecture 1 – ELB Introduction]]

## Lecture 2 – Types Of Load Balancer

[[ELB (Elastic Load Balancer)#Lecture 2 – Types Of Load Balancer]]

## Demo 1 – Creating Application Load Balancer
[[ELB (Elastic Load Balancer)#Demo 1 – Creating Application Load Balancer]]

## Demo 2 – Creating Network Load Balancer
[[ELB (Elastic Load Balancer)#Demo 2 – Creating Network Load Balancer]]

## Lecture 3 – Architecture And Weighted Routing In Load Balancer
[[ELB (Elastic Load Balancer)#Lecture 3 – Architecture And Weighted Routing In Load Balancer]]

## Lecture 4 –  Demo: Weighted Routing
[[ELB (Elastic Load Balancer)#Lecture 4 – Weighted Routing]]

  
## Lecture 5 – Sticky Session
[[ELB (Elastic Load Balancer)#Lecture 5 – Sticky Session]]

## Demo 3 – Sticky Session
[[ELB (Elastic Load Balancer)#Demo 3 – Sticky Session]]

  
## Lecture 6 – Auto Scaling Introduction
[[Auto Scaling_aws#Lecture 6 – Auto Scaling Introduction]]

## Lecture 7 – Components Of Auto Scaling
[[Auto Scaling_aws#Lecture 7 – Components Of Auto Scaling]]

## Demo 4 – Auto Scaling Creation
[[Auto Scaling_aws#Demo 4 – Auto Scaling Creation]]

## Lecture 8 – ELB And Auto Scaling Integration
[[Auto Scaling_aws#Lecture 8 – ELB And Auto Scaling Integration]]

## Demo 5 – ELB And Auto Scaling Integration