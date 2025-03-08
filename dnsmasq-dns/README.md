# DNSMASQ setup using Ansible
Automated setup of DNS server dnsmasq. The dns entries are in the `roles/configure-dnsmasq/templates/dnsmasq.conf.j2` file. 

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## To-Do
- [ ] Take DNS entries from the group_vars file.