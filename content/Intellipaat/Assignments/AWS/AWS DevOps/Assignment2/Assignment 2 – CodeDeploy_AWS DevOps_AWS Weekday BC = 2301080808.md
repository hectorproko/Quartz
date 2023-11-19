#AWS
> [!info] AWS DevOps Assignment - 2
> **Training Problem Statement:**
> You work for XYZ Corporation. Your corporation wants the files to be stored on a private repository on the AWS Cloud. Once done, you are required to automate a few tasks for ease of the development team. 
> 
> **Tasks To Be Performed:**
> 1. Create a CodeDeploy Application with the compute platform as EC2. 
> 2. Create a deployment group with the selected EC2 instance. 

### 1. Setting up CodeDeploy Application for EC2:

**In the AWS Management Console:** 
a. I sign in. 
b. I go to AWS CodeDeploy under Developer Tools. 
c. I click "Getting started", then choose "Create Application". 
d. I type "XYZ_Corporation_App" as the Application Name. 
e. I select "EC2/On-premises" for the "Compute platform". 
f. I click "Create application".
![[Pasted image 20231019092334.png]]
    

### 2. Setting up Deployment Group for the EC2 Instance:

*EC2 instance need AWS CodeDeploy Agent installed and running. This agent facilitates the deployment tasks and communicates with the CodeDeploy service.*

**In the AWS Management Console:**

a. I navigate to the CodeDeploy console and click on the application name I previously created.
b. Under the "Deployment groups" tab, I click "Create deployment group".
c. I name the Deployment Group as "XYZ_Deployment_Group".
d. For the Service role, I choose the previously created role "AWSCodeDeployRole" which has the "AWSCodeDeployRole" policy attached.
e. I opt for "In-place deployment" in the "Deployment type" section.
f. In "Environment configuration", I select "Amazon EC2 instances".
g. I decide to identify my EC2 instance using tags. I ensure the EC2 instance I want to deploy to has the tag `Name` set to `XYZ_Instance`. Alternatively, I could manually select the instance.
h. In "Deployment settings", I select the "CodeDeployDefault.OneAtATime" configuration for simplicity.

i. I finalize by clicking "Create deployment group".
![[Pasted image 20231019092629.png]]

%%Disabled load balancing[[create deploynet group.png]]%%

You've now successfully created an AWS CodeDeploy application and a deployment group targeting an EC2 instance using the AWS Management Console.

%%
> [!info]- Explanations 
> 1. **CodeDeploy Application**:
>     
>     - This is a logical entity that represents your application in AWS CodeDeploy. Think of it as a container or a namespace for your deployments.
> 2. **Deployment Group**:
>     
>     - This is a set of individual deployment targets, in this case, an EC2 instance. It specifies the criteria to identify the deployment targets (using tags or an Auto Scaling group name).
>     - The deployment group also specifies the service role that CodeDeploy should assume to carry out deployments (the `AWSCodeDeployRole`).
> 3. **Configuration for Deployment**:
>     
>     - The deployment configuration associated with the deployment group, such as `CodeDeployDefault.OneAtATime`, determines how the deployment will be carried out on the targets.
> 4. **EC2 Target Instance**:
>     
>     - This is the actual server or virtual machine where you want to deploy your application.
>     - The EC2 instance should have the CodeDeploy agent installed and running, and it should be tagged or belong to an Auto Scaling group as specified in your deployment group settings.
> 5. **Service Role (IAM Role)**:
>     
>     - The IAM role (`AWSCodeDeployRole`) that CodeDeploy assumes to interact with other AWS services, such as accessing an application stored in an S3 bucket or interacting with EC2 instances.
> 
> However, there are a couple of important things to note:
> 
> - **No Actual Application Deployed Yet**: You've set up the infrastructure and the configuration, but you haven't actually deployed any code or application to the EC2 instance through CodeDeploy. The actual content to be deployed (like an application revision stored in S3 or GitHub) needs to be specified in a deployment.
>     
> - **Prerequisite Configurations**: This setup assumes that the EC2 instance you're targeting already has the CodeDeploy agent installed and running. The instance should also have the necessary IAM instance profile attached to allow the agent to communicate with CodeDeploy.

%%

