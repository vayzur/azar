# Deploy a Production Ready Apadana Cluster

## Supported Linux Distributions
- **Debian** 11, 12, 13
- **Fedora** 40, 42
- **Ubuntu** 22.04, 24.04
- **Rocky Linux** 8, 9, 10
- **Alma Linux** 8, 9, 10
- **CentOS/RHEL** 8, 9, 10
- **openSUSE** Leap 15.x/Tumbleweed

## Usage

### Install ansible
It is recommended to deploy the ansible version used by Azar into a python virtual environment.

```bash
python3 -m venv .venv
source .venv/bin/actiavte
pip install -r requirements.txt
```

### Installing the cluster
```bash
ansible-playbook -i inventory/hosts.yml cluster.yml
```

## Customize Ansible vars

Azar expects users to use one of the following variables sources for settings and customization:

| Layer                                  | Comment                                                                      |
|----------------------------------------|------------------------------------------------------------------------------|
| inventory vars                         |                                                                              |
|  - **inventory group_vars**            | most used                                                                    |
|  - inventory host_vars                 | host specific vars overrides, group_vars is usually more practical           |
| **extra vars** (always win precedence) | override with ``ansible-playbook -e @foo.yml``                               |

> [!IMPORTANT]
> Extra vars are best used to override Azar internal variables, for instances, roles/vars/. Those vars are usually **not expected** (by Azar developers) to be modified by end users, and not part of Azar interface. Thus they can change, disappear, or break stuff unexpectedly.

## Ansible tags

The following tags are defined in playbooks:

| Tag name                       | Used for                                              |
|--------------------------------|-------------------------------------------------------|
| chapar                         | Configuring Apadana apiserver                         |
| satrap                         | Configuring Apadana agents                            |
| spasaka                        | Configuring Apadana controller manager                |
| common                         | Download and installing binaries                      |

## Example commands

Example command to filter and apply only Chapar configuration tasks and skip
everything else:

```bash
ansible-playbook -i inventory/hosts.yml cluster.yml --tags chapar
```
