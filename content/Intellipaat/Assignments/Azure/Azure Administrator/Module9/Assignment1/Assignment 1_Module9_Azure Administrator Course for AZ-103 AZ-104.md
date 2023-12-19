---
tags:
  - azure
---
> [!info] Module 9: Assignment - 1
> **Tasks To Be Performed:** 
> 1. Create a Linux VM and install Apache2 on it 
> 2. Create Recovery Services vault 
> 3. Take backup of the VM deployed


### Step 1: Linux VM wiht Apache2

To create the VM, I follow the steps outlined in [[Assignment 1_Module4_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 4]] and run the following:

![[Install Apache]]



### Step 2: Create Recovery Services Vault

2. **I Create the Recovery Services Vault**:
    
    - I search for "Recovery Services vault".
    - I click "Create".
    - I fill in the details for the Recovery Services vault, such as the name, subscription, resource group (I use the same resource group as my VM for convenience), and region (the same region as my VM).
    - I review the settings and click "Create" to provision the vault.
      ![[Pasted image 20231212152614.png]]

### Step 3: Take Backup of the VM Deployed

1. **I Navigate to the Newly Created Recovery Services Vault**:
    
    - After the vault is created, I go to the "Recovery Services vaults" section in the portal and open the vault I just created.
      ![[Pasted image 20231212153111.png]]
2. **I Set Up Backup**:
    
    - Inside the Recovery Services vault, I click "+Backup".
    - I select "Azure Virtual Machine" as the workload running in Azure.
    - I click "Backup" to configure and enable backup for the VM.
      ![[Pasted image 20231212153227.png]]
3. **Configure Backup**:
    
    - "Policy sub type" I select "Enhanced" as it covers VMs
    - I then add the VM I want to backup
      ![[Pasted image 20231212153757.png]]
1. **I Enable Backup**:
    
    - Once I've configured the backup settings, I click "Enable Backup".
    - Azure will schedule the backup job based on the policy I've defined.


%%Linkedin
By completing these steps, I will have successfully created a Recovery Services vault and set up a backup for my Linux VM with Apache2 installed. The VM's data will be backed up according to the schedule and retention policy I've configured.%%