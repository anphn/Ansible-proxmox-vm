![docker hub](https://img.shields.io/docker/pulls/richarvey/nginx-php-fpm.svg?style=flat-square)
![docker hub](https://img.shields.io/docker/stars/richarvey/nginx-php-fpm.svg?style=flat-square)
![Travis](https://img.shields.io/travis/ngineered/nginx-php-fpm.svg?style=flat-square)

# ansible-role-proxmox-vm

## Overview

Ansible role - manage VM via Proxmox API for Kiotviet (clone, configure, start, stop and remove).

Tags:  

  - **create:** clone, configure and start the VM
  - **stop:** stop the VM
  - **update:** stop, reconfigure and start the VM
  - **destroy:** stop and remove the VM
  - **status:** get the current status of the VM

## Getting started with an example

### Configure

Edit `proxmox-vm/vars/main.yml`:  

```yaml
---
# default vars file for proxmox-vm
proxmox_host: proxmox.lan
proxmox_user: root@pam
proxmox_password: password
proxmox_storage: hq_citigo
```

### Run

`playbook.yml`:  

```yaml
- hosts: localhost
  connection: local
  gather_facts: false

  roles:
    - proxmox-vm
```

Running playbook:  

```bash
# create VM from template
ansible-playbook playbook.yml
# destroy VM
ansible-playbook playbook.yml --tags destroy
```

## Variables

### Required

| Name | Type | Description |
| --- | --- | --- |
| `proxmox_host` | string | Proxmox IP address or hostname (ex: `192.168.0.10`, `proxmox.lan`) |
| `proxmox_user` | string | Proxmox user (ex: `root@pam`, `admi@pve`) |
| `proxmox_password` | string | Proxmox user password |
| `node` | string | node name (ex: `node1`) |
| `vm_name` | string | VM name. If `vm_vmid` is setted, it is not required |
| `vm_vmid` | int | VMID (`100-N`). If `vm_name` is setted, it is not required |

### Optional

| Name | Type | Description |
| --- | --- | --- |
| `node` | string | node run VM |
| `template_name` | string | template name. If `template_vmid` is setted, it can take arbitrary value |
| `template_id` | string | template VMID (100-N)|

| `vm_user` | string | user name (*cloud-init required*) |
| `vm_password` | string | user password (*cloud-init required*) |
| `vm_sshkeys` | list of string | list of public SSH keys (OpenSSH format - *cloud-init required*) |
| `vm_ipconfig0` | string | Ip address and gateway (ex: `ip=192.168.0.20/24,gw=192.168.0.254` - *cloud-init required*) |
| `vm_nameserver` | string | DNS server IP address (ex: `8.8.8.8 8.8.4.4` - *cloud-init required*) |
| `vm_searchdomain` | string | DNS search domains (ex: `google-public-dns-a.google.com` - *cloud-init required*) |
| `vm_sockets` | int | the number of CPU sockets (ex: `2`) |
| `vm_cores` | int | the number of cores per socket (ex: `2`) |
| `vm_memory` | int | amout of RAM for the VM in `MB` (ex: `512`, `1024`, `2048`) |
| `vm_disksize` | string | the extend disk size (ex: `+20G`, `+1T`). Default root disk is scsi0 |
| `vm_netbrigde` | string | Network brigde vlan |

For more detailed examples and explanations please refer to the documentation.
## Documentation
- [Proxmox-api](https://pve.proxmox.com/pve-docs/api-viewer)
