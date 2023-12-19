---
tags:
  - azure
---
> [!info] Module 8: Assignment - 2
> **Tasks To Be Performed:** 
> 1. Create a new user 
> 2. Assign the previously created user this role\

Continuing [[Assignment 1_Module8_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 8]]

### Step 1: Create a New User in Azure Active Directory

1. **I Navigate to Users**:
    - I search for "Users"
    -  I click on "+ New User".
      ![[Pasted image 20231210180731.png]]
2. **I Create the User**:
    
    - I fill in the required information for the new user, such as name and username.
    - I specify a temporary password that the user will be prompted to change upon first sign-in.
    - I complete the rest of the user information as needed and click "Create" at the bottom of the pane.
      ![[Pasted image 20231210181022.png]]

### Step 2: Assign the Custom Role to the New User

1. **I Navigate to the Subscription**:
    
    - I go to the subscription where the VMs are located.
2. **I Open Access Control (IAM)**:
    
    - I select "Access control (IAM)" to view the role assignments.
      ![[Pasted image 20231210174432.png]]
3. **I Assign the Role**:
    
    - I click on "Add role assignment" to open the role assignment pane.
      ![[Pasted image 20231210181606.png]]
    - I search for the custom role "VM Operator" in the list of roles.
      ![[Pasted image 20231210181841.png]]
    - Once I've found it, I select it and click "Next".
4. **I Select the User**:
    
    - I click "Select members" and search for the new user I just created.
      ![[Pasted image 20231210181938.png]]
    - I select the user and then click "Select".
5. **I Review and Assign**:
    
    - I review the role and member details, and then click "Review + assign" to assign the role to the user.

### Step 3: Confirm the Role Assignment

1. **I Check the Role Assignment**:
    - After assigning the role, I remain on the Access Control (IAM) blade.
    - I use the "Check access" feature to search for the new user and confirm that the "VM Operator" role is listed under their assigned roles.
      ![[Pasted image 20231210182202.png]]

> [!success]
> ![[Pasted image 20231210182343.png]]

%%By completing these steps, you will have successfully created a new user in Azure Active Directory and assigned them the custom role that allows them to view, start, and stop VMs, but not perform any other actions.%%




