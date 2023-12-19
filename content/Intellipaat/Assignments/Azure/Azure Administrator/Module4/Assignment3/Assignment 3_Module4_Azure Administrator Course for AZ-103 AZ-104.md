==Pending CleanUP==
---
tags:
  - azure
---
> [!info] Module 4: Assignment - 3
> **Tasks To Be Performed:** 
> 1. Create a VM scale set with Ubuntu as OS 
> 2. Give min VM’s as 1 and maximum as 5 
> 3. For scale-out CPU % is 75 and increase by 1 VM 
> 4. For scale-in CPU % is 25 increase by 1 VM

### Step 1: Create a VM Scale Set with Ubuntu OS

1. **I Log into the Azure Portal**:
    
    - I open a web browser and navigate to the [Azure Portal](https://portal.azure.com/). I sign in with my credentials.
2. **I Navigate to VM Scale Sets**:
    
    - In the Azure Portal, I select "Virtual machine scale sets" from the menu or search for it in the search bar.
3. **I Create the VM Scale Set**:
    
    - I click on "Create" to start the process of creating a new VM scale set.
    - In the "Basics" tab, I select the appropriate subscription and resource group (or create a new one if necessary).
    - I enter a name for the scale set.
    - Under "Region", I choose the region where I want to deploy the scale set.
    - For the "Image", I select an Ubuntu Server image.

### Step 2: Configure the VM Scale Set

1. **I Set the Instance Count**:
    
    - In the "Scaling" section, I set the initial instance count to 1, as I want the minimum number of VMs to be 1.
2. **I Configure the VM Size and Settings**:
    
    - I select the VM size according to my requirements.
    - I configure other settings like networking, storage, and monitoring as needed.

### Step 3: Enable and Configure Auto-Scaling

1. **I Enable Auto-Scaling**:
    
    - In the "Scaling" section, I enable the auto-scaling feature.
2. **I Configure Scale-Out Settings**:
    <br>![[Pasted image 20231207115058.png]]
    - I set the "Scale-out" threshold at 75% CPU usage.
    - I specify that the scale-out action should increase the instance count by 1.
    - I ensure the maximum number of VMs is set to 5.
3. **I Configure Scale-In Settings**:
    
    - I set the "Scale-in" threshold at 25% CPU usage.
    - I specify that the scale-in action should decrease the instance count by 1.

 <br>![[Pasted image 20231207120457.png]]

<br>![[Pasted image 20231207120550.png]]

### Step 4: Review and Create the VM Scale Set

1. **I Review the Configuration**:
    
    - I go through the settings to ensure everything is configured correctly for my requirements.
2. **I Create the VM Scale Set**:
    
    - After reviewing, I click "Review + create" to deploy the VM scale set.
    - I make sure to download key
      <br>![[generate new  key pair download.png]]



<br>![[Pasted image 20231207123748.png]]
I login to it to stress it
%%I edited this picture. I copied one of the VMs from the pic [[Pasted image 20231207131432.png|underneath]]. Cuse i was expecting to see the original VM next to the newly created VM from scaleet, not the case, I think this was due to repeating the steps and mixing the pics with new and old, fingers cross #%%

<br>![[create virtual machine scale set.png]]
In networking tab had to edit the NIC to allow inboud SSH

<br>![[Pasted image 20231207123507.png]]

To simulate high CPU usage in the EC2 instances, I mirrored the approach from [[Assignment 4 – CloudWatch Dashboard_Module3_AWS Weekday BC = 2301080808|Assignment 4 – CloudWatch Dashboard]] . Specifically, I executed the command: 
```bash
while true; do openssl dgst -sha256 /dev/zero; done
```

Before:
<br>![[Pasted image 20231207124310.png]]
After:
<br>![[Pasted image 20231207124722.png]]

More Vm span, not sure why 2 more
<br>![[Pasted image 20231207131432.png]]


In the scaletset's monitoring tab I see the CPU spike I created
<br>![[Pasted image 20231207131743.png]]