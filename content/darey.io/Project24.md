---
tags:
  - Kubernetes
  - "#helm"
title:
---

*==Pending Migration from Link==*
[Project 24](https://github.com/hectorproko/BUILDING-ELASTIC-KUBERNETES-SERVICE-EKS-WITH-TERRAFORM)

# BUILDING ELASTIC KUBERNETES SERVICE (EKS) WITH TERRAFORM

[https://github.com/hectorproko/AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM-PART-1-to-4/blob/main/PART3_PROJECT_18.md#add-s3-and-dynamodb-resource-blocks-before-deleting-the-local-state-file-1](https://github.com/hectorproko/AUTOMATE-INFRASTRUCTURE-WITH-IAC-USING-TERRAFORM-PART-1-to-4/blob/main/PART3_PROJECT_18.md#add-s3-and-dynamodb-resource-blocks-before-deleting-the-local-state-file-1)

1. Open up a new directory on your laptop, and name it eks
2. Use AWS
3.  CLI to create an S3 bucket

4. Create a file – backend.tf Task for you, ensure the backend is configured for remote state in S3

```
#Terraform expects that both S3 bucket and DynamoDB resources are already created before we configure the backend. So, let us run terraform apply to provision resources.

#Configure S3 Backend

terraform {

  backend "s3" {

    bucket         = "hector-dev-terraform-bucket"

    key            = "global/s3/terraform.tfstate"

    region         = "us-east-1"

    dynamodb_table = "terraform-locks"

    encrypt        = true

  }

}
```

So first Im going to do a first terraform init without the backend so I can have everything ready for the s3, dynamo for the backned

```
hector@hector-Laptop:~/Project24/eks$ tree
.
├── backend.tfX  renamed to exclude
├── main.tf
└── providers.tf
0 directories, 3 files
```

```
hector@hector-Laptop:~/Project24/eks$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 4.0"...
- Installing hashicorp/aws v4.26.0...
- Installed hashicorp/aws v4.26.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
hector@hector-Laptop:~/Project24/eks$ 
```


==terraform apply (we needed a variables fiel with region variable)==

Part of the Output:
```
…
…
…
Plan: 4 to add, 0 to change, 0 to destroy.
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_dynamodb_table.terraform_locks: Creating...
aws_s3_bucket.terraform-state: Creating...
aws_s3_bucket.terraform-state: Creation complete after 2s [id=hector-dev-terraform-bucket]
aws_s3_bucket_versioning.version: Creating...
aws_s3_bucket_server_side_encryption_configuration.first: Creating...
aws_s3_bucket_server_side_encryption_configuration.first: Creation complete after 0s [id=hector-dev-terraform-bucket]
aws_s3_bucket_versioning.version: Creation complete after 1s [id=hector-dev-terraform-bucket]
aws_dynamodb_table.terraform_locks: Still creating... [10s elapsed]
aws_dynamodb_table.terraform_locks: Creation complete after 14s [id=terraform-locks]

Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
hector@hector-Laptop:~/Project24/eks$

```

<mark style="background: #ABF7F7A6;">Doing the backend</mark>

```
hector@hector-Laptop:~/Project24/eks$ mv backend.tfX backend.tf
hector@hector-Laptop:~/Project24/eks$ terraform plan
╷
│ Error: Backend initialization required, please run "terraform init"
│
│ Reason: Initial configuration of the requested backend "s3"
│
│ The "backend" is the interface that Terraform uses to store state,
│ perform operations, etc. If this message is showing up, it means that the
│ Terraform configuration you're using is using a custom configuration for
│ the Terraform backend.
│
│ Changes to backend configurations require reinitialization. This allows
│ Terraform to set up the new configuration, copy existing state, etc. Please run
│ "terraform init" with either the "-reconfigure" or "-migrate-state" flags to
│ use the current configuration.
│
│ If the change reason above is incorrect, please verify your configuration
│ hasn't changed and try again. At this point, no changes to your existing
│ configuration or state have been made.
```

```
hector@hector-Laptop:~/Project24/eks$ terraform init

Initializing the backend...
Do you want to copy existing state to the new backend?
  Pre-existing state was found while migrating the previous "local" backend to the
  newly configured "s3" backend. No existing state was found in the newly
  configured "s3" backend. Do you want to copy this state to the new "s3"
  backend? Enter "yes" to copy and "no" to start with an empty state.

  Enter a value: yes

Releasing state lock. This may take a few moments...

Successfully configured the backend "s3"! Terraform will automatically
use this backend unless the backend configuration changes.

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v4.26.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
hector@hector-Laptop:~/Project24/eks$
```

Create a file – [network.tf](https://github.com/hectorproko/BUILDING-ELASTIC-KUBERNETES-SERVICE-EKS-WITH-TERRAFORM/blob/main/eks/network.tf) and provision Elastic IP for Nat Gateway, VPC, Private and public subnets.

# BUILDING ELASTIC KUBERNETES SERVICE (EKS) WITH TERRAFORM – PART 2

