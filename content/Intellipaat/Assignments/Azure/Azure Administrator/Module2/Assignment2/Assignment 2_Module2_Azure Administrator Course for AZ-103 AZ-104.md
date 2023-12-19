==Pending CleanUP==
---
tags:
  - azure
---
> [!info] Module 2: Assignment - 2
> **Tasks To Be Performed:**
> 1. Create 3 storage accounts with “Team” tags: team1, team2 and team3 respectively 
> 2. Create one more storage account for team2 
> 3. List all resources for team2 using tags

Continuing from [[Assignment 1_Module2_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 2]]

In these steps, I'm using `eastus` as the location and `Standard_LRS` as the SKU. I can replace these with different values if needed.

### Step 1: Create 3 Storage Accounts with Team Tags

```bash
az storage account create --name team1storageaccount54321 --resource-group rg-1 --location eastus --sku Standard_LRS --tags Team=team1
az storage account create --name team2storageaccount54321 --resource-group rg-1 --location eastus --sku Standard_LRS --tags Team=team2
az storage account create --name team3storageaccount54321 --resource-group rg-1 --location eastus --sku Standard_LRS --tags Team=team3
```

Verify:
```bash
az storage account list --resource-group rg-1 --query "[].{Name:name, ResourceGroup:resourceGroup}" -o table
```
<br>![[Pasted image 20231206114839.png]]

### Step 2: Create One More Storage Account for Team2

```bash
az storage account create --name team2storageaccount2th --resource-group rg-1 --location eastus --sku Standard_LRS --tags Team=team2
```


### Step 3: List All Resources for Team2 Using Tags
I use the following command to list all resources that have been assigned the tag `Team` with the value `team2`.

```bash
az resource list --tag Team=team2 -o table
```
<br>![[Pasted image 20231206115528.png]]


