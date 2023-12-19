> [!info] Module 1: Assignment - 3
> **Tasks To Be Performed:**
> Use Azure CLI and Azure PowerShell to: 
> 1. Create three more resource groups in a specific region. For example: “West US” 
> 2. List all resource groups in West US

Continuing from [[Assignment 2_Module1_Azure Administrator Course for AZ-103 AZ-104|Assignment  2:_Module1]]

In order to use "Azure CLI" I make sure the terminal is set to "Bash"
![[azure cloud shell powershell bash.png]]

![[Pasted image 20231206094413.png|400]]

To create three new resource groups in the "West US" region, In the command-line interface I enter the following commands:
```bash
az group create --name ResourceGroup1 --location westus
az group create --name ResourceGroup2 --location westus
az group create --name ResourceGroup3 --location westus
```

To list all resource groups in the "West US" region, I use the following command:
```bash
az group list --query "[?location=='westus']" --output table
```

> [!success]
> ![[Pasted image 20231206091725.png]]
