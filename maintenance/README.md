# General Maintenance Automation
> [!WARNING]
> This playbook is still under development, some features might not work yet as expected

Automated setup of DNS server coredns.

## Playbook
The playbook follows the following instructions:
- update systems and install dnsmasq to `dns` hosts
- configure dnsmasq / copy the configuation file over to each host
- *TODOD: setup keepalived / setup a virtual IP address for fault tolerance*

## Configuring
All of the configuration files can be found in the `/roles/configure/templates` folder. Currently you have to add each DNS configuration there. 

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## To-Do
- [ ] Setup keepalived and a VIP for automatic failover
- [ ] Add more depth dynamic configuration