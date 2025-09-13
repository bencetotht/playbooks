# HAProxy Configuration Playbook
> [!WARNING]
> This playbook is still under development, some features might not work yet as expected

Automated rollout of HAProxy configuration to multiple nodes.

## Playbook
The playbook follows the following instructions:
- update systems and ensures the packages `haproxy` and `keepalived` are installed
- copies the configuration to each node
- *TODO: keepalived setup*

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Provide your `haproxy.cfg` file at `roles/configure/templates/haproxy.cfg`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## To-Do
- [ ] Setup keepalived