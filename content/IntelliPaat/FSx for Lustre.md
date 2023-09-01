FSx for Lustre makes it very easy to launch and run the world's most popular file system [[Lustre]]

# Features of Amazon FSx for Lustre

- Most popular high-performance file system
- Seamless integration with our Amazon [[S3]] data
- Accessible from on-premises
- Multiple deployment options
- Data accessible to other AWS services
- Simple and fully managed

We can integrate it with S3 that makes it easier to process datasets. When linked with S3, Lustre shows all S3 objects as files, and any change made will reflect in the S3 bucket as well

# Use Cases


[[ML (Machine Learning)]] 
workloads use massive amounts of training data. Multiple instances need to process this training data simultaneously, so a shared file storage is very helpful

Media Processing and Transcoding:
Media workflows, such as video rendering and visual effects, need compute and storage resources to handle the massive amounts of data being created

# FSx For Lustre Creation
#chat #miniProject 
We do it in [[Assignment 4 – FSx_Module2_AWS Weekday BC = 2301080808#2. Create an FSx file system for Lustre and attach it to an Amazon Linux 2 instance.|Assignment 4]]

### Step 1: Launch FSx for Lustre

1. Navigate to the Amazon FSx service in the AWS Console.
2. Select "Amazon FSx for Lustre" and click on it.

---

### Step 2: Configure File System

1. Provide a name for your file system.
2. Choose the Deployment and Storage type. In this example, we will go with "Scratch" and "SSD."
3. Configure the throughput and storage. The minimum size you can set is 1.2 TiB. The throughput will be calculated based on this size.

---

### Step 3: Network and Security

1. Select the default VPC.
2. Open your machine's security group to edit inbound rules.
    - Add a custom TCP rule to allow inbound traffic on TCP port 988.
    - Add another custom TCP rule to allow port range 1021-1023.
3. Save the changes.

---

### Step 4: EC2 Setup

1. Ensure you have an EC2 instance running Amazon Linux.
2. Connect to your EC2 instance.
3. Update the instance by running `sudo yum update`.
4. Install dependencies needed for FSx for Lustre with the appropriate commands. 
```bash
sudo amazon-linux-extras install -y lustre2.10
```
   

---

### Step 5: Attach FSx to EC2

1. Navigate back to the FSx console and click "Attach" on your file system.
2. Copy the provided command to create a directory on your EC2 instance. Run this command.
3. Copy and run the provided command to mount the FSx file system to the directory you created.

---

### Step 6: Verify

1. Run verification commands to ensure the FSx filesystem is successfully mounted.

---

### Conclusion:

- Your FSx file system is now set up and attached to your EC2 instance.


# Calculating Pricing

## Lustre in North Virginia (us-east-1)
### Storage Options:

1. Scratch
2. Persistent

#### Pricing Example:

- **Type**: Scratch 
- **Cost**: $0.14 per GB per month
![[Pasted image 20230821172406.png]]
### Problem Statement:

- **Data to Store**: 4800 GB
- **Usage**: 8 hours/day for 30 days
![[Pasted image 20230821172443.png]]
#### Calculations:

1. **Hourly Cost**: 
    - `$0.14 / (30 x 24)`
  
2. **Total Cost**: 
    - Hourly Cost x 4800 GB x 8 hours/day x 30 days
