- Create two Virtual Networks (VNets), one in the East US region (Vnet 1) and one in the West US region (Vnet 2).
 - In each VNet, deploy two Virtual Machines (VMs) - VM1 and VM2.
---

> [!attention] VNet to check location,  cidr


![[Pasted image 20231214155942.png]]

![[Pasted image 20231214160004.png]]
![[Pasted image 20231214150852.png]]

![[Pasted image 20231214160407.png]]


while creating the VPC we get an option to create Bastion, did that on central-us


### VMs
1. [[Clone the GitHub Repository]]

2. ![[Configure VMs]]

# Creating VM1 and VM2 East US
VM1 manual
```
#!/bin/sh
git clone https://github.com/hectorproko/azproject.git
cd azproject
sudo apt remove python3-blinker -y
sudo apt autoremove -y

sudo ufw allow 5000/tcp
sudo apt-get update
sudo apt-get install -y python3
sudo apt-get install -y python3-pip
python3 -m pip install -U pip
sudo pip3 install azure-storage-blob azure-storage-file-share azure-storage-file-datalake azure-storage-queue
pip3 install configparser
sudo pip3 install flask


sed -i "s|accountname|hectorstorage12345|" config.ini
sed -i "s|storageaccountkey|+gUKWA3UnIjAFv1u/xfV4cRNvCGbBS6H1SEVK54X9EPr1vELLpGQm2j3uYb1cefZnY/X5bYwPng/+AStbD71PA==|" config.ini

sudo python3 app.py
```


> [!Not necessary]
>  `sudo ufw allow 5000/tcp` ==app is running on 80==


![[Pasted image 20231215092722.png]]

![[Pasted image 20231215095439.png]]
![[Pasted image 20231215095800.png]]
after opening port 80 in NIC


VM2
```
git clone https://github.com/azcloudberg/azproject
bash vm2.sh
```

# Creating VM1 and VM2 West US






---

# REDOING