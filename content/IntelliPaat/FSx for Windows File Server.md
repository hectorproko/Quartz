### Introduction

Amazon FSx for Windows File Server (FSx) offers a fully managed native Microsoft Windows file system, enabling a wide range of compatibility with Windows-based applications and services. It is designed to work seamlessly with Amazon EC2 instances and integrates well with features like SMB protocol, Windows NTFS, and Microsoft Active Directory.

---

### Key Features

1. **Compatibility**: Fully compatible with Microsoft products; must run Windows version 7 or above.
2. **Access**: Can be accessed from Windows EC2 machines, workspaces, or even VMware Cloud on AWS.
3. **Management**: Fully managed by AWS. Hardware patching and other administrative tasks are taken care of automatically.
4. **Storage**: Uses SSDs for fast performance, but can also use HDDs if required.
5. **Protocols & Systems**: Supports SMB protocol, [[NTFS (New Technology File System)|Windows NTFS]], and Microsoft Active Directory.

---

### Use Cases

1. **Shared File Storage**: Useful for Windows-based applications that require shared file storage.
2. **Development Environment**: Teams can store code and build repositories to facilitate collaborative development.
3. **Bug Fixing & Performance Testing**: Applications and repositories can be shared among team members for bug fixing and performance assessments.

### Supported Clients

#### 1. Amazon EC2 Instances

- **Compatibility**: EC2 instances running Windows or Linux distributions like Ubuntu are fully compatible with Amazon FSx.
- **Use Case**: Ideal for application servers or web servers that require access to a shared Windows file system.

#### 2. [[Amazon WorkSpaces]]

- **Compatibility**: Amazon WorkSpaces running Windows can easily integrate with FSx for shared or individual file storage needs.
- **Use Case**: Useful for virtual desktop scenarios where users need to access or store files on a centralized Windows file system.

#### 3. Amazon AppStream 2.0 Instances

- **Compatibility**: AppStream 2.0, which provides virtual application streaming, is also compatible with FSx.
- **Use Case**: Allows streamed applications to read and write data to a common file system, beneficial in collaborative scenarios.

#### 4. VMware Cloud on AWS

- **Compatibility**: VMware workloads running on AWS can also access FSx for Windows File Server.
- **Use Case**: Good for enterprises running a hybrid cloud solution with VMware workloads, who require access to a Windows-based file system.

---

### Access Methods (Same for All Clients)

1. **DNS Name in Active Directory**: Easy discovery and access to FSx file shares via the DNS name registered in Active Directory.
2. **[[DFS (Distributed File System)#DFS Namespaces|Distributed File System (DFS) Namespace]]**: Can be integrated into your DFS namespace if your organization utilizes this for file storage.

---

### Environments (Applicable for All Clients)

1. **On-Premise Environment**: Even on-premise systems can access FSx if hybrid cloud connectivity is set up.
2. **From an AWS Account, Another VPC, or Region**: 
	- **AWS Account**: FSx can be set up to be accessed from different AWS accounts, offering flexibility in multi-account AWS architectures.
	- **Another VPC**: Through [[VPC peering|VPC peering]] or [[AWS Transit Gateway|AWS Transit Gateway]], you can connect to FSx from a different VPC.
	- **Another Region**: Accessing from a different AWS region is possible but should be carefully planned to account for latency and data transfer costs.




### Failover Process
#### What Triggers the Failover?

- Various conditions can initiate the failover process, such as an issue with the preferred file server, an Availability Zone going down, or during planned maintenance activities.

#### Steps During Failover

1. **Detection of Failure**: The system identifies a need for failover.
2. **Activation of New File Server**: A new file server (likely in a different Availability Zone) becomes active.
3. **Handling Requests**: This new file server starts serving all read and write requests.

#### Post-Failover Activities

1. **Resource Availability**: Once the initial issues are resolved and all resources are available in the required subnet, FSx automatically switches back to the preferred file server.
2. **Data Reconciliation**: Any data changes made during the failover are reconciled.

#### Timing

- The whole process, from detection of the issue to completing the failover, typically takes around 30 seconds. This minimizes downtime and ensures high availability.

The goal of the FSx failover process is to maintain data availability and service integrity with minimal disruption. It's a quick and automated way to handle failures or other issues that might affect your file storage needs.


### Creating an Amazon FSx for Windows File Server on AWS
#chat 
#miniProject 
#### Pre-Requisites:

1. AWS Account
2. A particular instance of Windows AMI
3. Amazon FSx for Windows File Server

#### Part 1: Setting up Directory Service

1. Navigate to AWS Directory Service and choose to set up a directory.
2. Select [[AWS Managed Microsoft AD]].
3. Click on "Next".
4. Choose the standard edition and provide a DNS name. You can use an existing DNS name or create a new one.
5. Set an admin password. Ensure it includes at least three out of these four categories: lowercase, uppercase, numeric, and special characters.
6. Configure the VPC settings:
    - You can leave it as "No Preference" or select a specific VPC and subnet where your instance resides.
7. Review your settings and click "Create Directory". The creation might take up to 30 minutes.

#### Part 2: Creating Amazon FSx for Windows File Server

1. Navigate to Amazon FSx.
2. Click "Create File System".
3. Choose Amazon FSx for Windows File Server.
4. Provide a File System name.
5. Choose the deployment type: Multi-AZ or Single-AZ.
6. Set the storage capacity to a minimum of 32 GiB.
7. Choose your preferred subnet (same as your machine for easy connection).
8. Select your previously created directory.
9. Review settings and click "Create File System". Creation can take up to 30 minutes.

#### Part 3: Connecting to the Windows Instance

1. Go to the AWS EC2 dashboard and choose your Windows machine.
2. Click "Connect" and download the RDP file.
3. Use your private key file to decrypt the password.
4. Use the decrypted password to connect through RDP to the instance.

#### Part 4: Configuring Network Settings

1. Open "Control Panel" on your Windows instance.
2. Navigate to "Network and Internet" -> "Network and Sharing Center" -> "Change Adapter Settings".
3. Go to "Ethernet" -> "Properties" -> "Internet Protocol Version 4 (TCP/IPv4)".
4. Use the following DNS server addresses and input DNS from your AWS directory.

#### Part 5: Joining the Domain

1. Navigate to "System" -> "Advanced System Settings" -> "Computer Name" -> "Change".
2. Choose "Member of Domain" and input your domain name.
3. Provide the admin username and password.

#### Part 6: Mounting the File System

1. Open Command Prompt.
2. Run a command to map the FSx file system to a drive letter (e.g., `net use H: \\fsx\share`).
3. When prompted, provide your directory credentials.

You should now see the Amazon FSx mapped to a drive on your Windows instance.

Please note that this is a simplified step-by-step guide. The actual process may vary based on your specific requirements.


# Pricing

## Windows File Server in North Virginia (us-east-1)

### Storage Options:

1. SSD storage capacity
2. HDD storage capacity
3. Throughput storage capacity
4. Backup storage capacity
![[Pasted image 20230821172146.png]]
#### Pricing Example:
![[Pasted image 20230821172247.png]]
- **Deployment**: Single-AZ 
- **Storage**: SSD 
- **Cost**: $0.130 per GB per month 

### Problem Statement:

- **Data to Store**: 10 TB
- **Storage Type**: HDD 
- **Deployment**: Multi-AZ
- **Throughput**: 60 MBPS 
- **Backup**: 5 TB average during the month

#### Calculations:

1. **Storage Cost**: 
    - HDD cost in Multi-AZ is $0.025 per GB per month.
    - `5 TB x 0.025`
  
2. **Throughput Cost**: 
    - Cost for Multi-AZ is $4.5 per MBPS per month.
    - `60 MBPS x 4.5 = $270 per month`
  
3. **Backup Cost**: 
    - Cost is $0.050 per GB per month (both Single and Multi-AZ)
    - `5 TB x 0.050`

4. **Total Monthly Cost**: $456
