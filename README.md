ansible-role-proxmox-provision
=========

[![CI](https://github.com/dtoch56/ansible-role-proxmox-provision/workflows/CI/badge.svg?event=push)](https://github.com/dtoch56/ansible-role-proxmox-provision/actions?query=workflow%3ACI)



Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

| Variable         | Description                                                          | Default  |
| ---------------- |:-------------------------------------------------------------------- |:-------- |
|                  |                                                                      |          |

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
