# Ansible

Agentless automation tool that is installed on a single host (control node). From control node, it manages the fleet of machines remotely (managed nodes) with SSH and other transports.

## Ansible concepts
- **Control node** - A system where ansible is installed.
- **Managed node** - A remote system that is controlled by Ansible.
- **Inventory** - List of managed nodes.

## Installing Ansible
Installing ansible on Ubuntu (bionic);
```
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
