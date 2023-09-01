Going over an assigment 

CLient and Master, when creatin client  you should have .pem key
Only master can ssh to client so we create .pem file in Master and copy contents for .pem , change permissions to read only for user


> [!NOTE] AWS EC2 Instance Setup - Live Lecture Transcript
> **Part 1: Introduction and Setup**
> 
> In this live lecture, we will walk through the process of setting up and connecting to AWS EC2 instances. EC2 instances are virtual servers that you can create and manage in the Amazon Web Services cloud platform.
> 
> **Part 2: Launching the Master Instance**
> 
> 1. **Creating a Key Pair:**
>     
>     - Open the AWS Management Console.
>     - Navigate to the EC2 Dashboard.
>     - Choose "Key Pairs" from the left menu.
>     - Click "Create Key Pair" and provide a name for the key pair.
>     - Save the private key (.pem) file securely.
> 2. **Launching the Master Instance:**
>     
>     - Navigate to the EC2 Dashboard.
>     - Click "Launch Instance" and choose an Amazon Machine Image (AMI).
>     - Select the instance type (e.g., t2.micro for free tier eligibility).
>     - Choose the previously created key pair.
>     - Configure the security group rules to allow SSH traffic from anywhere.
>     - Launch the instance.
> 
> **Part 3: Adding Security Group Rules**
> 
> 1. **Modifying Security Group Rules for Master Instance:**
>     
>     - Remove existing rule or add a new one.
>     - Choose "SSH" and set source type to "Anywhere."
> 2. **Security Group Rules for Client Instance:**
>     
>     - Create a new security group named "client security group."
>     - Set rules to allow SSH traffic from master instance's private IP.
>     - Save changes.
> 
> **Part 4: Connecting to Instances**
> 
> 1. **Connecting to Master Instance:**
>     
>     - Use the EC2 instance connect option.
>     - Confirm successful connection.
> 2. **Connecting to Client Instance:**
>     
>     - Attempt to connect using EC2 instance connect.
>     - Understand that it fails due to restrictions.
> 
> **Part 5: Resolving Client Instance Connection Issue**
> 
> 1. **Understanding the Issue:**
>     
>     - Client instance can only be accessed via master's IP.
> 2. **SSH Connection from Master:**
>     
>     - Connect to client instance from the master using SSH.
>     - This is possible due to the allowed communication from master to client.
> 
> **Part 6: SSH Key Setup and Permissions**
> 
> 1. **Importing Key Pair to Master Instance:**
>     
>     - Create a file and paste the private key content.
>     - Save and exit the editor.
> 2. **Setting File Permissions:**
>     
>     - Change file permissions using CHMOD to make the key file read-only.
>     - Verify the changed permissions.
> 
> **Part 7: Connecting to Client Instance**
> 
> 1. **Using SSH to Connect:**
>     
>     - Copy the SSH command from the instructions.
>     - Use the copied command to connect to the client instance.
> 2. **Successful Connection:**
>     
>     - Confirm successful SSH connection to the client instance.
> 
> **Part 8: Troubleshooting and FAQs**
> 
> 1. **Common Issues:**
>     - Verify file creation and key content.
>     - Use pseudo (sudo) for necessary commands.
>     - Check file permissions and ownership.
> 
> **Part 9: Conclusion and Termination**
> 
> 1. **Terminating Instances:**
>     - Use the EC2 Dashboard to terminate instances.
> 
> Thank you for attending the live lecture on AWS EC2 instance setup. If you have further questions or need assistance, feel free to reach out.

^a2edcb
