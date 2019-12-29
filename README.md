# Ansible Role: azurecli

Ansible role for installing an Azure CLI (`azure-cli`) into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-azcli.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-azcli)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

The target server requires the following packages:

  - python3
  - python3 development packages
  - python3 venv
  - gcc

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                        | Description                                                                    | Default Value        |
|---------------------------------|--------------------------------------------------------------------------------|----------------------|
| `azcli_version`                 | Use a specific version of azure-cli, eg. `2.0.78`. Specify `false` for latest. | `false`              |
| `azcli_install_dir`             | Installation directory to put azure-cli virtual environments.                  | `$HOME/.virtualenvs` |
| `azcli_current_dirname`         | Name for the currently active azure-cli Virtualenv.                            | azure-cli            |
| `azcli_install_os_dependencies` | Allow role to install OS dependencies.                                         | `false`              |
| `azcli_python3_path`            | Specify a path to a specific python version to use in virtualenv.              | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: azcli_hosts
  roles:
     - { role: xanmanning.azurecli, azcli_version: 2.0.78 }
```

Example playbook for installing the latest azure-cli version globally:

```yaml
---
- hosts: azcli_hosts
  become: true
  vars:
    azcli_install_os_dependencies: true
    azcli_install_dir: /opt/azure-cli/bin
    azcli_current_dirname: current
  roles:
    - role: xanmanning.azurecli
```

### Activating the azure-cli venv

You need to activate the python3 virtual environment to be able to access `az`.
This is done as per the below:

```bash
source {{ azure_install_dir }}/{{ azure_current_dirname }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/azure-cli/bin/current/bin/activate
```

## License

BSD

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
