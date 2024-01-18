---
tags:
  - "#Terraform"
  - IaC
---
# AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM-PART-1-4
Project 16-19 Terraform
*==TERRAFORM CLOUD* ==
### AUTOMATE INFRASTRUCTURE WITH IAC USING TERRAFORM. PART 4 - TERRAFORM CLOUD  

Created an account  

Start from scratch  


![[welcome.png]]


![[organization.png]]


![[workspace.png]]


![[workspace2.png]]


![[permission.png]]

Lets created the repo to choose  

![[install.png]]

![[cloud.png]]

![[variables.png]]

Make sure you select Environment variable  

Worspace name is terraform-cloud like the repo name is automatic  



This is how it looks if you navigate back  
![[workspaces.png]]


![[terraform_cloud_apply.gif]]


![[created.png]]  


![[terraform_cloud_destroyed.gif]]


![[triggered.png]]


![[terraform_cloud_autoPlanning.gif]]


Configure 3 branches in your `terraform-cloud` repository for `dev`, `test`, `prod` environments  

Make necessary configuration to trigger runs automatically only for `dev` environment  

Create an Email and Slack notifications for certain events (e.g. started `plan` or errored run) and test it  

Settings > Notifications > Create a Notification  


Create a new Workspace  
	Workspace Name: terraform-cloud-dev  
	Step 4: Configure settings  
	Apply Method: Auto apply  
	VCS branch: dev  
	
Need to create a new run  

