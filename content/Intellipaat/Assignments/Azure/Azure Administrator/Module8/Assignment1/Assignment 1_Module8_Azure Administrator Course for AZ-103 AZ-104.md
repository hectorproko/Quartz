---
tags:
  - azure
---
> [!info] Module 8: Assignment - 1
> **Tasks To Be Performed:** 
> 1. Create a custom role which can view, start and stop VMs 
> 2. But should not be able to do anything else

%%[[Azure Access Management]]%%


### Step 1: Define the Custom Role

1. **I Open Azure Cloud Shell**:

2. **I Create a JSON Definition for the Custom Role**:
    
    - I define the role in a JSON file with the necessary permissions. Here’s a sample JSON that allows viewing, starting, and stopping VMs:
		```json
		{
		    "Name": "VM Operator",
		    "Id": null,
		    "IsCustom": true,
		    "Description": "Can view, start, and stop virtual machines.",
		    "Actions": [
		        "Microsoft.Compute/virtualMachines/start/action",
		        "Microsoft.Compute/virtualMachines/deallocate/action",
		        "Microsoft.Compute/virtualMachines/read",
		        "Microsoft.Compute/virtualMachines/instanceView/read"
		    ],
		    "NotActions": [],
		    "AssignableScopes": ["/subscriptions/SUBSCRIPTION_ID"]
		}
		```
    - I replace `SUBSCRIPTION_ID` with my actual subscription ID. %%`37c43e3f-51ba-4c33-ba98-e70251afe450`%%

3. **I Save the JSON Definition**:

  - I save the JSON content to a file named `vm-operator-role.json`.


### Step 2: Create the Custom Role Using Azure Cloud Shell

1. **I Run the az Command to Create the Role**:
    
    - I run the following command to create the new role:
		```bash
		az role definition create --role-definition ./vm-operator-role.json
		```

### Verify
Go to Subscriptions > Access control (IAM) > Roles

> [!success]
> <br>![[Pasted image 20231210174432.png]]


%%By completing these steps, you will have successfully created a custom role that has the specific permissions to view, start, and stop VMs in Azure. This role will not grant any additional permissions beyond those explicitly defined.
%%

