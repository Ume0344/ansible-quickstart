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