> [!info] Module 7: Assignment - 4
> **Tasks To Be Performed:** 
> 1. Deploy 2 VMs in different regions 
> 2. Balance the load on these VMs geographically 
> 
> To accomplish this please use Azure Traffic Manager

### Step1: VMs
To create the 2 VMs I follow steps in [[Assignment 1_Module4_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 4]] making sure to use different regions
![[Pasted image 20231210123006.png]]

I opened port 80 (HTTP) and installed Apache.

![[Install Apache]]

I tested the Apache service on both VMs using their respective Public IPs directly.

> [!success] 
> ![[Pasted image 20231210124037.png]]
> ![[Pasted image 20231210124045.png]]
> 

### Step 2: Set Up [[Azure Traffic Manager|Traffic Manager]]

1. **I Navigate to Traffic Manager Profiles**:
    
    - In the Azure Portal, I search for "Traffic Manager profile" and click "+Create".
2. **I Configure the Profile**:
    
    - I fill in the details for the profile, like the name and resource group.
    - For the routing method, I select "Geographic" to ensure traffic is routed based on the geographic location of the DNS queries.
3. **I Create the Profile**:
    
    - I review the settings and create the Traffic Manager profile.
      ![[traffic manager profile.png]]
      ![[traffic manager profile2.png]]

### Step 3: Add Endpoints

1. **I Add VMs as Endpoints**:
    - Within the Traffic Manager profile, I click on "Endpoints" and then "Add" to configure my VMs as endpoints.
    - I enter the details for each endpoint, including the name, target resource type, target resource, and the geographic location it serves.
      ![[Pasted image 20231210124929.png]]

With second endpoint
![[Pasted image 20231210125139.png]]
fix 
![[Pasted image 20231210125257.png]]

![[Pasted image 20231210125444.png]]

![[Pasted image 20231210130711.png]]

### Step 4: Configure DNS

1. **I Configure DNS Names**:
    - The Traffic Manager profile will have a DNS name, like `http://mytrafficmanagerprofile12345.trafficmanager.net`.
    - I use this DNS name to access my application, and Traffic Manager will route traffic to the appropriate VM endpoint based on the geographic routing method.

### Step 5: Test the Configuration

1. **I Test the Traffic Manager Setup**:
    - I access the Traffic Manager DNS name from different geographic locations to verify that it routes to the closest regional VM.
    - I can use various online tools to simulate requests from different geographic locations to ensure that the geographic routing is functioning as expected.

used localbroswer.com to see how my page looks from another country "Spain" and it redirects to VM in North Europe since is closer to East US
![[Pasted image 20231210130402.png]]

Without simulating my location no matter how many times I refresh my page I get VM in East US cuse I'm located in the US
![[Pasted image 20231210130840.png]]


By following these steps, you will have configured Azure Traffic Manager to balance the load across VMs in different regions based on geography, ensuring users are directed to the VM that is geographically closest to them.