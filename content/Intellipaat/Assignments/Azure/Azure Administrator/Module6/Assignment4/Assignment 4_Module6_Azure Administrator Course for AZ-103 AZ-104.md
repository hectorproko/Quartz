---
tags:
  - azure
---
> [!info] Module 6: Assignment - 4
> **Tasks To Be Performed:** 
> 1. Use the previously created Linux VM 
> 2. Install Apache2 on this VM 
> 3. Create a Network Security Group to the subnet in which VM has been deployed 
> 4. Open NSG rules for subnet and VM on port 80 
> 5. Verify if you can see the Apache2 page

### Step 1: Previous VM

SSH into "StaticIPVM" from [[Assignment 3_Module6_Azure Administrator Course for AZ-103 AZ-104|Assignment 3: Module 6]]
<br>![[staticipvm overview.png]]
### Step 2: Install Apache

```bash
sudo apt-get update
sudo apt-get install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

Verifying locally using the command `lynx localhost`
<br>![[Pasted image 20231208124906.png]]

However, it doesn't work over the internet because port 80 is not open.
<br>![[Pasted image 20231208124956.png]]



### Step 3: Create a Network Security Group (NSG) for the Subnet

1. **I Navigate to Network Security Groups in Azure Portal**:
    
    - In the Azure Portal, I go to "Network Security Groups" and click "Create" to create a new NSG.
2. **I Create the NSG**:
    
    - I fill in the details for the NSG, such as name, subscription, resource group, and the location that matches my VM's location.
    - I click "Create" to provision the NSG.
      <br>![[Pasted image 20231208130317.png]]

### Step 4: Open NSG Rules for Subnet and VM on Port 80

1. **I Configure the NSG Rule for Port 80**:
    
    - After the NSG is created, I go to its settings and click on "Inbound security rules".
    - I click "Add" to create a new rule.
    - I set the following:
        - Source: Any
        - Source port ranges: *
        - Destination: Any
        - Destination port ranges: 80
        - Protocol: TCP
        - Action: Allow
        - Priority: Default Value
        - Name: AllowHTTP
    - I save the rule.
2. **I Associate the NSG with the VM's Subnet**:
    
    -  Withing the newly created NSG I navigate to "Settings > Subnet" and click "+ Associate".
    - I select the Virtual Network where VM is and the subnet.
      <br>![[Pasted image 20231208141252.png]]
    - Click "OK"
      <br>![[Pasted image 20231208141909.png]]
      Since my VM resides in the subnet I applied the NSG, it inherits the NSG. In the VMs "Settings > Networking" I see an addition security group added vi subnet
      <br>![[Pasted image 20231208144001.png]]
      

> [!attention]
> We have now opened port 80 within the subnet. However, to access it from the internet, we need to open port 80 directly on the NIC associated with the public IP we are using.


%%Issue Still cant access the site:
I have 2 nsg attached to the VM now
its default has 22 open
subnet has 80 open
but the default nsg seems to be interfering with the subnet one. Because I opened http in the default nsg and works. But when i remove it is like it doesnt reach the second nsg which opens http
<br>![[Pasted image 20231208145332.png]]
It works not but not sure why, because when it [[Pasted image 20231208144001.png|was like]] this it kept on failiding, then the screen change to the above and the only difference i see is the order in which the nsg appears%%

### Step 5: Verify the Apache2 Page
- After opening Port 80 in NIC
- I use a web browser to navigate to `http://<VM-public-IP>`
<br>![[20.14.87.3 browser test.png]]





%%

---

In Networking > Netwok settings
I can now see again
<br>![[Pasted image 20231208144001.png]]
and i can not even ssh to machine

Original first one has ssh
Second has http

after adding ssh open like so, in the second one, i can ssh but I can not HTTP
<br>![[Pasted image 20231208163647.png]]

letst add http ot the first nsg


---
Subnet SEcuirty group applies to private IPs?
only works in the networks within subnet or subnets withing that subnet.

If VM has NIC with public IP, it wont apply to it, need to apply NSG to the NIC

<br>![[Untitled.jpg]]

%%