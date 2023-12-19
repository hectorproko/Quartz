> [!info] Module 2: Assignment - 1
> **Tasks To Be Performed:**
> 1. Create 2 resource groups rg-1 and rg-2 
> 2. Add storage account to rg-1 
> 3. Move storage account from rg-1 to rg-2 

%%Same way I started [[Assignment 1_Module1_Azure Administrator Course for AZ-103 AZ-104]]%%

In the Azure Portal I navigate to the "Cloud Shell"  Icon in the upper right corner
![[Pasted image 20231206090119.png]]

### Step 1: Create Two Resource Groups

In the command-line interface and run:
```bash
az group create --name rg-1 --location eastus
az group create --name rg-2 --location eastus
```

Verify:
```bash
az group list -o table
```
![[Pasted image 20231206103718.png]]

### Step 2: Add a Storage Account to `rg-1`
%%I delete the storage created in [[Assignment 1_Module1_Azure Administrator Course for AZ-103 AZ-104]] and it was used to run the Terminal, so closed the terminal

So created a new one automatically again cs21003200105a6a072
%%

I create a new storage account in resource group `rg-1`
```bash
az storage account create --name hectorstorage12345 --resource-group rg-1 --location eastus --sku Standard_LRS
```

Verity:
```bash
az storage account list --resource-group rg-1 --query "[].{Name:name, ResourceGroup:resourceGroup}" -o table
```
![[Pasted image 20231206104926.png]]

### Step 3: Move Storage Account from `rg-1` to `rg-2`

First, I get the resource ID of the storage account by running:
```bash
az storage account show --name hectorstorage12345 --resource-group rg-1 --query id --output tsv
```

The ID is pretty long so I'll store in a variable:
```bash
storageid=$(az storage account show --name hectorstorage12345 --resource-group rg-1 --query id --output tsv)
```

Using variable, I move the storage account to `rg-2` with the following.
```bash
az resource move --destination-group rg-2 --ids $storageid
```

![[Pasted image 20231206105929.png]]

### Verity:
The following command confirms storage account no longer in `rg-1`
```bash
az storage account list --resource-group rg-1 --query "[].{Name:name, ResourceGroup:resourceGroup}" -o table
```
The following confirms it is located in `rg-2`
```bash
az storage account list --resource-group rg-2 --query "[].{Name:name, ResourceGroup:resourceGroup}" -o table
```
![[Pasted image 20231206110516.png]]