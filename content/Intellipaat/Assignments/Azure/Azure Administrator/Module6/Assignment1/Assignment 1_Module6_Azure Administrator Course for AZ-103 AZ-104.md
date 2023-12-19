---
tags:
  - azure
---
> [!info] Module 6: Assignment - 1
> **Tasks To Be Performed:** 
> 1. Create a virtual network in West US 
> 2. Create another virtual network in South India 
> 3. Deploy virtual machine in West US with the virtual network in West US 
> 4. Deploy virtual machine in South India inside virtual network in South India 
> 5. Create VNet-VNet peering to connect West US and South India VM 
> 6. Check this by pinging VM1 to VM2 via ping command using private IP address

### Step 1: Create a Virtual Network in West US

1. **I Log into the Azure Portal**:
    
    - I open a web browser and navigate to the [Azure Portal](https://portal.azure.com/). I sign in with my credentials.
2. **I Create the West US Virtual Network**:
    
    - In the Azure Portal, I search "Virtual Network" click "+ Create".
    - I fill in the details, setting the "Name" and choosing "West US" as the "Region".
    - I specify the address space and subnet details.
    - I review and create the virtual network.
      ![[Pasted image 20231208102601.png]]
    
%%Originally was West US 2, created new one, this pic was edited to show 3 instead of 2

> [!tip]
> The resource group affects the region you can choose

> [!attention]
> Re-did everything with a resource group based on region

%%
### Step 2: Create Another Virtual Network in South India

1. **I Repeat the Creation Process for South India**:
    - Similarly, I create another virtual network, this time choosing "South India" as the region.
    - I ensure that the address space does not overlap with the West US virtual network.
      ![[Pasted image 20231207203055.png]]
      ![[Pasted image 20231208102917.png]]


### Step 3: Deploy a VM in West US within the West US Virtual Network

1. **I Create a VM in the West US Virtual Network**:
    - Using [[Assignment 1_Module4_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 4]] as reference.
    - I make sure to pick "West US" region and the virtual network I just created.

### Step 4: Deploy a VM in South India within the South India Virtual Network

1. **I Create a VM in the South India Virtual Network**:
    - I follow the same steps to create another VM, this time in the South India region and associated with the South India virtual network.

![[Pasted image 20231208105100.png]]

I'll SSH into the SouthIndiaVM and attempt to ping WestUSVM using its private IP, but as expected, it fails.
![[Pasted image 20231208104659.png]]

### Step 5: Create VNet-to-VNet Peering

1. **I Set Up Peering for West US Virtual Network**:
    
    - In the Azure Portal, I go to the West US virtual network and select "Peerings".
    - I click "Add" and fill in the details to create a peering connection to the South India virtual network.
      ![[Vnetpeering add.png]]
      ![[Pasted image 20231208112613.png]]
2. **I Set Up Peering for South India Virtual Network**:
    
    - Similarly, I set up peering from the South India virtual network to the West US virtual network.
      ![[Pasted image 20231208112530.png]]


### Step 6: Verify Connectivity with Ping Using Private IP Addresses

1. **Ping Each VM from the Other**:
- From the West US VM, I successfully ping the South India VM.
- From the South India VM, I successfully ping the West US VM.

> [!success]
> ![[Pasted image 20231208110909.png]]


%%
> [!question]- Question on why create 2 connections if with one both VMs were able to ping each other
> In Azure, VNet peering connections are bi-directional, but they must be explicitly created in both VNets to establish a successful peering relationship. When you create a peering from West US VNet to the South India VNet, you've only established one half of the peering. For the peering to be fully functional, you need to create a corresponding peering from the South India VNet back to the West US VNet.

Went ahead to created the second peering in the other VNet already had it, cant remember doing it myself, not sure if it was automatically

%%


%%
For linkedin

By completing these steps, you have created two virtual networks in different regions, deployed VMs within each network, established VNet-to-VNet peering, and verified the connectivity using the ping command.
%%