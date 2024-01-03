
> [!info] Module 5: Ansible Assignment - 1
> Tasks To Be Performed:** 
> 1. Setup Ansible cluster with 3 nodes 
> 2. On slave 1 install Java 
> 3. On slave 2 install MySQL server 
> 
> Do the above tasks using Ansible Playbooks


> [!NOTE] EC2 instances
> Ansible Control Machine `10.0.1.223`
> Slave1 `10.0.1.65`
> Slave2 `10.0.1.233`

^a2c939


1. **I install Ansible on the control node**:

- If I'm using a Debian-based system such as Ubuntu, I install Ansible with:
```bash
sudo apt update -y
sudo apt install ansible -y
```

![[Pasted image 20231106085216.png]]
%%Notice no default config file present, this installation did not created `/etc/ansible/[hosts,ansible.cfg]` as its usually the case
%%

> [!attention] Another install option
> This method adds the Ansible PPA (Personal Package Archive) to your system and install Ansible from that source:
> ```bash
> sudo add-apt-repository -y ppa:ansible/ansible
> sudo apt update -y
> sudo apt install ansible -y
> ```
> This method will install the latest version of Ansible from the Ansible PPA, which is often more recent than the version available in the default repositories.

^aa5175

2. Setup SSH `.pem` 
   %%ssh-agent lifespan is until you close instance%%
%%
```
eval $(ssh-agent -s)
ssh-add daro.io.pem
ssh-add -l
```

%%

^be0450

In order to establish a temporary and secure connection to slave instances for inspection purposes, I load the key into the session once at the start using `ssh-agent` utility. ^1cba58
```bash
ubuntu@ip-10-0-1-223:~$ ls
daro.io.pem
ubuntu@ip-10-0-1-223:~$ chmod 600 daro.io.pem
ubuntu@ip-10-0-1-223:~$ eval $(ssh-agent -s)
Agent pid 2707
ubuntu@ip-10-0-1-223:~$ ssh-add daro.io.pem
Identity added: daro.io.pem (daro.io.pem)
ubuntu@ip-10-0-1-223:~$ ssh-add -l
2048 SHA256:wq3aSIyEU9dbylJv50YOhgXXPfcxZT7J5EmRIjLXZeA daro.io.pem (RSA)
```

Tested connection to one of the slaves `Slave1` 
![[Pasted image 20231106092328.png]]


2. **I set up the inventory file**:

- I'll create inventory file,  at current working directory `/home/ubuntu`, using a text editor like `nano`: ^29ce4e
```bash
nano inventory.ini
```
- Inside the file, I create a group `[nodes]` and add my three nodes under this group, replacing the placeholders with the actual IP addresses and usernames:
```bash
[nodes]
slave1 ansible_host=10.0.1.65 ansible_user=ubuntu
slave2 ansible_host=10.0.1.233 ansible_user=ubuntu
```

I'll ping the hosts using the ping module to test connection
```bash
ansible all -m ping -i inventory.ini
```

^c4a4b0

> [!success]
> ![[Pasted image 20231106105936.png]]


3. **I create the Ansible playbook**:

- I open a new file called `myplaybook.yml` with my text editor:
```bash
nano myplaybook.yml
```
- I then proceed to write my playbook, defining the tasks to install Java on `slave1` and MySQL on `slave2`.
```yml
---
- hosts: slave1
  become: yes
  tasks:
    - name: Install Java on Slave 1
      ansible.builtin.apt:
	    update_cache: yes
        name: default-jdk
        state: present

- hosts: slave2
  become: yes
  tasks:
    - name: Install MySQL server on Slave 2
      ansible.builtin.apt:
	    update_cache: yes
        name: mysql-server
        state: present
```
 %% 
> [!question]- Issue: Installing mysql-server
> > [!fail] 
> > Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?
> 
> > [!success]
> > Needs `apt-get update`, playbook equivalent `update_cache: yes`
> 

%%

4. **I execute the Ansible playbook**:

- In the terminal, I navigate to the directory where my `myplaybook.yml` is located.
- I run the playbook with:
```bash
ansible-playbook -i inventory.ini myplaybook.yml
```

> [!success]
> ![[Pasted image 20231106114821.png]]