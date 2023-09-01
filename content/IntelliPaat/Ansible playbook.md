Ansible playbook is a [[code file]] written in [[YAML (Yet Another Markup Language)]]. It defines one or multiple sequences of tasks to be executed on remote machines. Playbooks are the heart of Ansible's automation, describing the desired state and actions that Ansible should take to achieve that state on the target machines. Each task in a playbook references an Ansible module, which defines the actual operations to be performed.

An organized unit of scripts

**Playbook** have number of **plays**
**Play** contains **tasks**
**Tasks** calls core or custom **modules**
Handler gets triggered from notify and executed at the end only once.

![[Ansible Playbook Structure|900]]

