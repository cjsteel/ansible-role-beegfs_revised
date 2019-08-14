ansible-role-beegfs
=========

Under heavy development, use at your risk

[![Build Status](https://travis-ci.org/cjsteel/ansible-role-beegfs.svg?branch=master)](https://travis-ci.org/cjsteel/ansible-role-beegfs)

The purpose of this role is to install and configure the parallel cluster file system beegfs on one or more systems.

## Acknowledgements

This role was initialized using Robert de Bock's excellent [ansible-role-skeleton](https://github.com/robertdebock/ansible-role-skeleton) and is an updated interpretation of a clone of the  [ansible-role-beegfs](https://github.com/stackhpc/ansible-role-beegfs) repository at [commit 21acbbe](https://github.com/stackhpc/ansible-role-beegfs/commit/21acbbeced9beeaa7bf16b53ac28dbebbf312b10)

## Begin Unedited Templated Documentation

[Unit tests](https://travis-ci.org/cjsteel/ansible-role-beegfs) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/cjsteel/ansible-role-beegfs/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
# Docker test:
pip install molecule ara
molecule test
# Vagrant tests
molecule test --scenario-name vagrant
```
There are many scenarios available, please have a look in the `molecule/` directory.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://cjsteel.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/cjsteel/drawings/artifacts/beegfs.png "Dependency")

Requirements
------------

- A system installed with required packages to run Ansible. Hint: [bootstrap](https://galaxy.ansible.com/cjsteel/bootstrap).
- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

## Inventory Example

```shell
[leader]
beegfs-node-01 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/beegfs-node-01/virtualbox/private_key

[follower]
beegfs-node-01 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/beegfs-node-01/virtualbox/private_key

[cluster:children]
leader
follower

[cluster_beegfs_mgmt:children]
leader

[cluster_beegfs_mds:children]
leader

[cluster_beegfs_oss:children]
leader
follower

[cluster_beegfs_client:children]
leader
follower
```



Role Variables
--------------

- beegfs_parameter: Description of values. [default: value]

Dependencies
------------

- None known.

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|yes|yes|yes|yes|yes*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes|yes|yes*|
|opensuse-leap|yes|yes|yes|yes|yes*|
|ubuntu-artful|yes|yes|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Example Playbook
----------------

```
---
- name: beegfs
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: cjsteel.bootstrap
    - role: cjsteel.beegfs
      beegfs_parameter: value
```

To install this role:
- Install this role individually using `ansible-galaxy install cjsteel.beegfs`

Sample roles/requirements.yml: (install with `ansible-galaxy install -r roles/requirements.yml
```
---
- name: cjsteel.bootstrap
- name: cjsteel.beegfs
```

### Similar roles

#### stackhcp

- [ansible-role-beegfs description](https://www.stackhpc.com/ansible-role-beegfs.html)
- [ansible-role-beegfs on ansible-galaxy](https://galaxy.ansible.com/stackhpc/beegfs)

License
-------

Apache License, Version 2.0

Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>