
# Intellipaat
### Lecture 8 – Ansible Role
An ansible role is group of tasks, files, and handlers stored in a standardized file structure.

Roles are small functionalities which can be used independently used but only within playbook

[[Ansible playbook]] organizes tasks
[[Ansible Role]] organizes [[Ansible playbook|playbooks]]

#### Why do we need Ansible Roles?

- Roles simplifies writing complex playbooks *(organize task into different playbooks)* *(break big task to smaller task you can call as functions)*
- Roles allows to reuse common configuration steps between different types of servers
- Roles are flexible and can be easily modified



RoleName/
├── [[Ansible Role#defaults/|defaults/]]
│   └── [[Ansible Role#Sample|main.yml]]
├── [[Ansible Role#files/|files/]]
├── [[Ansible Role#handlers/|handlers/]]
│   └── main.yml
├── [[Ansible Role#meta/|meta/]]
│   └── main.yml
├── [[Ansible Role#tasks/|tasks/]]
│   └── main.yml
├── [[Ansible Role#templates/|templates/]]
│   └── index.html.j2
├── [[Ansible Role#vars/|vars/]]
│   └── main.yml
└── [[Ansible Role#README.md|README.md]]

Structure of an ansible role consists of below given components:
	**Tasks**: Contains the main list of tasks to be executed by the role.
	**Templates**: Contains templates which can be deployed via this role.
	**Handlers**: Tasks that get triggered from some actions.
	**Vars**: Stores variables with higher priority than default variables. Difficult to override.

#### Creating an Ansible Role

1. Ansible roles should be written inside `/etc/ansible/roles/`
```bash
cd /etc/ansible/roles
```

Use the `ansible-galaxy init <role name> —offline` command to create one Ansible role

```bash
ansible-galaxy init web —offline
```


2. Use `tree` to see structure

3. Go inside task folder inside apache directory. Edit **main.yml** using sudo nano **main.yml**. Make changes as shown. Save and then exit.

```bash
sudo nano ansible/role/web/tasks/main.yml
```

```bash
---
#tasks fil for apache
- include: install.yml
- include: configure.yml
- include: service.yml
```

4. Create `install.yml`, `configure.yml` and `service.yml` to include in the `main.yml`.  Keeping install, configure and service files separately helps us reduce complexity.

To install apache2 in the remote machine `ansible/role/web/tasks/install.yml`
```bash
---
  — name: install apache2
    apt: name=apache2 update_cache=yes state=latest
```


5. To configure the `apache2.conf` fiIe and to send copy.html file  to the remote machine. Add notify too, based on which handlers will get triggered
`ansible/role/web/tasks/configure.yml`

```bash
---
  - name: Configure Website
    copy: src=index.html dest=/var/www/html
    notify:
      - restart apache2 service
  - name: send copy.html file
```

^c78b76

> [!tip] How Handler would look
> *Had to include it myself*
> `handlers/main.yml`
> ```bash
> ---
> - name: restart apache2 service
>   service:
>     name: apache2
>     state: restarted
> ```
> 

6. To start apache2 service in  the remote machine
`ansible/role/web/tasks/service.yml`

```bash
---
  - name: starting apache2 service
    service: name=apache2 state=started
```

7. Go inside meta and add information related to the role
   Add author information, role descriptions, company information etc
`ansible/role/web/meta/main.yml`

8. Go to the `/etc/ansible/` and create one top level file where we can add [[Ansible Host|hosts]] and roles to be executed

   Execute apache role on the hosts that is under the group name servers, added in the inventory file [[path_etc_ansible_hosts|/etc/ansible/hosts]]

also add [[site.yaml]]

```bash
---
  - hosts: servers
    roles:
     - web
```

9. Before we execute our [[Ansible Playbook Structure|top level yml]] file we will check for syntax errors.
```bash
ansible-playbook <filename.yml> --syntax-check
```

10. Execute the top level yml  file. 
```bash
ansible-playbook <filename.yml>
```

### Lecture 9 – Using Roles In Playbook

Mentions `ansible-galaxy` how it creates skeleton for your role

Also mentions how a role is just breaking 1 big playbook into folder variables, tasks. Cuse those you can define all in one playbook

[[Jinja]] is a sperate tool but Ansibles uses to generate documents

> [!NOTE]- Mentioned `ansible_fqdn` used in httpd.conf.j2
> In Ansible, `ansible_fqdn` is a special variable that represents the [[FQDN (Fully Qualified Domain Name)]] of the target host. It's part of Ansible's built-in "facts" or "variables" that are automatically discovered when gathering facts about a host.
> 
> When you run a playbook or an ad-hoc command with fact gathering enabled (which is the default behavior), Ansible will collect various pieces of information about the target hosts, known as "facts". These facts include system characteristics, like its IP address, hostname, operating system type/version, and more.
> 
> Specifically:
> 
> - `ansible_fqdn`: This variable contains the FQDN of the host, which is usually the hostname combined with the domain name. For example: `host1.example.com`.
>     
> - `ansible_hostname`: This variable contains just the hostname of the machine. For the above example, it would be `host1`.
>     
> 
> If you're writing playbooks or roles and want to use the FQDN of the machine for some tasks (like configuring a software that requires the FQDN), you can utilize the `ansible_fqdn` variable.


Calling the role *(no continuity to previous Lecture)*
```bash
— name : This playbook invoke the Ansible role
  hosts: webservers
  gather_facts: True
  roles:
    - apache
  vars:
    apache_name: Kelly
    apache _ port: 91
```
*Notice you will override some variables in vars and default folder*

# Others
#chat
### defaults/ 
This directory contains the default values for role variables. They have the lowest priority of any variables available and can be easily overridden by any other variable, including inventory variables.
#### Sample
`defaults/main.yml`

```yaml
---
# default value for webserver package
webserver_package: apache2
```

### files/
This directory contains static files which you want to be copied to the systems you are managing. No templating happens here.
#### Sample
n/a
### handlers/
Handlers are special tasks in Ansible that run only when notified by another task. Unlike regular tasks, which run in the order they are defined, handlers are executed once, after all of the tasks are completed. They are typically used for activities that need to be executed conditionally based on changes in the system – most commonly, restarting services. Think of them as triggered actions: they only run if something in the playbook explicitly "calls" or "notifies" them.

For example, you may not want to restart a service every time a playbook runs, but only when a specific configuration file changes. In such a scenario, you'd use a handler. The main task would make changes to the configuration file and then "notify" the handler to restart the service only if changes were actually made.

[[Ansible Role#^c78b76|Example above using notify:]]
#### Sample
`handlers/main.yml`

```yaml
---
- name: restart webserver
  service:
    name: "{{ webserver_package }}"
    state: restarted

```
### meta/
The metadata can include details such as the role's author, the supported platforms, dependencies (other roles required to run the role), and more.
#### Sample
`meta/main.yml`

```yaml
---
galaxy_info:
  author: "John Doe"
  description: "Setup and configure a web server."
  company: "Tech Inc."
  license: "MIT"
  min_ansible_version: 2.4
  platforms:
    - name: Ubuntu
      versions:
        - trusty
        - xenial
        - bionic
    - name: EL (Red Hat/CentOS)
      versions:
        - 7
        - 8
  galaxy_tags:
    - web
    - server
    - nginx
    - apache
dependencies:
  - { role: 'common', version: '2.0.0' }
  - { role: 'database', db: 'mysql' }
```

> [!NOTE]- Description of the metadata fields
> 1. **galaxy_info**: This section provides metadata information that can be particularly useful if you're sharing your role on Ansible Galaxy, a shared repository of Ansible roles.
>     
>     - **author**: The name of the person or organization that created and maintains the role.
>     - **description**: A short description of what the role does.
>     - **company**: (Optional) The name of the company the author belongs to.
>     - **license**: The license for this role (e.g., MIT, GPL, etc.).
>     - **min_ansible_version**: The minimum Ansible version required to run the role.
>     - **platforms**: List of operating systems the role supports.
>     - **galaxy_tags**: Keywords/tags that help in categorizing and searching for the role in Ansible Galaxy.
> 2. **dependencies**: Roles that must be run before the current role. This is useful when the functionality of one role depends on another role. For instance, a role that sets up a web application might depend on another role that sets up a database.

Remember, these are just sample fields. Depending on the use case, more fields can be added, or some of them might be omitted.
### tasks/
The series of tasks to be executed by the role. These tasks can call modules, and they can also loop and use conditionals.
#### Sample
`tasks/main.yml`

```yaml
---
- name: install webserver
  apt:
    name: "{{ webserver_package }}"
    state: present
  notify:
    - restart webserver
```

### templates/
Jinja2 template files, which use variables to substitute information and can be deployed to managed systems.
#### Sample
`templates/index.html.j2`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to {{ ansible_hostname }}</title>
</head>
<body>
<h1>Hello, this is served from {{ ansible_hostname }}</h1>
</body>
</html>
```

> [!tip]- How to use
> If you have a Jinja2 template named `index.html.j2` and you'd like to render it to a target system using Ansible, you'd use the `template` module instead of the `copy` module.
> 
> Here's how you would modify your task to use the `templates/index.html.j2`:
> 
> ```bash
> ---
>   - name: Configure Website using Template
>     template:
>       src: templates/index.html.j2
>       dest: /var/www/html/index.html
>     notify:
>       - restart apache2 service
>   - name: send copy.html file
>     # (whatever this task does goes here)
> ```

### vars/
Variables for the role. These have a higher precedence than default variables.
#### Sample
`vars/main.yml`

```yaml
---
# Variable overridden for a specific environment
webserver_package: nginx

```

### README.md
A text file that provides all necessary information about the role, its purpose, and how it's used. This is especially helpful when sharing the role with others or when revisiting a role after a period of time.