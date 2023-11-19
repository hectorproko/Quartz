==Pending CleanUP==
#AWS
> [!info] AWS DevOps Case Study - 1
> **Training Problem Statement:**
> You work for XYZ Corporation. Your corporation wants the files to be stored on a private repository on the AWS Cloud. Once done, you are required to automate a few tasks for ease of the development team. 
> 
> **Tasks To Be Performed:**
> 1. Create a website in any language of your choice and push the code into GitHub. 
> 2. Migrate your GitHub repository into the AWS CodeCommit repository. 
> 3. Create two CodeDeploy deployments (for the QA stage and the Production stage) with an EC2 deployment group into which you can push the code from the CodeCommit repository. 
> 4. Using AWS CodePipeline, create a software development life cycle: 
> 	   a. The source is the CodeCommit repository 
> 	   b. The code will be pushed into the deployment created in CodeDeploy 
> 	   c. There should be two stages in deployment, the QA stage and the Production stage 
> 	   d. Only when the QA stage is successful, the Production stage should be executed 
> 5. Create a third stage where the same website is pushed into an Elastic Beanstalk environment. 
> 
> *Note: The application can be of any language, or it can even be a sample application. The purpose here is to create a CI/CD pipeline, not to create a great application.*

**Referencing previous assignments:**
- [[Assignment 1 – AWS DevOps_AWS DevOps_AWS Weekday BC = 2301080808|Assignment 1 – AWS DevOps]]: Set up the SSH client and change the local git repo remote origin. 
- [[Assignment 2 – CodeDeploy_AWS DevOps_AWS Weekday BC = 2301080808|Assignment 2 – CodeDeploy]]: Create a CodeDeploy application and Deployment Group. 
- [[Assignment 3 – CodePipeline_AWS DevOps_AWS Weekday BC = 2301080808|Assignment 3 – CodePipeline]]: Use the same PHP page. 
- [[Assignment 2 – Elastic Beanstalk_Module9_AWS Weekday BC = 2301080808|Assignment 2 – Elastic Beanstalk]]: Learn how to create a Beanstalk environment.

---

1. **GitHub Repository Creation**:
  - Created a GitHub repository named `php_page`.
    <br>![[Pasted image 20231026092129.png|260]]

2. **AWS CodeCommit Repository**:
  - Created a new repository named `php_page` in AWS CodeCommit.

3. **Linking Repositories**:
  - Clone the `php_page` repository.
  - Change the remote origin to link the local repository to the `php_page` repository in CodeCommit.

Use the following command:
```bash
git remote add codecommit ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/php_page
```

<br>![[Pasted image 20231020205521.png]]

4. **Setting Up the SSH Client for AWS CodeCommit**
   I open my terminal: This is where I'll input all the necessary commands.
   
   I edit the SSH configuration:
```javascript
Host git-codecommit.*.amazonaws.com   
User APKAG4NQRHE3SUWI647   
IdentityFile ~/.ssh/id_rsa
```
%%The User in this assignment or repo was not APKAG4NQRHE3SUWI647, used AKIA4GNRQHE3YHDJ77VM just wanted to reuse the image%%
<br>![[Pasted image 20231018202828.png]]

I push the content to AWS CodeCommit: Using the terminal, I run:
```bash
git push codecommit main
```

I verify the push: I navigate to the `php_page` repository in CodeCommit
<br>![[Pasted image 20231026091502.png|400]]


5. Setting Up 2 EC2 Instances for Deployment
   - **I make a mental note**: Every EC2 instance requires three main configurations a Role, the CodeDeploy Agent installed, and the appropriate tags.
   - **I configure the security group** to ensure ports for SSH and HTTP are open for accessibility.

**CodeDeploy Agent Install**
In the user data section, I paste the following script to install CodeDeploy agent:
```bash
#!/bin/bash
sudo apt-get update -y
sudo apt-get -y install ruby
sudo apt-get -y install wget
cd /home/ubuntu
wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
sudo chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent start
```
%%*Doesnt seem to do the job from user data consistently*, May require you to resintall, if deploy fails%%
%%
> [!NOTE]- Installing CodeDeploy agent for Ubuntu
> 1. Update the package manager and install Ruby and wget:
> ```
> sudo apt update -y
> sudo apt install wget -y
> ```
> 2. Download the CodeDeploy agent archive to the default user's home directory:
> ```
> cd /home/ubuntu
> wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
> ```
> 
> 3. Make the installer script executable:
> ```
> chmod +x ./install
> ```
> 
> 4. Do one of the following:
>    - To install the latest version of the CodeDeploy agent on any supported version of Ubuntu Server except 20.04:
> ```
> sudo ./install auto
> ```
> 

%%
**EC2 Instance Tags**
The tags for each EC2 instance are crucial. They enable the deployment group in AWS CodeDeploy to correctly reference and target the instances during the deployment process. Without the appropriate tagging, the deployment might not work as intended.

Server 1 (QA Environment)

|Key|Value|
|---|---|
|env|QA|
|Name|server1|
|app|XYZ-Website|

Server 2 (PROD Environment)

|Key|Value|
|---|---|
|env|PROD|
|Name|server2|
|app|XYZ-Webs|


**Attaching an IAM Role to EC2**
After creating the EC2 instances, I select them in the EC2 dashboard. Then, I click on **Modify IAM role**. In the dropdown menu, I pick the role `EC2CodeDeploy` (associated with the policy `AmazonEC2RoleCodeDeploy`).
<br>![[Pasted image 20231026095027.png|400]]
<br>![[Pasted image 20231026095620.png|550]]

6. **Creating Application in AWS CodeDeploy**

	Application Name: XYZ-website
	- Navigate to Developer Tools > CodeDeploy > Applications > Create application.
	- Under "Application configuration", set the following:
	    - Application name: XYZ-website
	    - Compute platform: EC2/On-premises
	<br>![[Pasted image 20231026102046.png|400]]
	
	Deployment Groups: Create two deployment groups, namely QA and PROD.
	- Role: `CodeDeployRole` *(with policies `AmazonEC2FullAccess` and `AWSCodeDeployRole`)*.
	%%<mark style="background: #FFB8EBA6;">does it really need EC2FullAccess or is it included in the other</mark>%%
	
	I manage Tags:
	- I ensure to pick tags that relate to my EC2 instances.
	- I identify the specific EC2 instance by selecting two tags: "app" and "env". I make sure both tags match by using two tag groups.
	
	- During the setup, I uncheck the option "Enable load balancing".
	%%[[deployment group QA.png]]%%
	%%Forgot to change to *CodeDeployDefault.OneAtATime* diff in pic%%
	
	I replicate the steps for PROD:
	- I repeat the same steps to set up the application in the PROD environment.
	%%[[deployment group PROD.png]]%%
	
	<br>![[Pasted image 20231026103800.png|500]]
	
	
	
	%%Pipeline roles default can be used%%

7. **Creating an Elastic Beanstalk Environment**

	I start by navigating to AWS Elastic Beanstalk. Once there, I initiate the creation process by clicking on the `Applications` tab and selecting "Create New Application". I then set the application name to "PHP_app". Keeping in line with [[Assignment 2 – Elastic Beanstalk_Module9_AWS Weekday BC = 2301080808|Assignment 2 – Elastic Beanstalk]], I ensure that I choose a PHP web environment to host my page.
	
	<br>![[PHP Beanstalk app.png|450]]
	<br>![[PHP beanstalk env.png]]



8. **Creating a CodePipeline**

	I start by naming my pipeline "Deploying_PHP" and selecting "V1" for the version. I use the default role.
	
	Next, for the source stage, I choose AWS CodeCommit as the source provider. I pick the repository "php_page" and set the branch to "php".
	<br>![[Pasted image 20231026135039.png|400]]
	*I chose the "php" branch because that's where I stored the web pages and scripts* %%Maybe merge to main%%
	
	In the "Add build stage", I selected AWS CodeBuild as my build provider. I set the region to "US East (N. Virginia)". When it came to selecting a project name, I realized I needed to create a new one. So, I opted to create "SimpleZIP" right there by clicking the "Create project" button. Once "SimpleZIP" was successfully created in the AWS CodeBuild console, I proceeded. I didn't add any environment variables at this stage. For the build type, I chose "Simple build" to trigger a single build.
	<br>![[Pasted image 20231024145833.png|470]]
	*A BuildProject defines the environment in which you execute the build phase commands.*
	
	For the "Add deploy stage", I'll skip it for now. Once I edit the pipeline, I'll incorporate all the deploy stages.
	
	Both stages have completed without any issues as indicated by the green checkmarks. Next, I'll proceed by clicking the "Edit" button to make necessary adjustments.
	<br>![[IntelliPaat/Assignments/AWS/AWS DevOps/Case Study/pipeline.png]]
	
	
	I've added three new stages titled "QA", "PROD", and "Beanstalk" by clicking the "Add stage" button. For each stage, there's an option to include specific actions. 
	<br>![[Pasted image 20231026141016.png|300]]
	
	To define actions for these stages, I'll proceed by clicking the "Add action group" button within each stage.
	
	For the "QA" stage, an action group named "Deploying-QA" has been set up. It utilizes AWS CodeDeploy as the action provider and targets the "US East (N. Virginia)" region. The input artifact selected is "BuildArtifact". Within this action, the application name defined is "QX-XYZ-Website" and the deployment group is "QA".
	<br>![[QA Action Group.png|450]]
	
	Similarly, for the "PROD" stage, an [[PROD Action Group.png|action group]] has been created with settings that are largely consistent with the "QA" action group, but with a different deployment group specified.
	
	For the "Beanstalk" stage, an action group named "Deploying-Beanstalk" has been established. This action uses AWS Elastic Beanstalk as its provider and is directed at the "US East (N. Virginia)" region. The input artifact chosen is "BuildArtifact". The specified application within this action is "[[PHP Beanstalk app.png|PHP_app]]" and it targets the "[[PHP beanstalk env.png|PHPapp-env]]" environment in Elastic Beanstalk.
	<br>![[Beanstalk Action Group.png|450]]
	
	
	
	After finalizing my changes, I click the "Save" button and see [[Newly added stages.png|newly created stages]]. 
	
	Click button "Release change" to restart the pipeline
	
	When I see that all [[successfulStages.png|stages have been successfully completed]] stages have been successfully completed, I know my tasks are accomplished.
	
	I navigate to my EC2 dashboard to verify if the page is hosted. Once there, I spot all my EC2 instances that are hosting the PHP page, including the Beanstalk-associated one. Using their public IPs, I promptly access my browser and input each IP to view the hosted content.
	<br>![[Pasted image 20231026143401.png]]

> [!Success]
> **Beanstalk**
> <br>![[Pasted image 20231026143451.png]]
> **Server1 (QA)**
> <br>![[Pasted image 20231026143556.png]]
> **Server 2 (PROD)**
> <br>![[Pasted image 20231026143634.png]]``


---

%%

> [!tip]
> Remember teh pipeline uses a bucket that it creates, and the bucket needs verision, i guess when you dont pick one of yours it creates one with what is needed
> 


# Issue

> [!question] Issue:
> 
> The build was causing deploy to fail:
> > [!error]
> >    `No such file or directory @ rb_sysopen - /opt/codedeploy-agent/deployment-root/789d20b6-ab8f-4c53-aba9-d37d152225c7/d-0L021MKF2/deployment-archive/index.php`
> 
> 1. I think is because `buildspec.yml` has
> ```
> artifacts:
>   type: 
>   files:
>     - index.html
>     - appspec.yml
>     - scripts/install_dependencies
>     - scripts/start_server
>     - 1.png
>     - aws.gif
>     - back.jpg
> ```
> and some of these files dont exist in repo 1.png, aws.gif, back.jpg
> will trying removing them from list
> 
> > [!success]
> > 2. about removing but adding index.php into the artifiacts
> > ```
> > artifacts:
> >   type: 
> >   files:
> >     - index.html
> >     - index.php
> >     - appspec.yml
> >     - scripts/install_dependencies
> >     - scripts/start_server
> >     - 1.png
> >     - aws.gif
> >     - back.jpg
> > ```
> > 


> [!tip] Explanation
> - The files you specify in the `artifacts` section of the `buildspec.yml` are the ones that get packaged up after the build.
>     
> - The files you specify in the `files` section of the `appspec.yml` are the ones that CodeDeploy expects to find in the artifact and will attempt to deploy to the target instances.



# Errors
To test inside each applicaiton created a deployment but had ec2 tags as targets
<br>![[Pasted image 20231020212730.png]]

Had this error
<br>![[Pasted image 20231021190606.png]]
Was targeting Index.zip, but the actually file was lowercase index.zip

I belive this error was because no agent was running
<br>![[Pasted image 20231021202731.png]]

%%