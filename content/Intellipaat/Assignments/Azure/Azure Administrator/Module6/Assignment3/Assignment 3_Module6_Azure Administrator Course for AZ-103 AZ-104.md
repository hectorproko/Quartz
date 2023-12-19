> [!info] Module 6: Assignment - 3
>  **Tasks To Be Performed:** 
> 1. Use the previously created VM 
> 2. Created a NIC 
> 3. Attach NIC to the previously created VM


### Step 1: Previous VM
Using `StaticIPVM` from [[Assignment 2_Module6_Azure Administrator Course for AZ-103 AZ-104|Assignment 2_Module 6]]
![[staticipvm overview.png]]

### Step 2: Create a Network Interface Card (NIC)

2. **I Navigate to 'Network Interfaces'**:
    
    - In the Azure Portal, I search for "Network Interface", and select it.
3. **I Create the NIC**:
    
    - I click "Create" to start the process of creating a new NIC.
    - I fill in the necessary information like the name for the NIC, subscription, resource group (using the same one as the VM), and Region (which should match the VM's location).
    - I select the Virtual Network and Subnet where my existing VM resides.
    - I review all the settings and click "Create" to provision the new NIC.
      ![[Pasted image 20231208121618.png]]

### Step 3: Attach NIC to the Previously Created VM

1. **I Stop the VM**:
    
    - Before attaching the NIC, I ensure that the VM is stopped. I go to the VM's overview page in the Azure Portal and click "Stop".
2. **I Attach the NIC to the VM**:
    
    - Once the VM is stopped, I navigate to the VM's settings and select "Networking" - "Network settings".
      %%
      Dont add to this picture it is shared on another note
      %%
      ![[Pasted image 20231208115551.png]]
    - I click "Attach network interface" and select the NIC I just created.
      ![[Pasted image 20231208123149.png]]
      
    - I click "Ok" to attach the NIC to the VM.
3. **Verify the NIC Attachment**.

> [!success]
>    ![[Pasted image 20231208123339.png]]



%%
Linkedin
By following these steps, you will have successfully created a new Network Interface Card and attached it to your existing VM in Azure. This allows your VM to have multiple network interfaces for different networking purposes, such as segregating traffic or connecting to different networks.%%