---
tags:
  - azure
---
> [!info] Module 9: Assignment - 3
> **Tasks To Be Performed:** 
> 1. Use the previous VM deployment 
> 2. Create an alert for the deletion of the above VM

### Task 1: Use the Previous VM Deployment
Using VM from [[Assignment 1_Module9_Azure Administrator Course for AZ-103 AZ-104|Assignment 1: Module 9]]

### Task 2: Create an Alert for the Deletion of the VM

I search "Alerts"
Click "+ Create" and select "Alert Rule"

I selected my VM as the scope.
<br>![[Pasted image 20231214103540.png]]

As for the condition, I configured it to detect a signal for the deletion of the VM.
<br>![[Pasted image 20231214104216.png]]

For the 'Actions' section, I created an action group with 'Notifications' set to an email address.
<br>![[Pasted image 20231214104119.png]]

I reviewed the settings and clicked on 'Create.'
<br>![[Pasted image 20231214104404.png]]
To test the alert, I deleted the VM by clicking the 'Delete' button.
<br>![[Pasted image 20231214111937.png]]

Upon checking the alerts, I observed the notifications, and in my mailbox, I received corresponding emails. I received multiple notifications because I clicked 'Delete' several times.

> [!success]
> <br>![[Pasted image 20231214113513.png]]
> <br>![[Pasted image 20231214113933.png]]