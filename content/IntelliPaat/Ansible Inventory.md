<mark style="background: #FFF3A3A6;"></mark>**Ansible Inventory**: A configuration file that lists and organizes the machines Ansible manages, potentially grouping them for easier task targeting and variable application.

<mark style="background: #FFF3A3A6;">Default inventory file used:</mark>  [[path_etc_ansible_hosts|/etc/ansible/hosts]]


> [!NOTE]- configuration file vs code file
> The Ansible inventory is primarily a **[[configuration file]]** because its primary purpose is to specify and organize the machines that Ansible manages. It's a way to define hosts and groups of hosts, along with variables associated with them.
> 
> However, it can also be thought of as a "[[code file]]" in certain advanced scenarios, especially when using dynamic inventories, which may rely on scripts or programs to generate the inventory dynamically based on external sources.
> 
> In common usage, it's best to think of the Ansible inventory as a configuration file, but it's worth noting its potential for dynamic behavior.

The inventory can be:

1. **Static**: Typically a plain-text file (default is `/etc/ansible/hosts`) which lists hostnames or IP addresses, potentially grouped by function or other criteria.
    
    Example:
```bash
[web]
webserver1.example.com
webserver2.example.com

[database]
dbserver1.example.com
```

2. **Dynamic**: A script or system that dynamically generates a list of hosts based on various sources (e.g., cloud providers, LDAP). This is useful when your infrastructure is more dynamic, and the exact list of managed nodes might change over time, such as due to autoscaling.
    

You can specify a different inventory file using the `-i` flag with the `ansible` or `ansible-playbook` command.

In addition to defining hosts and groups, the inventory can also define variables that can be used in playbooks and roles. These can be set on a per-host or per-group basis, allowing for fine-grained control over configuration settings and values specific to each host or group.
