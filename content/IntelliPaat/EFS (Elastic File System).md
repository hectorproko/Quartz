[[EFS vs FSx]]

Managed [[NAS (Network Attached Storage)|NAS]] based on [[NFS (Network File System) protocol|NFS]]
# What is EFS?

EFS (Elastic file system) is a file-level storage service that provides a shared elastic file system with virtually limitless scalability. EFS is a highly available storage system that can be used by multiple servers at the same time. Amazon Web Services EFS is a fully managed service that provides on-demand scalability. This means that the user does not have to be concerned about their workload increasing or decreasing. If the workload suddenly increases, the storage will automatically scale up, and if the workload decreases, the storage will automatically scale down.

Managed [[NAS (Network Attached Storage)]] service

# Why do we need EFS
If our application is running on Amazon EC2 and needs a file system or in any use case where a file system is needed

# Features of EFS
- Completely managed
- Data security that is both accessible and long-lasting
- Lifecycle management and storage classes
- Compliance and security
- Performance that scales
- Serverless file storage and containers
# ![[EBS vs EFS]]


# Creating and Mounting an EFS on AWS
#chat 
#miniProject 
Steps to created an EFS and mount it onto an Ubuntu EC2 instance.

> [!NOTE] Creating and Mounting an EFS on AWS
> Did it here [[Assignment 3 – EC2 And EFS_Module2_AWS Weekday BC = 2301080808|Assignment 3 – EC2 And EFS]]
> #### Setting Up an EC2 Instance
> 
> 1. **Launch EC2 Instance**: In your AWS dashboard, click on "Launch Instance."
> 2. **Instance Details**: Name your instance `Ubuntu EFS` and choose the AMI of Ubuntu.
> 3. **Key Pair**: Choose an existing key pair that is not a demo key.
> 4. **Network Settings**:
>     - Edit network settings but leave the VPC and Subnet as default.
>     - Choose a security group (Example: `launch-wizard-18`). Note this down for later.
> 
> #### Creating an EFS
> 
> 5. **Navigate to EFS**: Go to the AWS EFS service.
> 6. **Create File System**:
>     - Name it `Ubuntu EFS`.
>     - Set VPC to default.
>     - Choose `Standard` as the storage class.
> 7. **Mount Targets**: Wait for mount targets to be created.
> 
> #### Modifying Security Groups
> 
> 8. **Update Security Groups for EFS**: Go to Manage -> Security Groups and attach the same security group as your EC2 instance (`launch-wizard-18`).
> 
> #### Connecting EC2 and EFS
> 
> 9. **Connect to EC2**: SSH into your Ubuntu EC2 instance once it's running.
> 10. **Update Packages**: Run `sudo apt-get update`.
> 11. **Install NFS Client**: Run `sudo apt-get install nfs-common -y`.
> 
> #### Mounting EFS on EC2
> 
> 12. **Create Directory**: Create a directory where EFS will be mounted. Run `sudo mkdir /EFS`.
> 13. **Mount EFS**: Use the AWS-provided NFS client command or DNS/IP information to mount the EFS to the directory. Example: Run `sudo mount -t nfs -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 DNS_NAME:/ /EFS`.
> 
> #### Verifying the Mount
> 
> 14. **Check Mount**: Run `df -h` to verify that EFS has been successfully mounted.
> 
> #### Create a Test File
> 
> 15. **Navigate to EFS Directory**: Run `cd /EFS`.
> 16. **Create File**: Run `sudo touch 1.txt` to create a file in the mounted EFS directory.

> [!attention]
> > <mark style="background: #FFF3A3A6;">*Need to create security group to open EFS, this sample jut opens everything*</mark>
> > **NFS (Port 2049)**: The main port you'll need to open is 2049, which is used for NFS (Network File System) operations.
> 


