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
