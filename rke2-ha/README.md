# Highly-Available RKE2 Cluster using HAProxy and keepalived
Automated deployment of a highly available Kubernetes cluster using Rancher Kubernetes Engine 2.


The playbook also includes the following applications:
- [MetalLB](https://metallb.io/) for loadbalancing
- [Traefik](https://traefik.io/traefik/) for a reverse proxy
- [Longhorn](https://longhorn.io/) for native distributed block storage

## Playbook
The playbook follows the following instructions:
- configures loadbalancers using haproxy and keepalived
- prepares the cluster nodes: install updates, packages, dependencies, enable IPv4 and 6 forwarding
- configures RKE2 servers and agents
- installs cluster manifests: MetalLB, Traefik, Longhorn
> *optionally, you can change the `manifests_dir` value in the configuration file to the rke2 directory so that each component will be installed at the cluster start*
- install RKE2
- start the RKE2 service on all servers

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
