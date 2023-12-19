---
tags:
  - azure
---
> [!info] Module 1: Assignment - 1
> **Tasks To Be Performed:** 
> 1. Connect to Azure Cloud Shell 
> 2. Create a resource group “new-rg” in South Central US region 
> 
> Send the commands along with the screenshots for the completion of this assignment. 


In the Azure Portal I navigate to the "Cloud Shell"  Icon in the upper right corner
<br>![[Pasted image 20231206090119.png]]

It prompts me to create ''Storage account", I click "Create" which results in a new account
<br>![[azure storage account module1 assig1.png]]


Afterwards "Cloud Shell" opens a bash terminal by default (Azure CLI)

In the terminal I run the following command to create resource group:
```bash
az group create --name new-rg --location southcentralus
```
<br>![[Pasted image 20231206092831.png]]

To verify I list the resource groups in that region
```bash
az group list --query "[?location=='southcentralus']" --output table
```

> [!success]
> <br>![[Pasted image 20231206093026.png]]



