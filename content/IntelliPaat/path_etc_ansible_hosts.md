<mark style="background: #FFF3A3A6;">Default inventory file</mark>

```css
/etc/ansible/hosts
```

![[path_etc_ansible_hosts.png]]

> [!tip]- Explanation
> 1. `[production]`:
>     
>     - This is a group name. In Ansible's inventory system, you can organize hosts into groups to make it easier to manage and target specific sets of machines. In this case, there's a group named "production."
> 2. `slave1 ansible_ssh_host=18.225.34.114`:
>     
>     - `slave1` is an alias or hostname that you're using within Ansible to reference a specific machine.
>     - `ansible_ssh_host=18.225.34.114` is a variable setting for that specific host. It tells Ansible that when you refer to `slave1`, it should connect to the IP address `18.225.34.114` using SSH.
>     - This type of aliasing is particularly useful when you have complex domain names or if you want to use more descriptive internal names within your Ansible playbooks and commands.