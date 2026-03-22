# Ansible Provisioning for Debian VMs on Proxmox

This repository contains an Ansible setup to provision freshly installed Debian servers.

## Create cloud-init template in Proxmox

To create a new template, copy/paste the following commands in the Proxmox console.

- Download the Debian 13 (Trixie) Cloud Image
- Creat the blank VM
- Import the new Debian 13 disk
- Attach the disk (with IO Threading enabled)
- Add Cloud-Init & Set Display
- Set boot order
- Convert to template

```
mkdir -p /tmp/cloud-init && cd /tmp/cloud-init
wget https://cloud.debian.org/images/cloud/trixie/daily/latest/debian-13-generic-amd64-daily.qcow2
qm create 1000 --name "debian-13-template" --memory 2048 --cores 2 --cpu host --net0 virtio,bridge=vmbr0
qm importdisk 1000 debian-13-generic-amd64-daily.qcow2 local-lvm
qm set 1000 --scsihw virtio-scsi-single --scsi0 local-lvm:vm-1000-disk-0,iothread=1
qm set 1000 --ide2 local-lvm:cloudinit --vga std
qm set 1000 --boot c --bootdisk scsi0
qm template 1000
```

## Clone the template to a VM

In the Proxmox CLI (where 107 is the target VM ID)

```
qm clone 1000 107 --name "rogier-test" --full true
qm set 107 --ipconfig0 ip=192.168.1.107/24,gw=192.168.1.1
qm resize 107 scsi0 16G
qm start 107
```

## Ansible configuration

- **Inventory**: The static IP addresses of your VMs are defined in `inventory/hosts.yml`.
- **SSH User**: By default, the playbook config in `inventory/hosts.yml` assumes `root`. If you configured a different user during the Debian installation (e.g., `debian`), change the `ansible_user` variable in `inventory/hosts.yml`, or pass `-u <username>` when running the playbook.

## Ansible usage

### 1. Running against defined IPs (Static Inventory)

To provision the servers defined in `inventory/hosts.yml`:

```bash
ansible-playbook playbook.yml
```

### 2. Running against an ephemeral IP

If you have spun up a temporary VM and just want to run this playbook against its IP address (e.g., `192.168.1.99`) without adding it to the static inventory, you can pass the IP directly to the `-i` flag. Don't forget the trailing comma:

```bash
ansible-playbook playbook.yml -i "192.168.1.224,"
```

## Encrypting passwords / files

Password file should be in home directory, see vault_password_file. Password is stored in password manager.

```
ansible-vault encrypt roles/ssh/templates/id_ed25519.pub.j2
ansible-vault decrypt roles/ssh/templates/id_ed25519.pub.j2
ansible-vault view roles/ssh/templates/id_ed25519.pub.j2
```

## Adding More Roles/Tasks

You can expand this setup by adding more roles in the `roles/` directory and including them in `playbook.yml`. The `common` role currently updates packages and installs basic utilities.

# Bootstrapping VMs without cloud-init

To bootstrap a freshly installed VM without cloud-init, run the following script:

```
#!/bin/bash

# Abort the script if any command fails
set -e

# check if first parameter is filled
if [ -z "$1" ]; then
    echo "Usage: $0 <ip_address>"
    echo "  Example: $0 192.168.1.224"
    echo ""
    echo "Or use \"all\" to run against all nodes in inventory"
    echo "  Example: $0 all"
    exit 1
fi

IP=$1

if [ "$IP" = "all" ]; then
    ## Install for all nodes in inventory
    echo "Installing sudo for all nodes in inventory"
    ansible all -u rlommers -k -b --become-method su -K -m apt -a "name=sudo state=present update_cache=yes"
    ansible all -u rlommers -k -b --become-method su -K -m user -a "name=rlommers groups=sudo append=yes"
    ansible all -u rlommers -k -b --become-method su -K -m copy -a "content='rlommers ALL=(ALL) NOPASSWD: ALL\n' dest=/etc/sudoers.d/rlommers mode=0440"
    echo "✅ Successfully bootstrapped all nodes in inventory!"
else    
    ## Install for specific node passed as parameter to this script
    echo "Installing sudo for node $IP"
    ansible all -i "$IP," -u rlommers -k -b --become-method su -K -m apt -a "name=sudo state=present update_cache=yes"
    ansible all -i "$IP," -u rlommers -k -b --become-method su -K -m user -a "name=rlommers groups=sudo append=yes"
    ansible all -i "$IP," -u rlommers -k -b --become-method su -K -m copy -a "content='rlommers ALL=(ALL) NOPASSWD: ALL\n' dest=/etc/sudoers.d/rlommers mode=0440"
    echo "✅ Successfully bootstrapped node $IP!"
fi
```