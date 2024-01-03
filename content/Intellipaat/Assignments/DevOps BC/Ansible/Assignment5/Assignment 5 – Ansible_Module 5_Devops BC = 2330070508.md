
> [!info] Module 5: Ansible Assignment - 5
> **Tasks To Be Performed:** 
> 1. Create a new deployment of Ansible cluster of 5 nodes 
> 2. Label 2 nodes as test and other 2 as prod 
> 3. Install Java on test nodes 
> 4. Install MySQL server on prod nodes 
> 
> Use Ansible roles for the above and group the hosts under test and prod.

### Step 1: Inventory File

I start by updating the inventory file `inventory.ini` from [[Assignment 1 – Ansible_Module 5_Devops BC = 2330070508|Assignment 1 – Ansible]] to define the nodes and their respective groups.

```yaml
[all:vars]
ansible_user=ubuntu

[test]
slave1 ansible_host=10.0.1.65 
slave2 ansible_host=10.0.1.233

[prod]
slave3 ansible_host=10.0.1.210
slave4 ansible_host=10.0.1.85

[other]
slave5 ansible_host=10.0.1.211
```
%%I make sure to replace `my_ssh_user` with the username that I have SSH access with, and `ip_of_x` with the actual IP addresses of my nodes.

Using ping [[Assignment 1 – Ansible_Module 5_Devops BC = 2330070508#^c4a4b0|Pinging nodes]]
[[Assignment 1 – Ansible_Module 5_Devops BC = 2330070508#^be0450|Setup SSH .pem]]
%%

### Step 2: Create a Playbook

I create a playbook named `setup.yml`. Inside, I define the tasks for each group directly:

```yaml
---
- hosts: test
  become: yes
  tasks:
  - name: Update the apt cache
    apt:
      update_cache: yes
    changed_when: false

  - name: Install default JDK
    apt:
      name: default-jdk
      state: present

- hosts: prod
  become: yes
  tasks:
  - name: Update the apt cache
    apt:
      update_cache: yes
    changed_when: false

  - name: Install MySQL server
    apt:
      name: mysql-server
      state: present
```
%%Having the update_cache as its own task instead of in apt: with the other task has its benefits, find out%%

### Step 3: Execute the Playbook

I run the playbook with the following command:
```bash
ansible-playbook -i inventory.ini setup.yml
```
This will apply the Java installation tasks to the test nodes and the MySQL installation tasks to the prod nodes.
![[Pasted image 20231106210807.png]]
### Step 4: Verify the Installations
```bash
#I verify Java installation on test nodes:
ansible test -i inventory.ini -m shell -a "java -version"

#And I check MySQL installation on prod nodes:
ansible prod -i inventory.ini -m shell -a "mysql --version"
```

> [!success]
> ![[Pasted image 20231106211340.png]]

These commands will give me the version output for Java and MySQL, confirming that the installations are successful on the respective nodes.

> [!attention]
> The versions of Java differ because I had [[Installing Jenkins On AWS#^7992da|previously installed Java manually on Slave1]], which explains why the [[Pasted image 20231106210807.png|playbook output]] indicates that no changes were made. Shown as `change=0`.

