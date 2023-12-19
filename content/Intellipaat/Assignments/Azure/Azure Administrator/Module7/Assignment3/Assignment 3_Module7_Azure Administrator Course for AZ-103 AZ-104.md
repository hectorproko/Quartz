> [!info] Module 7: Assignment - 3
> **Tasks To Be Performed:** 
> 1. For the two VMs deployed previously configure DNS for the public IPs of the VM

[[Assignment 5_Module6_Azure Administrator Course for AZ-103 AZ-104]]


### Step 1: Configure DNS Name for the Public IP of VM1

1. **I Go to the Public IP Resource**:
    
    - In the Azure Portal, I navigate to the "Public IP addresses" section.
    - I locate the public IP resource associated with VM1.
2. **I Configure the DNS Name**:
    
    - I select the public IP resource to open its properties.
    - In the "Configuration" settings, I find the "DNS name label" section.
    - I enter a unique DNS name label for VM1. This label, combined with the location's DNS suffix, will form the fully qualified DNS name. For example, if I enter `myvm1`, the full DNS name will be `myvm1.<region>.cloudapp.azure.com`.
      ![[Pasted image 20231209221930.png]]
      
      `thisisvm1.eastus.cloudapp.azure.com`
      
3. **I Save the Configuration**:
    
    - I save the changes to apply the DNS name label to the public IP.

### Step 2: Configure DNS Name for the Public IP of VM2

1. **I Repeat the Process for VM2**:
    - Similarly, I find the public IP resource for VM2.
    - In the configuration settings, I set a unique DNS name label for VM2, for example, `myvm2`.
    - I save the changes to apply the new DNS name.

`thisisvm2.eastus.cloudapp.azure.com`


### Step 3: Test the DNS Configuration

![[Pasted image 20231209222718.png]]
![[Pasted image 20231209222825.png]]