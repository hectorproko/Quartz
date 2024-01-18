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

1. I create a new repository in my GitHub and call [terraform-cloud](https://github.com/hectorproko/terraform-cloud) and push the Terraform codes developed in the [[AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM|previous projects]] to the repository.
   
2. Create a [Terraform Cloud](https://www.terraform.io/cloud) account

3. Create an organization
   Select "Start from scratch", choose a name for your organization and create it.
   ![[welcome.png]]
   ![[organization.png]]

3. Configure a workspace
   
   We will use a `version control workflow`, which is the most common and recommended way to run Terraform commands triggered from our Git repository.
   
   ![[workspace.png]]
   
   We will be prompted to connect our GitHub account to our workspace – I follow the prompt and add our newly created repository [terraform-cloud](https://github.com/hectorproko/terraform-cloud)  to the workspace.
   ![[workspace2.png]]
   
   
   ![[permission.png|300]]  
   ![[install.png|300]]  

  ![[cloud.png|600]]

4. Configure variables
   Terraform Cloud supports two types of variables: environment variables and Terraform variables. Either type can be marked as sensitive, which prevents them from being displayed in the Terraform Cloud web UI and makes them write-only.
   
   I'll select Environment variable  

   I set two environment variables: `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, using the same values as in [[PART1_PROJECT_16]] . These credentials will be used to provision the AWS infrastructure by Terraform Cloud.
   
   ![[variables.png|200]]

  After we set these 2 environment variables – Terraform Cloud is all set to apply the codes from GitHub and create all the necessary AWS resources.

  The Workspace name, `terraform-cloud` was assigned automatically based on the repo name

  ![[workspaces.png]]

5. Now it is time to run our Terraform scripts. I run `terraform plan` and `terraform apply` from web console
   ![[terraform_cloud_apply.gif]]
   
   ![[created.png]]  

Then I run `terraform destroy` to bring down the infrastructure
![[terraform_cloud_destroyed.gif]]

![[triggered.png|300]]

So far I triggered the provisioning via UI. But since we have an integration with GitHub, the process can be triggered automatically.

I'll change something in the README and look at "Runs" tab again – plan must be launched automatically, but to apply I still need to approve manually. 

> Since provisioning of new Cloud resources might incur significant costs. Even though we can configure "Auto apply", it is always a good idea to verify the plan results before pushing it to apply to avoid any misconfigurations that can cause ‘bill shock’.

![[terraform_cloud_autoPlanning.gif]]




