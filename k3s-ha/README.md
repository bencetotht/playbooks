# Highly-Available K3S Cluster using HAProxy and keepalived
Automated deployment of a highly available Kubernetes cluster using K3S.

## Playbook
The playbook follows the following instructions:
- prepares the cluster nodes: install updates, packages, dependencies
- configures loadbalancers using keepalived and HAProxy
- install K3S

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## To-Do
- [ ] Create a new user and provide the user with the `.kubeconfig` file
---
Credit: Based on the [k3s-ansible](https://github.com/techno-tim/k3s-ansible) playbook by [TechnoTim](https://github.com/techno-tim)