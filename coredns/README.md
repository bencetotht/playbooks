# DNSMASQ setup using Ansible
> [!WARNING]
> This playbook is still under development, some features might not work yet as expected

Automated setup of DNS server dnsmasq. The dns entries are in the `roles/configure-dnsmasq/templates/dnsmasq.conf.j2` file. 

## Playbook
The playbook follows the following instructions:
- update systems and install dnsmasq to `dns` hosts
- configure dnsmasq / copy the configuation file over to each host
- setup keepalived / setup a virtual IP address for fault tolerance

## Configuring
If you would like to use RFC2136 Dynamic Updates, update the Corefile to look like the following:
```conf
example.com {
  auto /etc/coredns/zones {
    reload 15s
    transfer to *
  }
  log
  errors
}

.:53 {
  forward . 1.1.1.1 8.8.8.8
  log
  errors
}
```

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## Test
You can test the service working by running the following commands:
```bash
# on the dns server
coredns -conf Corefile
# on your host
dig @127.0.0.1 www.example.com
```