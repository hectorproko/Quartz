---
tags:
  - azure
---
> [!info] Azure Administrator Capstone Project Az-104
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

==PENDING CLEANUP==


---


Regions to use "West US 3" and "East US"

1. **[[Set Up Virtual Networks and VM]]s:**
2. **[[Clone the GitHub Repository]]:**
3. **[[Configure VMs]]:**


---

I already have the same Virtual Network

VM1, West
<br>![[Pasted image 20231218170259.png]]
VM2, West
<br>![[Pasted image 20231218170721.png]]

VM1, East
<br>![[Pasted image 20231218171008.png]]

VM2, East
<br>![[Pasted image 20231218171350.png]]

I created the VMs with open HTTPS, HTTP, need to rest it by removing it and applying it as subnet

<br>![[Pasted image 20231218171833.png]]

---
We dont yet have subnet for the app gateway

---

Using "storage account" `hectorstorage12345`

<br>![[Pasted image 20231218172916.png]]
I create container "upload" with blob access

We create error.html file
which i get from https://github.com/azcloudberg/azproject

w3school output
<br>![[Pasted image 20231218173452.png]]


I download it and uploaded to "Static website"
<br>![[Pasted image 20231218174417.png]]
I click Save and i get the endpoints

<br>![[Pasted image 20231218174537.png]]
```bash
https://hectorstorage12345.z1.web.core.windows.net/
```
I click $web

<br>![[Pasted image 20231218175139.png]]

--- 
Creating App Gateways


Lets start with east us

---
ISSUE:
<br>![[WhatsApp Image 2023-12-18 at 19.33.48_180e2bd4.jpg]]

Bypass:
Instead of using `+ Gateway` subnet use `+ Subnet`
Seems like i can use whatever name bu

has something to do with the "availability dependent on dynamic use"
<br>![[Pasted image 20231218202600.png]]

---

### Creating gateways

> "app-gate-west-us"
> <br>![[Pasted image 20231218203526.png]]
> 
> Frontends: 
> I create new Public IP
> <br>![[Pasted image 20231218203502.png]]
> 
> Backend:
> <br>![[Pasted image 20231218203658.png]]
> 
> Configuration:
> <br>![[Pasted image 20231218203753.png]]
> 
> <br>![[Pasted image 20231218174537.png]]
> ```bash
> https://hectorstorage12345.z1.web.core.windows.net/
> ```
> I use the endpoint making sure to add `error.html` at the end
> 
> <br>![[Pasted image 20231218204429.png]]
> 
> Backend targets:
> Pool2 has VM2 which is home page so on top
> 
> 
> Pool1 with VM1 added as a path
> <br>![[Pasted image 20231218205456.png]]
> <br>![[Pasted image 20231218205642.png]]
> 
> <br>![[Pasted image 20231218205938.png]]
> 




"app-gate-east-us"
<br>![[FireShot Capture 116 - Create application gateway - Microsoft Azure - portal.azure.com.png]]

<br>![[Pasted image 20231218210542.png]]

<br>![[Pasted image 20231218210645.png]]

copy from top
<br>![[Pasted image 20231218203753.png]]

copy from top cuse is extaclty the same anyway
<br>![[Pasted image 20231218204429.png]]

The pictures end up the same here also

<br>![[Pasted image 20231218205456.png]]

<br>![[Pasted image 20231218205642.png]]

<br>![[Pasted image 20231218211700.png]]

<br>![[Pasted image 20231218212050.png]]


---
Running the vm1.sh and vm2.sh scripts

I clone https://github.com/azcloudberg/azproject

cd azproject

---
Edit the file `config.py` and replace the key and accout name

<br>![[Pasted image 20231218215826.png]]

```bash
+gUKWA3UnIjAFv1u/xfV4cRNvCGbBS6H1SEVK54X9EPr1vELLpGQm2j3uYb1cefZnY/X5bYwPng/+AStbD71PA==
```


looks like
```
[DEFAULT]
# Account name
account =hectorstorage12345
# Azure Storage account access key
key =XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
# Container name
container =upload
```


the we run app.py
<br>![[Pasted image 20231218220802.png]]

---
I create traffic manager

<br>![[Pasted image 20231218221252.png]]

<br>![[Pasted image 20231218221508.png]]

I go to my Traffic Manager and nagivate to "Endpoints" where I click "+ Add"

Yes the the gateway IP will we asked to ahve DNS
<br>![[Pasted image 20231218222011.png]]
<br>![[Pasted image 20231218222118.png]]

<br>![[Pasted image 20231218222306.png]]

<br>![[Pasted image 20231218222413.png]]


<br>![[Pasted image 20231218222607.png]]

<br>![[Pasted image 20231218222636.png]]


<br>![[Pasted image 20231218222729.png]]

<br>![[Pasted image 20231218222743.png]]

<br>![[Pasted image 20231218223243.png]]

If i navigate to my container `upload` I see the file i just uploaded
<br>![[Pasted image 20231218223459.png]]

Going to remove rules HTTP and HTTPS from all NICs and put them as subnet

After removing all of that and leaving only SSH, it still worked, no need 



Create VNet peering just like in [[Assignment 1_Module6_Azure Administrator Course for AZ-103 AZ-104#Step 5 Create VNet-to-VNet Peering|Assignment 1: Module 6]]

<br>![[FireShot Capture 117 - Add peering - Microsoft Azure - portal.azure.com.png]]

<br>![[Pasted image 20231218225520.png]]


<br>![[Pasted image 20231218225754.png]]
