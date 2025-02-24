# Create VM Ansible Role

This Ansible role is designed to automate the creation of a Linux virtual machine (VM) using **virt-install**. The role supports multiple Linux distributions including **Debian**, **Ubuntu**, **Fedora**, and **Arch Linux**. It also integrates **cloud-init** to automatically configure the VM, including setting up SSH and network configurations.

---

## Features

- **Distro Options**: Supports **Debian**, **Ubuntu**, **Fedora**, and **Arch Linux**.
- **Password**: Root password is **not** set during VM creation. The user will set the root password manually by logging via ssh after the VM is created.
- **SSH**: Enables **SSH root login** for remote access.
- **Networking**: Configures DHCP for the VM to automatically obtain an IP address.
- **Cloud-Init**: Uses `cloud-init` to customize the VM (e.g., SSH key setup, user creation, and more).
- **Flexible**: Automatically adapts to the selected Linux distro with appropriate `virt-install` and `cloud-init` configurations.

---

## Requirements

- Ansible 2.9 or higher
- `virt-install` and `cloud-init` installed on the host system.
- A Linux hypervisor (e.g., KVM, libvirt) with the necessary virtual network setup (`virbr0`).
- Access to the internet for downloading cloud images (Debian, Ubuntu, Fedora, Arch).

---

## Role Variables

- `vm_name`: Name of the virtual machine (default: `"test-vm"`).
- `vm_memory`: Amount of memory to allocate to the VM (default: `4096` MB).
- `vm_vcpus`: Number of virtual CPUs to allocate (default: `2`).
- `os_variants`: A dictionary for different supported OS versions (default: `ubuntu22.04`, `debian11`, `fedora38`, `archlinux`).
- `cloud_init_iso`: Path to the cloud-init ISO (default: `/var/lib/libvirt/images/cloud-init.iso`).
- `ssh_public_key`: (Optional) Set your public SSH key to allow SSH login.

---

## Usage

1. **Clone this repository** to your project:
   ```bash
   git clone <repository-url>

2. **Add the role to your playbook**:
```bash
---
- hosts: localhost
  become: yes
  roles:
    - vm_creator
```
Or you can use the exmaple playbook.

3. **Run the playbook to create a new VM**:
```bash
ansible-playbook -K example-playbook.yml (from step 2)
```
use -K run with sudo.

4. **Post-VM Creation**:

Find the VM's IP address:
```bash
virsh net-dhcp-leases default
```

SSH into the VM:
```bash
ssh root@<VM-IP>
```
Set the root password manually:
```bash
passwd
```

## Customization

    Modify the user-data.j2 template to customize the cloud-init configuration to suit your environment.
    
    Modify the  defaults/main.yml to customize the vm ram,disk size,cpu etc.

    Modify the  vars/main.yml to add/remove/change the linux distro image of vm you would like to create.

License

MIT License. See LICENSE for more details.

This role utilizes virt-install and cloud-init to simplify VM creation and configuration on Linux-based systems.


This **README.md** file is structured to provide clear documentation on the role, how to install it, configure it, and how to use it with different Linux distributions. 
Let me know if you want any changes or additions! 🚀

