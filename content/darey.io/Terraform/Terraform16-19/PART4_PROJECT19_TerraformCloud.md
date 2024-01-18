---
tags:
  - "#Terraform"
  - IaC
title: Automating Infrastructure with IAC Using Terraform Cloud
---
<!--# AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM-PART4 -->


**Introduction**

[Terraform Cloud](https://www.terraform.io/cloud) is a managed service that provides you with Terraform CLI to provision infrastructure, either on demand or in response to various events.

By default, Terraform CLI performs operation on the server whenever it is invoked, it is perfectly fine if we have a dedicated role who can launch it, but if we have a team working with Terraform – we need a consistent remote environment with remote workflow and shared state to run Terraform commands.

Terraform Cloud executes Terraform commands on disposable virtual machines, this remote execution is also called [remote operations](https://www.terraform.io/docs/cloud/run/index.html).


### Migrate .tf codes to Terraform Cloud

1. I create a new repository in my GitHub and call [terraform-cloud]([GitHub - hectorproko/terraform-cloud: Used by Project 19](https://github.com/hectorproko/terraform-cloud)) and push the Terraform codes developed in the [[AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM|previous projects]] to the repository.
   
2. Create a [Terraform Cloud](https://www.terraform.io/cloud) account

3. Create an organization
   Select "Start from scratch", choose a name for your organization and create it.
   ![[welcome.png]]
   ![[organization.png]]

3. Configure a workspace
   
   We will use a `version control workflow`, which is the most common and recommended way to run Terraform commands triggered from our Git repository.
   
   ![[workspace.png]]
   
   We will be prompted to connect our GitHub account to our workspace – I follow the prompt and add our newly created repository [terraform-cloud]([GitHub - hectorproko/terraform-cloud: Used by Project 19](https://github.com/hectorproko/terraform-cloud))  to the workspace.
   ![[workspace2.png]]
   
   
   ![[permission.png|300]]
   ![[install.png|300]]

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




