# Proxmox VM Role

## Description

This Ansible role creates a virtual machine on a Proxmox host.

## Requirements

* Ansible 2.9 or higher
* The `community.general` Ansible collection (version 8.0.0 or higher). Install with:
    `ansible-galaxy collection install -r roles/ansible_role_create_pve_vm/requirements.yml`

## Role Variables

###   Defaults

The following variables are defined in `defaults/main.yml`:

    proxmox_host: "your_proxmox_host" # The Proxmox host
    proxmox_user: "your_proxmox_user" # The Proxmox username
    proxmox_password: "your_proxmox_password" # The Proxmox password (NOT FOR GIT)
    proxmox_node: "pve" # The Proxmox node
    vm_id: 100 # The VM ID
    vm_name: "my-new-vm" # The VM name
    vm_memory: 2048 # The VM memory in MB
    vm_cpus: 2 # The number of vCPUs
    vm_disk_size: "32G" # The VM disk size (e.g., "32G", "100G")
    vm_storage: "local-lvm" # The storage pool for the VM's disk
    ostemplate: "local:vztmpl/ubuntu-22.04-standard_22.04-1_amd64.tar.gz" # The OS template to use
    # vm_ip: "192.168.1.150/24" # Optional static IP address
    # vm_gateway: "192.168.1.1" # Optional gateway
    # vm_bridge: "vmbr0" # Optional network bridge

### Variables for Git

The following variables are defined in `vars/main.yml` and are safe to commit to Git:

    vm_name: "my-vm"
    vm_cpus: 2
    vm_memory: 2048
    vm_disk_size: "32G"
    vm_id: 100
    ostemplate: "local:vztmpl/ubuntu-22.04-standard_22.04-1_amd64.tar.gz"
    vm_storage: "local-lvm"

### Sensitive Variables

The following sensitive variables should be placed in your playbook:

    proxmox_host: "your_proxmox_host"
    proxmox_user: "your_proxmox_user"
    proxmox_password: "your_secure_proxmox_password"

**Note:** Sensitive variables, such as passwords, should be passed directly into your playbook and not committed to version control.

## Usage

1.  Install the role and its dependencies:

    ```bash
    ansible-galaxy role install ansible_role_create_pve_vm
    ansible-galaxy collection install -r roles/ansible_role_create_pve_vm/requirements.yml
    ```

2.  Create a playbook that uses the role:

    ```yaml
    ---
    - hosts: localhost
      connection: local
      vars:
        proxmox_host: "your_proxmox_host"
        proxmox_user: "your_proxmox_user"
        proxmox_password: "your_secure_proxmox_password"
        vm_name: "my-new-vm"
        vm_cpus: 4
        vm_memory: 4096
        vm_disk_size: "100G"
        vm_id: 105
        vm_storage: "your_storage_pool" # Set this to your desired storage.
      roles:
        - ansible_role_create_pve_vm
    ```

3.  Run the playbook:

    ```bash
    ansible-playbook your_playbook.yml
    ```
