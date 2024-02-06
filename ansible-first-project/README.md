## Server Stats

This project takes few stats (Disk usage, uptime, Memory Usage etc) about the servers.

To run the playbook;
```
ansible-playbook -i inventory.ini playbooks/server_stats.yaml
```

To test the playbook;
```
ansible-playbook ./roles/check_server_stats/tests/main.yaml
```
