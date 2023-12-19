> [!info] Module 1: Assignment - 4
> **Tasks To Be Performed:** 
> Use Azure CLI and Azure PowerShell to: 
> 1. Delete all the resource groups in West US region using one command

Continuing from [[Assignment 3_Module1_Azure Administrator Course for AZ-103 AZ-104|Assignment 3: Module 1]]

To delete all resource groups in the West US region I use the following command:
```bash
az group list --query "[?location=='westus'].name" -o tsv | xargs -I {} az group delete --name {} --yes --no-wait
```

> `az group list --query "[?location=='westus'].name" -o tsv` lists all resource groups and filters them to only include those in the "West US" region, outputting only their names in a tab-separated values format.
>    ![[Pasted image 20231206095622.png]]
> 
> `xargs -I {} az group delete --name {} --yes --no-wait` takes each name and uses it to run the `az group delete` command, which deletes the resource group. The `--yes` flag bypasses the confirmation prompt, and the `--no-wait` flag makes the command return immediately without waiting for the deletion to complete.

To verify deletion:
```bash
az group list --query "[?location=='westus']" --output table
```

> [!success]
> ![[Pasted image 20231206100730.png]]
