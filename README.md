# Ansible role: labocbz.prepare_host

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Cbz-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: Prepare](https://img.shields.io/badge/Tech-Prepare-orange)
![Tag: Sudoers](https://img.shields.io/badge/Tech-Sudoers-orange)

An Ansible role to prepare your host to work with Ansible.

The Host Preparation role automates the process of preparing a target host for desired configurations. It handles package management, user and group creation, and sudoer management. This role helps streamline the initial setup process and ensures consistency across hosts.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
#prepare_host__users:
#  - login: "root"
#    group: "root"
#    uid: 1
#    gid: 1
#    sudoer: true
#    password: "secret"

#prepare_host__system_users:
#  - login: "www-data"
#    group: "www-data"
#    uid: 33
#    gid: 33

#prepare_host__packages_removed:
#  - "vim*"
#  - "vi*"

#prepare_host__packages_installed:
#  - "rsync"
#  - "curl"
#  - "python3"
#  - "python3-jmespath"
#  - "python3-pip"
#  - "python3-lxml"
#  - "libssl-dev"
#  - "libffi-dev"
#  - "git"
#  - "wget"
#  - "lsb-release"
#  - "gnupg2"
#  - "software-properties-common"
#  - "apt-transport-https"
#  - "ca-certificates"
#  - "sudo"
#  - "nano"
#  - "net-tools"
#  - "procps"
#  - "openssl"
#  - "lsof"
#  #- "initscripts"
#  - "zip"
#  - "tree"
#  - "python3-apt"
#  - "python3-pip"
#  - "python3-setuptools"
#  - "iftop"
#  - "htop"
#  - "cron"
#  - "virtualenv"
#  - "nethogs"
#  - "iproute2"
#  - "iptables"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_prepare_host__users:
  - login: "root2"
    group: "root2"
    uid: 1000
    gid: 1000
    sudoer: true
    password: "secret"

inv_prepare_host__system_users:
  - login: "www-data2"
    group: "www-data2"
    uid: 3333
    gid: 3333

inv_prepare_host__packages_removed:
  - "vim*"
  - "vi*"

inv_prepare_host__packages_installed:
  - "rsync"
  - "curl"
  - "python3"
  - "python3-jmespath"
  - "python3-pip"
  - "python3-lxml"
  - "libssl-dev"
  - "libffi-dev"
  - "git"
  - "wget"
  - "lsb-release"
  - "gnupg2"
  - "software-properties-common"
  - "apt-transport-https"
  - "ca-certificates"
  - "sudo"
  - "nano"
  - "net-tools"
  - "procps"
  - "openssl"
  - "lsof"
  - "zip"
  - "tree"
  - "python3-apt"
  - "python3-pip"
  - "python3-setuptools"
  - "iftop"
  - "htop"
  - "cron"
  - "virtualenv"
  - "nethogs"
  - "iproute2"
  - "iptables"

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.prepare_host"
  tags:
    - "labocbz.prepare_host"
  vars:
    prepare_host__users: "{{ inv_prepare_host__users }}"
    prepare_host__packages_removed: "{{ inv_prepare_host__packages_removed }}"
    prepare_host__packages_installed: "{{ inv_prepare_host__packages_installed }}"
    prepare_host__system_users: "{{ inv_prepare_host__system_users }}"
  ansible.builtin.include_role:
    name: "labocbz.prepare_host"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

### 2023-04-28: Update / Clean and autoremove packages

* Added an update / clean / autoremove / purge task

### 2023-06-11: Open Sources and Cache Update

* Moove into a new repos for open sources
* Adding codeowners
* Adding group and user creation
* Adding more simple pipeline for testing
* Remonving autoremove / purge / dist upgrade because RedHat ubi8 (YUM) is not compatible

### 2023-06-25: Refactoring vars

* Sudoers and users are in the same liste

### 2023-10-06: New CICD, new Images

* New CI/CD scenario name
* Molecule now use remote Docker image by Lord Robin Crombez
* Molecule now use custom Docker image in CI/CD by env vars
* New CICD with needs and optimization

### 2023-12-14: System users

* Role can now create system users and address groups

### 2023-12-17: Iptables

* Role create now a cron job to save iptables rules
* Role also create a cron job to restore iptables rules

### 2023-02-18: New CICI and fixes

* Added support for Ubuntu 22
* Added support for Debian 11/22
* Edited vars for linting (role name and __)
* Added generic support for Docker dind (can add used for obscures reasons ... user in use)
* Fix idempotency
* Added informations for UID and GID for user/groups
* Added support for user password creation (on_create)
* New CI, need work on tag and release

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
