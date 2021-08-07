ansible-role-proxmox-provision
=========

[![CI](https://github.com/dtoch56/ansible-role-proxmox-provision/workflows/CI/badge.svg?event=push)](https://github.com/dtoch56/ansible-role-proxmox-provision/actions?query=workflow%3ACI)



Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml).

## Template

| Variable                                  | Description                                                        | Default                                      |
| ----------------------------------------- |:------------------------------------------------------------------ |:-------------------------------------------- |
| proxmox_provision_template_img_url        | Cloud-init image url to download for creating template             | .../focal-server-cloudimg-amd64-disk-kvm.img |
| proxmox_provision_template_img_redownload | Force download cloud-init image (if image already exist on server) | false                                        |
| proxmox_provision_template_image          | Downloaded image file name                                         | focal-server-cloudimg-amd64-disk-kvm.img     |
| proxmox_provision_template_ostype         | Operating system type                                              | l26                                          |
| proxmox_provision_template_name           | Template name                                                      | Ubuntu2004Kvm                                |
| proxmox_provision_template_description    | Template description                                               | Ubuntu 20.04 KVM Disk                        |
| proxmox_provision_template_storage        |                                                                    | local                                        |
| proxmox_provision_template_recreate       |                                                                    | false                                        |
| proxmox_provision_template_iso_path       | Path to                                                            | /var/lib/vz/template/iso                     |
| proxmox_provision_template_id             | Proxmox VM ID for template                                         | 999                                          |
| proxmox_provision_template_bridge         | Bridge name to use in VM template                                  | vmbr1                                        |
| proxmox_provision_snippets_path           | Path to snippets directory                                         | /var/lib/vz/snippets                         |

## Cloud-init default user

| Variable                             | Description                                 | Default                         |
| ------------------------------------ |:------------------------------------------- |:------------------------------- |
| proxmox_provision_user               | User account name                           | ansible                         |
| proxmox_provision_user_uid           | User identifier (UID)                       | 1099                            |
| proxmox_provision_user_hashed_passwd | SHA512 password hash                        | ""                              |
| proxmox_provision_user_passwd        | User password (if hashed password is empty) | 7B6FMJHjVc9B4aFS                |
| proxmox_provision_user_ssh_keys      | Authorized ssh keys for account             | []                              |
| proxmox_provision_user_home          | Home directory path                         | /home/ansible                   |
| proxmox_provision_user_shell         | Default shell                               | /bin/bash                       |
| proxmox_provision_user_nopass_sudo   | Allow to use sudo without password          | False                           |
| proxmox_provision_user_lock_password | Lock user account                           | false                           |
| proxmox_provision_user_gecos         | General information about the account       | Ansible user                    |
| proxmox_provision_user_group         | User group identifier (GID)                 | anible                          |
| proxmox_provision_user_groups        | User groups                                 | adm, sudo, plugdev, dip, netdev |

## Cloud-init users (proxmox_provision_users: {})

| Variable    | Description                     | Default   |
| ----------- |:------------------------------- |:--------- |
| name        | User account name               |           |
| uid         | User identifier (UID)           |           |
| gecos       |                                 |           |
| shell       |                                 | /bin/bash |
| group       |                                 |           |
| lock_passwd |                                 | false     |
| password    |                                 |           |
| sudo        |                                 | false     |
| ssh_keys    | Authorized ssh keys for account | []        |

## Proxmox API variables

| Variable                       | Description                               | Default |
| ------------------------------ |:----------------------------------------- |:------- |
| proxmox_provision_api_host     |                                           |         |
| proxmox_provision_api_user     |                                           |         |
| proxmox_provision_api_password |                                           |         |
| proxmox_provision_kvm_defaults |                                           |         |

## Local subnetwork

| Variable     | Description                                                          | Default    |
| ------------ |:-------------------------------------------------------------------- |:---------- |
| ip           |                                                                      | 10.0.0.0   |
| cidr         |                                                                      | 24         |
| host         |                                                                      | 10.0.0.1   |
| nameserver   |                                                                      | 10.0.0.254 |
| gateway      |                                                                      | 10.0.0.1   |
| searchdomain |                                                                      | test.local |

## KVM list for provisioning (proxmox_provision_kvms: {})
| Variable             | Description        | Default                                      |
| ---------------------|:------------------ |:-------------------------------------------- |
| vmid                 |                    |                                              |
| clone_vm             |                    |                                              |
| name                 |                    |                                              |
| description          |                    |                                              |
| storage              |                    | {{ proxmox_provision_kvm_defaults.storage }} |
| network              |                    |                                              |
| network.ip           |                    |                                              |
| network.cidr         |                    | {{ local_subnetwork.cidr }}                  |
| network.gateway      |                    | {{ local_subnetwork.gateway }}               |
| network.nameserver   |                    | {{ local_subnetwork.nameserver }}            |
| network.searchdomain |                    | {{ local_subnetwork.searchdomain }}          |
| cores                |                    |                                              |
| sockets              |                    |                                              |
| memory               |                    |                                              |
| disksize             |                    |                                              |
| update               |                    | True                                         |
| onboot               |                    | True                                         |

## LXC list for provisioning (proxmox_provision_lxcs: {})
| Variable             | Description                                                          | Default  |
| -------------------- |:-------------------------------------------------------------------- |:-------- |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: dtoch56.proxmox_provision }

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2021 by DToch.

Development
------------------

    pip install pipenv
    pipenv install
