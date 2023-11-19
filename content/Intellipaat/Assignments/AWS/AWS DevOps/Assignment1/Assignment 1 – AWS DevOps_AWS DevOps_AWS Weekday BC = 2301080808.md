#AWS
> [!info] AWS DevOps Assignment - 1
> **Problem Statement:**
> You work for XYZ Corporation. Your corporation wants the files to be stored on a private repository on the AWS Cloud. 
> 
> **Tasks To Be Performed:** 
> 1. Create a CodeCommit repository and import a GitHub repository content into it.

%%[[CodeCommit_aws]]%%

### 1. Creating an IAM User:
1. I log into AWS.
2. I navigate to IAM.
3. I create a user named "GitUser."
4. I attach the `AWSCodeCommitFullAccess` policy.

### 2. Uploading Public SSH Key to the IAM User:
1. I click on the user.
2. I select the "Security credentials" tab.
3. I press the "Upload SSH public keys" button.
4. A window appears.
5. I paste my public key into the provided input box.
6. I click the "Upload SSH public key" button.
   ![[Pasted image 20231018201404.png]]
7. Once done, AWS gives me an SSH Key ID.
8. I note down this ID for future use.
   ![[Pasted image 20231018201734.png]]

### 3. Setting Up the SSH Client:
1. I open the `~/.ssh/config` file, or create it if it doesn't exist.
2. I add the following configuration:
	```css
	Host git-codecommit.*.amazonaws.com
	User APKAG4NQRHE3SUWI647
	IdentityFile ~/.ssh/id_rsa
	```
	![[Pasted image 20231018202828.png]]

%%
## 4. Test SSH Connection:
To ensure you've set everything up correctly, try cloning an existing CodeCommit repository:
```
git clone ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/Packer
```
%%

### 4. **Set Up CodeCommit Repository**
1. I go to AWS CodeCommit in the AWS Management Console.
2. I click the "Create repository" button.
3. I name the repository "Packer", matching the GitHub repo name.
4. I press "Create".
![[Pasted image 20231018203812.png]]

### 5. Cloning GitHub Repository
I navigate to my GitHub repository and copy the SSH URL: `git@github.com:hectorproko/Packer.git`.
![[Pasted image 20231018203924.png]]

On my local machine, I run:
```bash
git clone git@github.com:hectorproko/Packer.git
cd Packer
```

### 6. **Adding CodeCommit Repository as a New Remote:**

I go to the AWS CodeCommit console and navigate to the repository I just set up. I click on the Clone URL dropdown and choose Clone SSH, then I copy this URL.
![[Pasted image 20231018204407.png]]

Back in my local repository directory on my machine, I enter:
```bash
git remote add codecommit ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/Packer
```

To verify the remote was successfully added, I type:
```
git remote -v
```
![[Pasted image 20231018205114.png]]
<!-- The key takeaway here is that when adding a remote, you can name it whatever you like (`codecommit` in our case), and then you specify the URL of that remote repository.-->

### 7. **Pushing Repository Content to CodeCommit:**

Ensuring my SSH setup is correct, I can now push my local repository content to CodeCommit. I use the command:
```
git push codecommit main
```

%%**Note:** If you're using a branch other than `master`, replace `master` with your branch's name.%%
![[Pasted image 20231018210300.png]]


### **8. Verifying the Repository Content:**
I open the CodeCommit repository in the AWS Management Console. By checking the listed files and their commit history, I ensure they match what's in my original GitHub repository.
![[Pasted image 20231018210356.png]]

> [!success]
> The files in CodeCommit are the same as those in my GitHub repository.