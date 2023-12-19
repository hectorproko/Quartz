---
tags:
  - azure
---
> [!info] Module 8: Assignment - 3
> **Tasks To Be Performed:** 
>  1. Create a user group 
>  2. Attach the role created in Assignment 1 to this group 
>  3. Add new users to this group and check whether the permissions get assigned or not

Continuing [[Assignment 1_Module8_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 8]]

### Step 1: Create a User Group in Azure Active Directory

1. **I Navigate to Groups**:
    
    - I search "Groups" in the search bar.
2. **I Create a New Group**:
    
    - I click "New group".
    - I select the group type, typically "Security" for RBAC purposes.
    - I enter a group name and description.
    - I leave the "Membership type" as "Assigned" to manually add users.
    - I click "Create" to create the group.

### Step 2: Attach the Role to the Group

1. **I Navigate to the Subscription**:
2. **I Open Access Control (IAM)**:
    
    - I select "Access control (IAM)" from the subscription or resource blade.
    - I click on "Add role assignment"
      ![[Pasted image 20231210181841.png]]
    
3. **I Assign the Role to the Group**:
    
    - I select the custom role that I created, for example, "VM Operator".
    - I click "Select members" and search for the group I just created.
      ![[Pasted image 20231210185310.png]]
    - I select the group and then click "Review + assign" to assign the role to the group.

4. **I Check the Role Assignment**:
    - After assigning the role, I navigate to the Access Control (IAM) blade.
    - I use the "Check access" feature to search for the group and confirm that the "VM Operator" role is listed under their assigned roles.

> [!success]
> ![[Pasted image 20231210185520.png]]






### Step 3: Add New Users to the Group

I created two new users, 'user1' and 'user2,' following the same steps as in [[Assignment 2_Module8_Azure Administrator Course for AZ-103 AZ-104|Assignment 2: Module 8]].

1. **I Navigate Back to the Group**:
2. **I Select the Group**:
    
    - I find and select the group I created.
3. **I Add Members to the Group**:
    
    - I click "+ Add members".
    - I search for and select the new users I want to add to the group.
    - I click "Select" to add them as members of the group.
      ![[Pasted image 20231210190828.png]]

### Step 4: Check Whether the Permissions Are Assigned

1. **I Verify the Permissions for a User**:
    - To check if the permissions have been correctly assigned through group membership, I can navigate to "Access control (IAM)" in the subscription or resource group.
    - I use the "Check access" feature, search for a user I added to the group, and verify that they have the permissions associated with the "VM Operator" role.
      ![[Pasted image 20231210191211.png]]
      ![[Pasted image 20231210191235.png]]


%%By completing these steps, you will have created a user group, assigned the custom role to this group, and added users to the group. The users added to this group should now inherit the permissions defined by the custom role, which, in your case, allows viewing, starting, and stopping VMs. Remember, it may take a few minutes for role assignments to propagate and become active.%%