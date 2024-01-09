# Ansible

Agentless automation tool that is installed on a single host (control node). From control node, it manages the fleet of machines remotely (managed nodes) with SSH and other transports.

## Ansible concepts
- **Control node** - A system where ansible is installed.
- **Managed node** - A remote system that is controlled by Ansible.
- **Inventory** - List of managed nodes.

## Installing Ansible
Installing ansible on Ubuntu (bionic);
```
sudo apt update && \
sudo apt install software-properties-common && \
sudo add-apt-repository --yes --update ppa:ansible/ansible && \
sudo apt install ansible
```

## Inventory (.ini file)

1- Make sure the control node can SSH into managed nodes.

2- Add list of managed nodes in `inventory.ini` file.

3- Verify the inventory;
```
ansible-inventory -i inventory.ini --list
```

4- Ping `p4kubehosts` group in inventory.
```
ansible p4kubehosts -m ping -i inventory.ini
```

## Playbooks
**Module** - A unit of code (commands) that ansible runs on managed nodes.

**Task** - A list of one or more modules.

**Play** - An ordered list of tasks that run on managed nodes in inventory.

**Playbook** - A list of plays to define the order in which ansible performs plays (from top to bottom).

Run a playbook;
```
ansible-playbook -i <inventory_name> <playbook_namel.yaml> . i.e, 
ansible-playbook -i inventory.ini playbook.yaml
```

## Roles
A role is way to package related tasks, handlers, variables etc to them re-usable. This allows us to group related tasks together to ensure reusability and maintainability.
a `roles/` directory is created relative to a playbook.

## Group Variables
Variables applied to groups of servers that can be used is playbooks. Directory to store group variables is `group_vars`. Inside this directory, we have `all` file variables are applicable for all servers mentioned in an inventory. 

The file names inside this directory are named after host groups. For example, if we have a host group named `p4kubeservers`, we have file `group_vars/p4kubeservers`. This file will contain all the varibales that are needed for `p4kubeservers`.

Variables can be used in playbooks like;
```
# adminpass is a variabale
{{ adminpass }}
```

## Jinja
Ansible uses Jinja2, a text-based template language for python, to create dynamic configurations. It allows users to use varibales, loops, conditionals in playbooks.

Forexample, the for loop is executed like this in Jinja2;
```
{% for item in items %}
  {{ item }}
{{% endfor %}}
```

## Concepts relevant to plays

### Parallel Execution
Ansible can execute operations on number of servers in parallel. `serial` is used to define how many servers should be configured in parallel.

```
serial: 1 # Ansible run the operations on 1 server at a time.
serial: 10 # Ansible run the operations on 10 servers at a time parallely.
```

### Pre and post tasks
`pre_tasks` lets you run some tasks (pre-configurations) before roles are executed. 
`post_tasks` lets you run some tasks after roles are executed. 
