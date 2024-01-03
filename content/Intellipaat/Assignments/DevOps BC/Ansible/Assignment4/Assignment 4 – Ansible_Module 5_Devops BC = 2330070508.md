
> [!info] Module 5: Ansible Assignment - 4
> **Tasks To Be Performed:** 
> 1. Use the previous deployment of Ansible cluster 
> 2. Configure the files folder in the role with index.html which should be replaced with the original index.html 
> 
> All of the above should only happen on the slave which has NGINX installed using the role.

Using the role structure from [[Assignment 3 – Ansible_Module 5_Devops BC = 2330070508|Assignment 3 – Ansible]] 

**Step 1: Configure `files/index.html`** 
I place the `index.html` file that is to be deployed into the `files` directory within the role.

`index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ansible Deployment</title>
</head>
<body>
    <div class="header">
        <h1>Deployed from Ansible</h1>
    </div>
</body>
</html>
```


```bash
ubuntu@ip-10-0-1-223:~/nginx_role$ tree
.
├── README.md
├── defaults
│   └── main.yml
├── files
│   └── index.html #newly created
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── tasks
│   └── main.yml
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml

7 directories, 9 files
```



**Step 2: Update the Role's `tasks/main.yml`** 
I edit the `tasks/main.yml` file to incorporate the task that will substitute the existing `index.html` file.

```yaml
---
# tasks file for nginx_setup
- name: Gather the NGINX service facts
  service_facts: #Condition fails if not present
  
- name: Replace index.html with the custom one
  ansible.builtin.copy:
    src: index.html
    dest: /var/www/html/index.nginx-debian.html
    owner: root
    group: root
    mode: '0644'
  when: ansible_facts.services["nginx.service"] is defined and ansible_facts.services["nginx.service"].state == "running"
  notify: reload nginx
```

%%when using copy inside of role it assumes the files are in folder files

> [!attention]
> <mark style="background: #FFF3A3A6;">Handlers</mark> are used with `notify:` pay attention to when you started using handlers and the playbook has `notify:`

%%
%%
> [!attention]- Issue
> > [!fail] The condition `when:` is returns false and skipping task even though you know it is true
> > ![[Pasted image 20231106163245.png]]
> 
> > [!done] Add `service_facts:`
> > ```yaml
> > - name: Gather the NGINX service facts
> >   service_facts:
> > ```
> > 
> 

%%

^3e4b13

And the corresponding handler remains the same:
```yaml
---
# handlers file for nginx_setup

- name: reload nginx
  ansible.builtin.service:
    name: nginx
    state: reloaded
```

I'll run the same playbook from [[Assignment 3 – Ansible_Module 5_Devops BC = 2330070508#^54a359|Assignment 3 – Ansible]]

```yaml
---
- hosts: slave1
  become: yes
  roles:
    - apache_role

- hosts: slave2
  become: yes
  roles:
    - nginx_role
```

%%Dry run `ansible-playbook -i inventory.ini install_web_servers.yml --check`%%

```
ansible-playbook -i inventory.ini install_web_servers.yml 
```
![[Pasted image 20231106165755.png]]

From the terminal on Slave2 EC2, I utilize the text-based web browser Lynx to confirm the successful deployment.
```
lynx localhost
```

> [!success]
> ![[Pasted image 20231106171216.png]]
