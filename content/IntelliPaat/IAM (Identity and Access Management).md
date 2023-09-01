Identity and Access Management

User groups
Users
Roles


  
IAM (Identity and Access Management) and IAM roles are closely related but serve different purposes within the AWS ecosystem.

1. IAM is a web service that helps you securely control access to AWS resources for your users. Using IAM, you can create users, groups, and permissions that allow or deny access to AWS resources. When you create users in IAM, you're usually creating them to represent human users or sometimes applications that need to be able to interact with AWS services.
    
2. IAM roles, on the other hand, are a way to delegate permissions to AWS services to carry out actions on your behalf. Unlike IAM users, roles do not have long-term credentials (password or access keys) associated with them. Instead, when a role is assumed, temporary security credentials are created and used for the duration of the session. This is a more secure way to grant permissions to entities that need to perform actions on your behalf.
    
    A typical use of IAM roles is to assign them to resources (like EC2 instances) to allow those resources to interact with other AWS services (like S3 or DynamoDB). IAM roles can also be assumed by other entities, like other AWS accounts, federated users, or applications, to provide them with temporary access to your resources.
    

In summary, IAM users are primarily for humans or applications needing long-term access to AWS resources, while IAM roles are for enabling short-term access to resources, often from within AWS itself (like from an EC2 instance to an S3 bucket), and for securely delegating permissions to various entities.


# Intellipaat

## Lecture 1 – IAM Introduction

AWS  [[IAM (Identity and Access Management)]] is a web service that helps you securely control access to AWS resources.

You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.


1. **Use of ARN**: ARNs are necessary when specifying policies. You will require this ARN to specify it in the policy.
    
2. **Individual User Permissions**: You can create users in IAM and specify individual permissions for each user.
    
3. **Group-based Permissions**: Instead of giving permissions to individual users, you can create a group and attach permissions to that group. Any user added to that group will inherit those permissions.
    
4. **Efficiency for Large Teams**: For large teams, like a DevOps team with 100 users, it's more efficient to use groups rather than assigning permissions to each user individually.
    
5. **User and Group Management**: In IAM, you can create users and groups, specify users in those groups, and manage permissions more easily by associating them with groups rather than individual users.


### Lecture 2 - IAM Features

#### IAM Users
- Represents an entity that is created in AWS, can be a person or service.
- No permissions by default. Nothing is allowed.
- Access requirement:
	- Programmatic Access: User needs to make API calls from programs or uses CLI to access AWS resources.
	- Management Console Access: User needs to access AWS resources from management console.

**Access Keys:**
- Access keys are essential for programmatic access to an AWS account.
- They are used for API calls and accessing AWS resources through the Command Line Interface (CLI).
- These keys should be kept secret and secure, similar to how you would handle login credentials.
- AWS will not show existing access keys for security reasons.
- A user can have a maximum of two active access keys at any given time.
- If you need a new access key and already have two, you must delete one of the existing keys to create a new one.

Access keys are vital for automating tasks and integrating AWS services into third-party applications or platforms like Terraform. Just like login credentials, they need to be securely managed to ensure that only authorized users can access the AWS account programmatically.

#### IAM Groups:
- Groups are collection of IAM users
- For organizations with many users, IAM Groups are practical for managing permissions.
- You can place users into groups and then assign permissions to the entire group rather than individual users.

#### Multi-Factor Authentication (MFA):
- For added security, you can enable MFA, which requires two forms of authentication.
- MFA options include a security token-based device, SMS, or an MFA application like Google Authenticator

#### JSON Policies:
- Policies in IAM are written in [[JSON (JavaScript Object Notation)]].
- These policies dictate what actions a user or group can perform on specific AWS services or resources.


### Demo 1 – Users And Groups Creation
#chat #miniProject 
I think best practice is to attach policies to groups not users. So you always create group
> [!summary]
> Certainly! Below are the key steps broken down from the demo on how to create users, create groups, and attach users to a group in the IAM (Identity and Access Management) dashboard of AWS.
> 
> ### Creating Users
> 
> 1. **Open IAM Dashboard**: Navigate to the AWS IAM dashboard.
> 2. **View Existing Users**: Scroll down to see a list of all existing users.
> 3. **Click "Add User"**: To create a new user, click the "Add User" button.
> 4. **Specify Username**: Enter the username you wish to create (e.g., `dev1`).
> 5. **Create Additional Users**: If needed, click on "Add another user" to create more users (`dev2`, `dev3`, etc).
> 6. **Select AWS Access Type**: Choose how the user will access AWS. Options are by password or through programmatic access.
> 7. **Password Selection**: Choose either a custom password ("question password") or an auto-generated password for the user.
> 8. **Password Reset Option**: Decide whether to require the user to reset the password upon first sign-in. Check or uncheck the corresponding box based on your preference.
> 9. **Review and Create**: Review all settings and click "Next" to create the user.
> 
> ### Setting Permissions for Users
> 
> 1. **Navigate to Permissions**: After creating the user, click on "Next: Permissions".
> 2. **Assign Permissions**: You can either copy permissions from an existing user, attach existing policies directly, or attach the user to a group with set permissions.
> 3. **Skip For Now**: In the demo, the presenter skipped this step, leaving the users with no permissions.
> 
> ### Tagging Users (Optional)
> 
> 1. **Click Next for Tags**: If you want to assign tags to better manage users, you can do it at this step.
> 2. **Create User**: Click "Create User" to finalize the process.
> 
> ### Creating Groups
> 
> 1. **Navigate to User Groups**: Click on "User Group" from the IAM Dashboard.
> 2. **Create New Group**: Click on "Create Group".
> 3. **Specify Group Name**: Enter a name for the new group (e.g., `dev1and2group`).
> 4. **Select Users for Group**: Choose which users to attach to the group (`dev1`, `dev2`, etc).
> 5. **Assign Policies to Group (Optional)**: Attach any necessary policies to the group.
> 6. **Create Group**: Click "Create Group" to finalize.
> 
> ### Testing User Access
> 
> 1. **Open Incognito/Private Browser**: Log in as one of the newly created users.
> 2. **Enter Credentials**: Provide the username and password for the user.
> 3. **Verify Limited Access**: In the demo, the user has no permissions, which is confirmed by attempting to perform actions in AWS and encountering errors.
> 
> The demo concludes with a note that the next session will discuss attaching policies to user groups.



### Lecture 3 – Policies And Permissions

- Policies are JSON documents which mention what an user or group can do on AWS resources. It defines the Authorization paradigm for AWS resources.
- Contains 3 components at the least (EAR):
	1. EFFECT: Whether ACTlONS are ALLOWED/DENIED on RESOURCEs.
	2. ACTIONS: What actions are allowed or denied. e.g. create EC2 instance, delete S3 buckets, create Security Groups etc. all are different type of ACTIONS.
	3. RESOURCES: AWS resources like EC2 instances, ELB, S3 buckets or objects etc. Denoted by ARN.
- Policies can be attached to Users or Groups.
- Resource based policies: when policies are attached to resources.
PRINCIPAL: An entity that can take action on an AWS Resource.
```json
Effect, Action,
Resource : "S3"
Principal : "user-I"
```

![[Pasted image 20230822144757.png|450]]


```json
{
  "Version": "2012-10-17", // Version of the policy language
  "Statement": [ // Statement array, containing one or more individual statements
    {
      "Sid": "Stmt1", // Statement ID, optional but useful for identifying the statement
      "Effect": "Allow", // Effect: Specifies "Allow" or "Deny"
      "Principal": { // Principal: Who is allowed or denied
        "AWS": "arn:aws:iam::AccountNumberWithoutHyphens:root" // ARN of the AWS user, account, or service
      },
      "Action": "s3:GetObject", // Action: What specific actions are allowed or denied
      "Resource": "arn:aws:s3:::example-bucket/*", // Resource: On what AWS resources actions can be performed
      "Condition": { // Condition: When the policy is in effect
        "IpAddress": {
          "aws:SourceIp": "192.0.2.0/24" // Example of a condition (here, limiting by source IP)
        }
      }
    }
  ]
}

```



#### Types of IAM Policies

#### 1. AWS Managed Policies
- **Description**: Pre-configured by AWS.
- **Example**: Full administrator access, EC2 full access, DynamoDB full access.
#### 2. Customer Managed Policies
- **Description**: Customized policies created by users.
- **Example**: Policy granting full access to EC2 and EC3.
#### 3. Inline Policies
- **Description**: Directly attached to a single IAM user, group, or role.
- **Characteristics**: Not intended for reuse.

#### IAM Permissions

#### 1. Root Account
- **Default Permission**: Full administrative access.
#### 2. IAM User
- **Default Permission**: No permissions.
- **Assignment**: Permissions must be explicitly assigned.

---

#### IAM Roles and Trust Policies

#### 1. Permission Policies in Roles
- **Purpose**: To grant permissions to users.

#### 2. Trust Policies in Roles
- **Purpose**: To specify conditions for assuming a role.
- **Examples of Use Cases**:
    - Users of the same account with different permissions.
    - IAM users from different accounts.
    - Other AWS services.
    - External users (e.g., for auditing).


### Demo 2 – Attaching Policies To Users And Groups

> [!summary]- Steps 
> ### Step-by-Step Guide
> 
> #### Introduction
> 
> 1. Introduction to the session, explaining that it will cover creating policies and attaching them to users and user groups.
> 
> #### Overview of Users and Groups
> 
> 2. Navigate to the AWS IAM dashboard to show existing users ("one demo," "two demo," "three demo").
> 3. Show existing user groups ("dev 1 and 2 group" containing "dev 2 demo user" and "dev 1 demo user" and another group called "three group" containing "dev 3 demo user").
> 
> #### Create a Custom Policy
> 
> 4. Navigate to the policy creation screen in IAM.
> 5. Select the option to create a customized policy.
> 6. Choose which AWS services the policy should cover (EC2 and S3 in this case).
> 7. For each service, specify what actions are allowed (All actions for both EC2 and S3).
> 8. Define which resources can be accessed (All resources for both EC2 and S3).
> 9. Review the policy settings.
> 10. Name the policy (e.g., "Dev1.Dev2.Policy").
> 11. Optionally, add a description.
> 12. Create the policy by clicking "Create Policy".
> 
> #### Attach Policy to Individual User
> 
> 13. Navigate back to the users list in IAM.
> 14. Go to the details for an individual user (e.g., "Dev1 demo").
> 15. Show that the user currently has no permissions.
> 16. Add permissions to the user by attaching the newly created policy.
> 17. Verify the permissions are correctly applied by refreshing the AWS console and showing that the user can now access allowed services (EC2 and S3).
> 
> #### Attach Policy to User Group
> 
> 18. Navigate to the user groups list in IAM.
> 19. Select a user group (e.g., "dev 1 and 2 group").
> 20. Attach the policy to the group.
> 21. Verify that all users in the group now inherit the permissions from the attached policy.
> 
> #### Grant Full Admin Access to a User Group
> 
> 22. Navigate back to the user groups list in IAM.
> 23. Select another user group (e.g., "three group").
> 24. Attach the predefined "Admin" policy to give full admin access to the user group.
> 25. Verify full admin access by logging in as a user in that group and showing they have full permissions to all AWS services.
> 
> #### Conclusion
> 
> 26. Summarize what was covered in the session.
> 27. Mention what will be covered in the next session (Creating roles).
> 
> This should make it easier for you to follow the steps demonstrated in the video.

### Lecture 4 – Roles

- Role is similar to an user/group which has permissions/policies attached to it.
- Roles are temporary access given to anyone needs to perform the specific task mentioned in the Role.
- When a user assumes an AWS role, they temporarily take on the permissions associated with that role and relinquish their original permissions for the duration of the role session.

#### Cross-Account Roles

Here's how cross-account roles generally work:

1. **Account A** (Trusting Account) creates an IAM role and attaches permissions to it. This role is configured to trust **Account B** (Trusted Account).
    
2. **Account B**'s users can then assume the role from **Account A** and access resources according to the permissions attached to the role.
    
3. When a user in **Account B** assumes the role from **Account A**, they give up their original permissions and temporarily take on the permissions attached to the role from **Account A** for the duration of the session.
    
4. Once the session expires or the user explicitly revokes the role, they revert back to their original permissions in **Account B**.
    

Cross-account roles are particularly useful for consolidating resources and managing permissions at scale, as well as for facilitating secure access between different organizational units or even different companies.


#### Identity Federation

Identity Federation, on the other hand, enables external identities (like users authenticated via Google, Facebook, or a [[SAML (Security Assertion Markup Language)|SAML]]-based [[IdP (Identity Provider)|identity provider]]) to assume roles or gain temporary access within an AWS account without having to be a user within that AWS account. The federation process allows these external identities to receive a set of temporary AWS security credentials that they can use to access AWS services.

### Demo 3 – Using Roles In IAM

> [!summary]- Demo 3 Steps
> It sounds like the session covered a detailed tutorial on how to create roles, how users can switch roles, and how permissions work within roles in some kind of service (presumably AWS). Here are the steps extracted from the session for creating roles and allowing a user to switch roles:
> 
> ### How to Create Roles
> 
> 1. **Navigate to Roles Section**: Go to the section where roles are managed within the service.
> 2. **Initiate Role Creation**: Click on "Create Roles".
> 3. **Choose Policy Type**: Choose the type of role you want to create. For custom roles, select "Custom Trust Policy."
> 4. **Specify Trust Policy**: Define the trust relationship by specifying the principle (e.g., type `AWS`) and providing the ARN (Amazon Resource Name) of the user who will be allowed to switch to this role.
> 5. **Assign Permissions**: Click 'Next' and specify the permissions that the role will have. For example, to grant Amazon RDS full access, choose that particular permission.
> 6. **Name the Role**: Give a name to the role, for example, `dev 3 role demo`.
> 7. **Review and Create**: Review the permissions and other settings, then click on "Create Role" to finalize the process.
> 
> ### How to Switch Roles for a User
> 
> 1. **Log in as the User**: Sign in to the service console with the user credentials who is allowed to switch roles (e.g., `dev 3 demo`).
> 2. **Navigate to Switch Role**: Find the option to switch roles within the service console.
> 3. **Enter Details**: Provide the account details and the name of the role you want to switch to (e.g., `dev 3 role demo`).
> 4. **Confirm Switch**: Click on "Switch Role" to change the role.
> 5. **Check Access**: Once the role is switched, you will only be able to access the services for which the role has permissions (e.g., RDS but not EC2 or S3).
> 6. **Switch Back**: To revert to the original role, find the option to switch back and click on it.
> 
> ### Note:
> 
> - The role permissions strictly limit what services can be accessed. For example, if you granted only Amazon RDS access, then services like EC2 and S3 would be inaccessible when the role is active.
> 
> This provides a comprehensive guide based on the session you described. Hope it's helpful!

### Lecture 5 – Identity Federation

**1. Introduction to Identity Federations**

- We'll delve into how identity federation operates alongside security token services.
- How to access an AWS service using identity federation?
- The processes of authentication and authorization for task execution.

---

**2. Understanding Web Identity Federation**

- **Definition:** When you wish to use an AWS service via logging in from a web identity federation.
    
- **Providers Examples:** Google, Facebook, Amazon, Twitter. You might see options like "Continue with Gmail" on websites – that’s Web Identity Federation.
    
    - _Process Overview:_
        1. Website requests the identity federation provider to authenticate the user.
        2. Providers check user genuineness without storing credentials.
        3. Once authenticated, users can access website services.

---

**3. How Web Identity Federation Integrates with AWS**
![[Pasted image 20230822200942.png]]
- Set up a role in AWS allowing a service to be accessed using Web Identity Federation.
    
    - _Process Steps:_
        1. Authenticate through a Web Identity Federation (e.g., Amazon, Google, Facebook).
        2. An authorization token is generated post-authentication.
        3. Send an AWS access request using this token and your specified role ARN (Amazon Resource Name).
        4. Utilize the "Assume Role with Web Identity" from your role section. This is managed by STS (Security Token Service), generating a temporary and privileged user.
        5. Receive temporary security credentials to begin accessing AWS services.

---

**4. SAML Identity Federation Overview**
![[Pasted image 20230822201112.png]]
- **SAML:** Stands for Security Assertion Markup Language.
    
    - _Key Features:_
        1. Log into one account to view all linked accounts.
        2. Use single sign-on for authentication and authorization.
        3. Access various CROSH region platform services post-authentication.
    - _Implementation Details:_
        1. In the principle, the ARN of the SAML provider is visible.
        2. "Assume Role with SAML" is the action counterpart to "Assume Role with Web Identity."
        3. Requests from SAML providers are permitted to grant permissions.

---

**5. Deep Dive into SAML Identity Federation Process**
![[Pasted image 20230822201142.png]]
- Start with any identity provider, e.g., LDAP or Microsoft Active Directory.
    
    - _Step-by-step Breakdown:_
        1. Perform a single sign-on.
        2. Generate XML metadata.
        3. Authenticate using your SAML identity provider.
        4. Map data onto the AWS account and use security tokens.
        5. Interact with applications and authenticate via LDAP or Microsoft Active Directory.
        6. Generate a SAML assertion and associate it with the role ARN and SAML provider ARN.
        7. Request an "Assume Role with SAML" through STS.
        8. Receive temporary security credentials to access the AWS account.

---

**6. Security Token Service (STS) Explained**
![[Pasted image 20230822201206.png]]
- STS is our primary interaction point.
    
- It provides temporary security credentials, allowing limited-time access to an IAM user.
    
    - _Procedure:_
        1. Make an STS call from the application or user side.
        2. STS grants temporary credentials.
        3. Use these credentials to access the AWS account and relevant services.

---

**7. Delving into STS Call Features**

- **Assume Role:** Specify the service an application or user can access. The default duration is 15 minutes to 1 hour (modifiable).
    
    - "Assume Role with Web Identity" specifies requests from web identity providers.
    - "Assume Role with SAML" handles requests from SML identity providers.
- **Get Federation Token and Get Session Token:** These provide temporary access key, security access key, and similar resources.


## Lecture 8 – IAM Access Analyzer

Identity and Access Management on AWS Access

#### Access Analyzer
Analyzer assists in identifying potential resource-access risks by identifying any policies that grant access to an external principal. It accomplishes this by analysing resource-based policies in your AWS environment using logic-based reasoning. Another AWS account, a root user, an IAM user or role, a federated user, an AWS service, or an anonymous user can all be external principals.

Use Case
- AWS IAM Access Analyzer provides the following capabilities:
- IAM Access Analyzer helps identify resources in your organization and accounts that are shared with an external entity.
- IAM Access Analyzer validates IAM policies against policy grammar an best practices.
- IAM Access Analyzer generates IAM policies based on access activity in your AWS CloudTrail logs.

#### Access Advisor

The AWS Identity and Access Management (IAM) access advisor uses data analysis to help you confidently set permission guardrails by providing service last accessed information for your accounts, organizational units (OUs), and your AWS Organizations-managed organization.

> [!summary]- Use Case
> Assume Arnav Desai is a security administrator for Example Corp. He works with several development teams and monitors their access across multiple accounts. To get his development teams up and running quickly, he initially created multiple roles with broad permissions that are based on job function in the development accounts. Now, his developers are ready to deploy workloads to production accounts. The developers need access to configure AWS, however, Arnav only wants to grant them access to what they need. To determine these permissions, he uses access advisor APIs to automate a process that helps him understand the services developers accessed in the last six months. Using this information, he authors policies to grant access to specific services in production. I'll now show you an example to achieve this in one account using AWS CLI commands.
> 


## Demo 7 – IAM Access Analyzer
#chat #miniProject 
> [!NOTE]
> Certainly, it looks like you're describing how to use AWS IAM (Identity and Access Management) Access Analyzer with S3 buckets to monitor their access permissions. Here's a simplified list of steps to replicate the demo:
> 
> ### Setting Up S3 Buckets
> 
> 1. **Log into AWS Management Console** and navigate to the **S3 service**.
> 2. **Create a new bucket**.
> 
> - Name it as `demo1_112345` (or any name you prefer).
> - Select the region as `Ohio` (or any other region).
> - Enable `ACL` and disable `Block Public Access`.
> - Click on `Create Bucket`.
> 
> 3. **Create another bucket**.
> 
> - Name it as `demo2_2123456` (or any name you prefer).
> - Select the same region as before (`Ohio`).
> - Enable `ACL` and disable `Block Public Access`.
> - Click on `Create Bucket`.
> 
> ### Making S3 Buckets Public
> 
> 4. For both buckets, go to the `Permissions` tab.
> 5. Click on `Edit` in the `Access Control List (ACL)` section.
> 6. Grant the permissions that you desire and make it public.
> 7. Confirm the actions and save changes.
> 
> ### Setting up IAM Access Analyzer
> 
> 8. Navigate to **IAM Management Console**.
> 9. Go to `Access Analyzer`.
> 10. Click on `Create Analyzer`.
> 
> - Name it `demo1_analyzer` (or any name you prefer).
> - Set the Zone of Trust as the current AWS account.
> - Make sure to select the same region where your buckets are located.
> - Click on `Create Analyzer`.
> 
> ### Verifying with IAM Access Analyzer
> 
> 11. Once the Analyzer is created, you should be able to see the newly created buckets listed with their access levels.
> 12. You will get notifications if your buckets have public access.
> 
> ### Managing Access
> 
> 13. If the bucket is intended to be public, click on `Archive`.
> 14. If the bucket is not intended to be public, you can change its permissions by:
> 
> - Going back to S3 Management Console.
> - Clicking on `Block All Public Access` and confirming the action.
> 
> This is a high-level summary, and the steps can vary slightly based on your specific needs or AWS updates after my last training data in September 2021.