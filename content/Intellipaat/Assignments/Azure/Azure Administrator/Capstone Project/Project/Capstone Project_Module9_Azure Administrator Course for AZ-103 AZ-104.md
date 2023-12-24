---
tags:
  - azure
---


> [!info]- Azure Administrator Capstone Project Az-104
> You work as an Azure professional for a Corporation. You are assigned the task of implementing the below architecture for the company’s website. 
> <br>![[Pasted image 20231210204021.png]]
> There are three web pages to be deployed: 
> 1. The home page is the default page (VM2) 
> 2. The upload page is where you can upload the files to your Azure Blob Storage (VM1) 
> 3. The error page for 403 and 502 errors 
> 
> Application Gateway has to be configured in the following manner: 
> 1. Example.com should be pointed to the home page 
> 2. Example.com/upload should be pointed to the upload page
> 3. Application Gateway’s error pages should be pointed to error.html which should be hosted as a static website in Azure Containers. The error.html file is present in the GitHub repository 
> 
> The term ‘Example’ here refers to the Traffic Manager’s domain name. The client wants you to deploy them in the East US and the West US regions such that the traffic is distributed optimally between both regions. 
> 
> Storage Account has to be configured in the following manner: 
> 1. You need to host your error.html as a static website here, and then point the application gateway’s 403 and 502 errors to it. 
> 2. Create a container named upload, this will be used by your code to upload the files. 
> 
> Technical specifications for the deployments are as follows:
> 1. Deployments in both regions should have VMs inside VNets. 
> 2. Clone the GitHub repo https://github.com/azcloudberg/azproject to all the VMs. 
> 3. On VM1, please run vm1.sh this will deploy the upload page, on VM2 please run VM2.sh, this will install the home page. 
> 4. For running the scripts, please run the following command inside the GitHub directory from the terminal.
>    `VM1: ./vm1.sh` 
>    `VM2: ./vm2.sh` 
> 5. After running the scripts, please edit the config.py file on VM1, and enter the details related to your storage account where the files will be uploaded. 
> 6. Once done, please run the following command: `sudo python3 app.py` 
> 7. Both regions should be connected to each other using VNet-VNet Peering. 
> 8. Finally, your Traffic Manager should be pointing to the application gateway of both the regions.

---


%%[[Capstone video notes]]%%

## Creating VNets

Create two Virtual Networks (VNets), one in the East US region (Vnet 1) and one in the West US region (Vnet 2).
  
<br>![[Pasted image 20231214155942.png]]
<br>![[Pasted image 20231214160004.png]]
While creating the VPC, I enable the option to create a Bastion host.
<br>![[Pasted image 20231214150852.png]]

> [!done]
> <br>![[Pasted image 20231214160407.png]]
> 

----
## Creating VMs

In each VNet, deploy two Virtual Machines (VMs) - VM1 and VM2.

West US | East US
-- | -- 
VM1 <br>![[Pasted image 20231218170259.png]] | VM1 <br>![[Pasted image 20231218171008.png]] 
VM2 <br>![[Pasted image 20231218170721.png]] | VM2 <br>![[Pasted image 20231218171350.png]]

%%
I created the VMs with open HTTPS, HTTP, need to rest it by removing it and applying it as subnet

Edited the above "Public inbound ports" to delete HTTPS, HTTP cuse we don't want them to accept connections directly
%%

> [!done]
> <br>![[Pasted image 20231218171833.png]]

%%We dont yet have subnet for the app gateway%%

---
**Using "storage account" `hectorstorage12345`**
- I create a 'upload' container with blob access.
  <br>![[Pasted image 20231218172916.png]]

> [!example] I download [error.html](https://github.com/azcloudberg/azproject/blob/master/error.html) file that renders
> <br>![[Pasted image 20231218173452.png]]

I upload [error.html](https://github.com/azcloudberg/azproject/blob/master/error.html) to "Static website"
<br>![[Pasted image 20231218174417.png]]
I click 'Save' and then receive the endpoints.  


I click `$web`
<br>![[Pasted image 20231218174537.png]]

I make note of the "Primary endpoint"
```bash
https://hectorstorage12345.z1.web.core.windows.net/
```


> [!success]
> <br>![[Pasted image 20231218175139.png]]

---
%%
> [!question]- ISSUE:
> 
> > [!fail]
> > <br>![[WhatsApp Image 2023-12-18 at 19.33.48_180e2bd4.jpg]]
> > 
> 
> Issue has something to do with the "availability dependent on dynamic use"
> <br>![[Pasted image 20231218202600.png]]
> 
> > [!tip]
> > Instead of using `+ Gateway` subnet use `+ Subnet`
> > Seems like i can use whatever name.
> > 

%%

## Creating gateways

### app-gate-west-us


> [!summary]- Basics:
> <br>![[Pasted image 20231218203526.png]]


> [!summary]- Frontends:
> I "Add new" Public IP
> <br>![[Pasted image 20231218203502.png]]
> 


> [!summary]- Backends:
> <br>![[Pasted image 20231218203658.png]]


> [!summary]- Configuration:
> <br>![[Pasted image 20231218203753.png]]
> 
> I use the "Primary endpoint" with `/error.html` at the end
> - Listener
>   <br>![[Pasted image 20231218204429.png]]
> - Backend targets
> 
>    Pool1 is created with VM1 added as a node.
>    <br>![[Pasted image 20231218205456.png]]
> 
>    Pool2 contains VM2, which hosts the home page, positioned at the top.
>    <br>![[Pasted image 20231218205642.png]]


> [!summary]- Review + create
> <br>![[Pasted image 20231218205938.png]]

### app-gate-east-us


> [!summary]- Basics:
> <br>![[FireShot Capture 116 - Create application gateway - Microsoft Azure - portal.azure.com.png]]


> [!summary]- Frontends:
> I "Add new" Public IP
<br>![[Pasted image 20231218210542.png]]


> [!summary]- Backends:
<br>![[Pasted image 20231218210645.png]]


> [!summary]- Configuration:
> <br>![[Pasted image 20231218203753.png]]
> 
> I use the "Primary endpoint" with `/error.html` at the end
> - Listener
>   <br>![[Pasted image 20231218204429.png]]
> - Backend targets
> 
>   Pool1 is created with VM1 added as a node.
>   <br>![[Pasted image 20231218205456.png]]
> 
>   Pool2 contains VM2, which hosts the home page, positioned at the top.
>   <br>![[Pasted image 20231218205642.png]]


> [!summary]- Review + create
> <br>![[Pasted image 20231218211700.png]]


> [!done] Gateways
> <br>![[Pasted image 20231218212050.png]]


---
## Configure VMs

%%
Running the vm1.sh and vm2.sh scripts
 - On both VM1 and VM2 in each region, clone the repository `https://github.com/azcloudberg/azproject`.

- On VM1, run the script `vm1.sh` from the cloned GitHub directory to deploy the upload page.
    - On VM2, run the script `VM2.sh` to install the home page.
    - On VM1, edit the `config.py` file to include the details of your storage account where the files will be uploaded.
    - After configuration, execute `sudo python3 app.py` on VM1.

[[app.py]]
[[config.py]] 
[vm1.sh](https://github.com/hectorproko/azproject/blob/master/vm1.sh)
[wm2.sh](https://github.com/hectorproko/azproject/blob/master/vm2.sh)
%%

### VM1

> [!attention] Prerequisite: before running [vm1.sh](https://github.com/hectorproko/azproject/blob/master/vm1.sh)
> ```bash
> sudo apt remove python3-blinker -y
> sudo apt autoremove -y
> ```


I run the script [vm1.sh](https://github.com/hectorproko/azproject/blob/master/vm1.sh)
```bash
git clone https://github.com/hectorproko/azproject.git
cd azproject
bash vm1.sh
```


Inside my local repo `azproject` I edit file `config.py`
```bash
[DEFAULT]
# Account name
account =accountname
# Azure Storage account access key
key =storageaccountkey
# Container name
container =upload
```

I replace account name and key with the following commands:
```bash
sed -i "s|accountname|hectorstorage12345|" config.py
sed -i "s|storageaccountkey|*********|" config.py
```
`*********` represents my storage account key

<br>![[Pasted image 20231215092722.png]]

I execute the Flask application [[app.py]]:
```bash
sudo python3 app.py
```

<br>![[Pasted image 20231218220802.png]]
<br>![[Pasted image 20231215095439.png]]

%%Seems like like picked one of the VMs public IP to test
<br>![[Pasted image 20231215095800.png]]%%
%%after opening port 80 in NIC%%
### VM2
I run the script [vm2.sh](https://github.com/hectorproko/azproject/blob/master/vm2.sh) 
```bash
git clone https://github.com/azcloudberg/azproject
cd azproject
bash vm2.sh
```


---
## I create traffic manager

<br>![[Pasted image 20231218221252.png]]

<br>![[Pasted image 20231218221508.png]]


## Traffic Manager Endpoints
I go to my Traffic Manager and navigate to "Endpoints" where I click "+ Add"

At some point, the public IP of the gateway will need to be assigned a DNS name.
<br>![[Pasted image 20231218222011.png]]
<br>![[Pasted image 20231218222118.png]]

<br>![[Pasted image 20231218222306.png]] | <br>![[Pasted image 20231218222413.png]]
-- | -- 


Traffic Manager with endpoints I make note of the "DNS name"
<br>![[Pasted image 20231218222636.png]]

## Verify
I use the "DNS name" from above
<br>![[Pasted image 20231218222729.png]]
I test the path `/upload`
<br>![[Pasted image 20231218222743.png]]

I upload a file and click "Upload" button
<br>![[Pasted image 20231218223243.png]]

If I navigate to my `upload` container, I see the file I just uploaded.

> [!success]
> <br>![[Pasted image 20231218223459.png]]

%%
> [!attention]
> I remove the HTTP and HTTPS rules from all NICs and instead apply them at the subnet level. 
> 
> "After removing all those rules and leaving only SSH, everything still worked fine" - I think here I meant that there was no need for subnet level

%%
## Create VNet peering 

I follow the same steps as in [[Assignment 1_Module6_Azure Administrator Course for AZ-103 AZ-104#Step 5 Create VNet-to-VNet Peering|Assignment 1: Module 6]]

<br>![[FireShot Capture 117 - Add peering - Microsoft Azure - portal.azure.com.png]]

<br>![[Pasted image 20231218225520.png]]


> [!success]
> I ping each VM in different regions to each other.
> <br>![[Pasted image 20231218225754.png]]
