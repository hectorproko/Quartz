[[EFS vs FSx]]
Managed [[NAS (Network Attached Storage)|NAS]] service based on [[SMB (Server Message Block) protocol|SMB protocol]]

# What is Fsx?

Amazon FSx is a fully managed third-party file system solution. It makes use of SSD storage to provide fast performance with low latency.

Using FSx, we can launch and run high-performing file systems with just a few clicks while avoiding tasks such as provisioning hardware, configuring software, or taking backups


# Use cases of Fsx

- File systems that can establish permissions at the file or folder level and are accessible by multiple users.
- Application workloads that use the [[SMB (Server Message Block) protocol|SMB protocol]] and require shared file storage provided by Windows-based file systems ([[NTFS (New Technology File System)|NTFS]]).
- It is compatible with the following compute services:
  Amazon Elastic Compute Cloud 
  lnstances of Amazon Workspaces
  Instances of Amazon AppStream 2.0 & VMWare Cloud VMS running on AWS Environments.

# File Systems Provided

[[FSx for Windows File Server]]
[[FSx for Lustre]]

> [!attention]- Full List From AWS
> <iframe src="https://aws.amazon.com/fsx/" allow="fullscreen" allowfullscreen="" style="height:100%;width:100%; aspect-ratio: 16 / 9; "></iframe>
> 

# Why use FSx
- Simple and fully managed
- Highly available and durable
- Secure and complaint
- Fast delivery
- Pay only for the used resources
- Easy integration with other
- AWS services

# Features of FSx

Storage: 
[[DFS (Distributed File System)#DFS Namespaces|DFS (Distributed File System) Namespaces]] allow you to group file shares from multiple file systems into a single common folder structure (a namespace) from which you can access the entire file dataset.

Migration:
To copy your files, including both the data and the full set of metadata like ownership and Access Control Lists, to Amazon FSx, use Windows' Robust File Copy (RoboCopy).

Security:
- Supports identity-based authentication via Microsoft Active Directory over the [[SMB (Server Message Block) protocol|Server Message Block (SMB) protocol]].
- Amazon FSx automatically encrypts your data in transit and at rest using [[KMS (Key Management Service)|AWS KMS]] and SMB [[Kerberos]] session keys.
- Amazon FSx is [[ISO (International Organization for Standardization)|ISO]], [[PCI-DSS (Payment Card Industry Data Security Standard)|PCI-DSS]], and [[SOC (System and Organization Controls)|SOC]] compliant, as well as [[HIPAA (Health Insurance Portability and Accountability Act)|HIPAA]] compliant






