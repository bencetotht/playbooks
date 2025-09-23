# Garage S3 Compatible Storage Solution - Setup Playbook
> [!WARNING]
> This playbook is still under development, some features might not work yet as expected

Automated deployment of Garage storage for both a standalone and clustering mode.

## Playbook
The playbook follows the following instructions:
- update systems and ensures the necessary packages installed
- configures each node in the desired setup
- *TODO: loadbalancer setup*

## Configuration 
After the playbook completed successfully, you still need to adjust the storage setup as you would like to. Here is the list of general steps, but these may differ for you configuration.
- Create cluster layout
```bash
# create layout
garage layout assign -z <zone_name> -c 1G <node_id>
# apply layout
garage layout apply --version 1
```
> [!TIP]
> You can find out node ids with the following commnad: `garage -c /etc/garage.toml status`
- Create buckets and access keys
```bash
# create bucket
garage bucket create <bucket_name>
# generate accesskey
garage key create <key_name>
# allow access for key to bucket
garage bucket allow --read --write --owner <bucket_name> --key <key_name>
```

See more detail [here](https://garagehq.deuxfleurs.fr/documentation/quick-start/).

### Additional notes on clustering
After the playbook, you should manually connect the nodes together:
```bash
# get node id like:
garage node id
# then connect the nodes to other - this will establish communication both ways
garage node connect <output>
```

See more detail [here](https://garagehq.deuxfleurs.fr/documentation/cookbook/real-world/).

## Running the plabook
- Configure the hosts in `inventory/hosts.ini`
- Configure the variables in `inventory/group_vars/all.yaml`
- Run the playbook: 
```sh
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```
Additionally, you can define the user with the `--user` flag, or the ssh key file using the `--key-file` flag.

## To-Do
- [ ] Setup haproxy loadbalancing