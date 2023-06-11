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

An Ansible role to prepare your host to work with Ansible.

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
#prepare_host_sudoers:
#  - "testuser"

prepare_host_packages_removed:
  - "vim*"
  - "vi*"

prepare_host_packages_installed:
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
  - "initscripts"
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
  - "iproute2

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_prepare_host_sudoers:
  - "testuser"

inv_prepare_host_packages_removed:
  - "vim*"
  - "vi*"

inv_prepare_host_packages_installed:
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
  - "initscripts"
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
    prepare_host_sudoers: "{{ inv_prepare_host_sudoers }}"
    prepare_host_packages_removed: "{{ inv_prepare_host_packages_removed }}"
    prepare_host_packages_installed: "{{ inv_prepare_host_packages_installed }}"
    ansible.builtin.include_role:
    name: "labocbz.prepare_host"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-04-27: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez

### 2023-04-28: Update / Clean and autoremove packages

* Added an update / clean / autoremove / purge task

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
