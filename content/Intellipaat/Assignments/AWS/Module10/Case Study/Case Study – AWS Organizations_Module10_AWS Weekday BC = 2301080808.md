
> [!info] Module 10: Case Study - 1 
> **Problem Statement:** 
> You work for XYZ Corporation and the company is using AWS for its infrastructure. For administrative purposes it needs to provide certain employees with access to certain tasks. 
> 
> **Tasks To Be Performed:** 
> 1. Create a [[FSx for Lustre|FSx file system]] for both a Linux system and mount it to 2 EC2 Ubuntu or Amazon Linux instances. 
> 2. Create 2 Linux EC2 instances and launch web servers in all of them. 
> 3. Create a Global Accelerator and use it as the endpoint to both the instances. 
> 4. Create a network interface and attach it to one of your EC2 Linux instances. Use the network interface IP to SSH into the instance.


[[Assignment 4 – FSx_Module2_AWS Weekday BC = 2301080808#2. Create an FSx file system for Lustre and attach it to an Amazon Linux 2 instance.|Assignment 4 – FSx Lustre]]

So lets create Lustre storage, then we create EC2 with user data running command:
a. installs lustre client
b. mout drive
c. install host site but directed the lustre storge

![[Pasted image 20230824145753.png]]

From [[Assignment 1 – EC2_Module2_AWS Weekday BC = 2301080808#^022e1c]]
![[Pasted image 20230822214313.png]]


```bash
#!/bin/bash

# Update yum package manager
sudo yum update -y
# Install Lustre 2.10 dependencies
sudo amazon-linux-extras install -y lustre2.10
# Create a new directory
sudo mkdir -p /fsx
# Mount the Lustre filesystem to /fsx
sudo mount -t lustre -o noatime,flock fs-024eadf78b1e1fce8.fsx.us-east-1.amazonaws.com@tcp:/gelmnbev /fsx


# Install Nginx
sudo yum install nginx -y

# Modify the Nginx configuration to use the new webroot directory
sed -i 's|root /var/www/html;|root /fsx;|' /etc/nginx/sites-available/default

# Create new webroot directory
mkdir -p /fsx

# Change the website content in the new directory
echo '<!DOCTYPE html>
<html>
<head>
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>' > /fsx/index.html

# Enable and start Nginx service
systemctl enable nginx
systemctl start nginx

# Reload Nginx to pick up the new configuration
#systemctl reload nginx

```

^87ad1a


Creating the lustre FSx

I search for FSx Lustre, get to dasboard, click button "Create file system"

I select "amazon FSx for Lustre" click "Next"

named it "FSx file system"
picked lustre Security Group, look into ways to harden it
![[lustre security group.png]]
So we should redo it to only allow the EC2s to connect, since both EC2 will have the same Security Group, we can specify the security group in source to reference the EC2s

We have this security group `HTTP,HTTPS` which allows HTTP,HTTPS this will attached to both EC2 later for now this security will become the source of teh lustre security group for granular access
![[Pasted image 20231014222325.png]]
updated the `Lustre` security group
![[lustre security group 2.png]]
[changed ports to 1018-1023 as per docs](https://docs.aws.amazon.com/fsx/latest/LustreGuide/cannot-create-fs.html#:~:text=Action%20to%20take,with%20each%20other.)

> [!fail] issue:
> 
> ![[Pasted image 20231014230245.png]]
> ```
> The file system cannot be created because the default security group in the subnet provided or the provided security groups do not permit Lustre LNET network traffic on port 988
> ```
>


> [!question] Bypass
> in the source instead of using Security Groups, used the VPC CDIR

Lustre created, make note of the endpoint


> [!fail] Issue
> I spin RedHat machine could not ssh into, seem solely cuse it was an RedHat machine

[Installing Lustre client]([Installing the Lustre client - FSx for Lustre (amazon.com)](https://docs.aws.amazon.com/fsx/latest/LustreGuide/install-lustre-client.html)) in RedHat


---
### Creating Ubuntu with Lustre
[[lustre.png]]


https://docs.aws.amazon.com/fsx/latest/LustreGuide/install-lustre-client.html

```bash
sudo yum update -y
sudo amazon-linux-extras install -y lustre

#Create a new directory
sudo mkdir /fsx
#Mount
sudo mount -t lustre -o noatime,flock fs-0e660e4b2e8731c0a.fsx.us-east-1.amazonaws.com@tcp:/f7c4fbev /fsx

```

check
```
[ec2-user@ip-172-31-6-12 ~]$ rpm -qa | grep lustre
lustre-client-2.12.8-2.amzn2.x86_64
```

`lfs --version`

> [!NOTE] Using systemctl
> 
> This is expected behavior. The Lustre client does not typically run as a standalone service, unlike some other software. Instead, the client provides the necessary modules and tools to interact with Lustre file systems.

