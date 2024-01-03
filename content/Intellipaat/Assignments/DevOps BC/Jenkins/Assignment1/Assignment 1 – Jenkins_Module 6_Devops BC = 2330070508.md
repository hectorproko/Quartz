
> [!info] Module 6: Jenkins Assignment - 1
> **Tasks To Be Performed:** 
> 1. Trigger a pipeline using Git when push on develop branch 
> 2. Pipeline should pull Git content to a folder


> [!attention] Prerequisite
> ![[Installing Jenkins On AWS]] 

I create a repository named `JenkinsAssignment` on GitHub and then create a `develop` branch within it.
![[Pasted image 20231108102220.png|300]]

> [!NOTE]
> My terminal is already set up to be able to clone using SSH.

I'll create Freestyle job called `Job1`  
`Dashboard > New Item`  
![[Pasted image 20231108102959.png|400]]

![[Pasted image 20231108103235.png|400]]
![[Pasted image 20231108105216.png|400]]

%%
> [!NOTE]
> 1. **GitHub Project – Project URL:**
>     
>     - This is part of the Jenkins GitHub plugin which integrates Jenkins with GitHub specifically.
>     - The Project URL is used to link your Jenkins project to the corresponding GitHub project.
>     - When you configure this URL, Jenkins can use the GitHub API to display links to the GitHub repository on the Jenkins project pages.
>     - This URL is typically used for reference and integration features, such as linking to the source code from Jenkins build pages, but it does not control where Jenkins fetches the source code from.
> 2. **Source Code Management – Git – Repository URL:**
>     
>     - This is the URL Jenkins uses for checking out the source code as part of the build process.
>     - SCM configuration is where you define the repository from which Jenkins actually pulls the code to build and test.
>     - It's more functional as compared to the GitHub project URL because Jenkins uses this to interact with the repository to perform checkout, polling, and other SCM-related operations.

%%

%%Seem like we get away from not specifying credntials for the repo because it is public%%
We'll be working with branch `develop`
![[branch specifier develop.png]]
We want the job to be triggered by a GitHub webhook. 
![[GitHub hook trigger for GITScm polling.png|280]]
We want this job to execute in `Slave1`
![[Pasted image 20231108114842.png|280]]
Save
%%[[job1_entirepage.png|Entire Page for above]]%%

In GitHub, we set up the webhook. We navigate to 'Webhooks' in the repository settings.  
Click on "Add webhook"  
![[Pasted image 20231108105740.png]]

Enter the public IP address of the EC2 instance hosting Jenkins, followed by the Jenkins port, which is 8080.
![[webhook payload URL.png|400]]
Click button "Add webhook"
%%[[job1_entirepage 1.png]]%%

> [!attention]
> I need to be careful when restarting my EC2 instance (Jenkins Master), as this will change the public IP address.

> [!success]
> GitHub sends a ping to test it out.
> ![[Pasted image 20231108110428.png]]

We navigate back to our Jenkins dashboard, select 'Job1,' and execute it by clicking 'Build Now.'
![[build now button.png|280]]

If I click on the build and check its 'Console Output,' I can see that it was started by me and that it was successful.
![[Pasted image 20231108111550.png|280]]

To test the webhook, I'll make a push to the develop branch. I'll clone the repository, switch to the develop branch, create a file `somefile`, and then push it.
![[Pasted image 20231108112325.png]]

> [!success]
> We get another build this time triggered by the POST request that GitHub sends instead of "[[build now button.png|Build Now]]" button.
> ![[Pasted image 20231108112502.png|280]]

> [!success]
> Now, if we check inside the 'Slave1' node, we can see 'Job1's' workspace, which contains the contents from the repository.
> ![[Pasted image 20231108115633.png]]



%%
Some learning the connection to the repo could we done with username and toke
%%

%%Issue:
Forgot to restrict the job to Slave1 now I dont see `/home/ubuntu/jenkins` neithe rin master nor Slave1
In the Consoleout put we see it went to `/var/lib/jenkins/workspace/`
Fixed: added to only one on slave2%%
