---
tags:
  - Terraform
---
==PENDING CLEANUP==
### Windows

1. **Downloading Terraform**
   First, I head over to the official Terraform website to grab the latest version. In the downloads section, I select the `Windows_AMD64` option, since that matches my system's architecture. Clicking the link initiates the download of a `.zip` file.

2. **Extracting the Terraform Executable**
   Once the download finishes, I find the `.zip` file in my Downloads folder. I right-click on it and choose `Extract All...`, which reveals the `terraform.exe` within. I decide to keep it simple and leave `terraform.exe` right there in the Downloads folder for now.

3. **Setting Up the Environment Variable**
   <br><br>![[Add.Edit Environment Variables (Windows)]]
4. **Testing the Terraform Command**
   To check if everything's working, I open a new Command Prompt window and type `terraform --version`.
  > [!success]
  >    <br><br>![[terraform --version.png]]

  
### Linux

> From [[PART1_PROJECT_16]]


Update the system packages:
```bash
sudo apt update
```

Install the `wget` and `unzip` packages to download and extract the Terraform setup:
```bash
sudo apt-get install wget unzip -y
```


```bash
hector@hector-Laptop:~/Project16-17$ sudo wget https://releases.hashicorp.com/terraform/0.14.7/terraform_0.14.7_linux_amd64.zip #download terraform setup

hector@hector-Laptop:~/Project16-17$ ls #zip file downloaded
PBL  README.md  terraform_1.1.9_linux_amd64.zip

hector@hector-Laptop:~/Project16-17$ sudo unzip terraform_1.1.9_linux_amd64.zip #Extract the downloaded setup using unzip
Archive:  terraform_1.1.9_linux_amd64.zip
inflating: terraform

hector@hector-Laptop:~/Project16-17$ ls #terraform extracted
PBL  README.md  terraform  terraform_1.1.9_linux_amd64.zip

hector@hector-Laptop:~/Project16-17$ sudo mv terraform /usr/local/bin/ #moving extracted setup to /bin directory
```

> [!success]
> ```bash
> hector@hector-Laptop:~/Project16-17$ terraform -v #checking `version (not latest)
> Terraform v1.1.9
> on linux_amd64
> ```
