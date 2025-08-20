# Playbooks

A collection of Ansible playbooks for infrastructure automation, various Kubernetes clusters and high-availability configurations.

## 📚 Available Playbooks

### Kubernetes Clusters
- **[RKE2](./rke2-ha/)**: Automated deployment of a highly available Kubernetes cluster using Rancher Kubernetes Engine 2.
- **[K3S](./k3s-ha/)**: Automated deployment of a highly available lightweight Kubernetes cluster using K3S.

### DNS Services
- **[BIND9](./bind9/)**: Automated setup of BIND9 DNS server with high availability using keepalived for fault tolerance.
- **[CoreDNS](./coredns/)**: Automated setup of CoreDNS server with high availability using keepalived.
- **[DNSMasq DNS](./dnsmasq-dns/)**: Lightweight DNS server setup using dnsmasq with high availability.


## 🚀 Getting Started

### Prerequisites

- Ansible 2.9+
- SSH access to target hosts
- sudo/root privileges on target hosts

### Common Usage Pattern

Each playbook follows a similar structure and usage pattern:

1. **Configure Inventory**: Edit `inventory/hosts.ini` with your target hosts
2. **Set Variables**: Configure `inventory/group_vars/all.yaml` with your environment-specific variables
3. **Run Playbook**: Execute the playbook with appropriate flags

```bash
ansible-playbook site.yaml -i inventory/hosts.ini -b --ask-become-pass
```

**Common Flags:**
- `-b` or `--become`: Enable privilege escalation
- `--ask-become-pass`: Prompt for sudo password
- `--user`: Specify SSH user
- `--key-file`: Specify SSH private key file

### Configuration

Each playbook includes:
- `ansible.cfg`: Ansible configuration with SSH optimizations
- `site.yaml`: Main playbook file
- `inventory/`: Host and variable definitions
- `roles/`: Modular role definitions for specific tasks

## 📁 Repository Structure

```
playbooks/
├── bind9/                # BIND9 DNS server automation
├── coredns/              # CoreDNS server automation
├── dnsmasq-dns/          # DNSMasq DNS server automation
├── rke2-ha/              # RKE2 high-availability cluster
├── k3s-ha/               # K3S high-availability cluster
└── README.md             # This file
```

Each subdirectory contains a complete, self-contained Ansible playbook with its own:
- Inventory configuration
- Role definitions
- Variable files
- Documentation

## 🤝 Contributing

When contributing, please:
1. Test changes in a safe environment first
2. Follow existing patterns and structure
3. Update documentation for any new features

## 📄 License

This project is open source. Please check individual playbook directories for specific licensing information.

## ⚠️ Disclaimer

These playbooks are designed for infrastructure automation and may make significant changes to your systems. Always:
- Review playbooks before execution
- Test in non-production environments first
- Ensure proper backups are in place
- Understand the implications of each role and task
