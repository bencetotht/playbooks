# HA Redis Sentinel Cluster setup using Ansible
> [!WARNING]
> This playbook is still under development, some features might not work yet as expected.

Automated setup of a highly available Redis Cluster using Redis Sentinel.

## Playbook
The playbook follows the following instructions:
- update systems and install necessary binaries
- configure Redis and configure Redis Sentinel
- intall default metrics exporter for both Redis instances

## Configuring
Configure to your desired values in the `inventory/group_vars/all.yaml` file.

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## Extras
It is highly recommended to put the redis instances behind a load balancer to ensure automatic traffic re-routing in case of failure. 

In this case I used HAProxy, which you can setup with two configurations:
- **Option 1:** redirect all traffic to the current master node
- **Option 2:** distribute read-only traffic evenly among all nodes

Keep in mind, that only the master node can write data into the database, therefore the second option only distributes the read operations.

### Example Configuration
Option 1:
```conf
frontend redis_frontend
    bind *:6379
    mode tcp
    default_backend redis_backend

backend redis_backend
    mode tcp
    balance first
    option tcp-check
    timeout check 5s

    tcp-check send "AUTH yourPassword\r\nINFO replication\r\n"
    tcp-check expect string "role:master"

    server redis-01 192.168.88.61:6379 maxconn 1024 check inter 1s
    server redis-02 192.168.88.62:6379 maxconn 1024 check inter 1s
    server redis-03 192.168.88.63:6379 maxconn 1024 check inter 1s
```
Option 2:
```conf
frontend redis_frontend_readonly
    bind *:6380
    mode tcp
    default_backend redis_backend_readonly

backend redis_backend_readonly
    mode tcp
    balance roundrobin
    option tcp-check
    timeout check 5s

    tcp-check send "AUTH yourPassword\r\nPING\r\n"
    tcp-check expect string "PONG"

    server redis-01 192.168.88.61:6379 maxconn 1024 check inter 1s
    server redis-02 192.168.88.62:6379 maxconn 1024 check inter 1s
    server redis-03 192.168.88.63:6379 maxconn 1024 check inter 1s
```