# Vault

[![Build Status](https://travis-ci.org/brianshumate/ansible-vault.svg?branch=master)](https://travis-ci.org/brianshumate/ansible-vault)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-brianshumate.vault-blue.svg)](https://galaxy.ansible.com/brianshumate/vault/)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/brianshumate/ansible-vault.svg)](http://isitmaintained.com/project/brianshumate/ansible-vault "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/brianshumate/ansible-vault.svg)](http://isitmaintained.com/project/brianshumate/ansible-vault "Percentage of issues still open")

This Ansible role performs a basic [Vault](https://vaultproject.io/)
installation, including filesystem structure and example configuration.

It can also bootstrap a minimal development or evaluation server or HA
Consul-backed cluster in a Vagrant and VirtualBox based environment. See
[README_VAGRANT.md](https://github.com/brianshumate/ansible-vault/blob/master/examples/README_VAGRANT.md) and the associated [Vagrantfile](https://github.com/brianshumate/ansible-vault/blob/master/examples/Vagrantfile) for more details about the developer mode setup.

## Requirements

This role requires a Debian or RHEL based Linux distribution. It might work
with other software versions, but does work with the following specific
software and versions:

* Ansible: 2.1.2.0
* Vault: 0.6.2
* Debian: 8

## Role Variables

The role defines variables in `defaults/main.yml`:

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `vault_version` | `0.6.2` | Version to install |
| `vault_zip_url` | `https://releases.hashicorp.com/vault/{{ vault_version }}/vault_{{ vault_version }}_linux_amd64.zip` | Download URL |
| `vault_zip_sha256` | SHA256 SUM | Archive SHA256 summary |
| `vault_bin_path` | `/usr/local/bin` | Binary installation path |
| `vault_config_path` | `/etc/vault.d` | Configuration file path |
| `vault_data_path` | `/var/vault` | Data path |
| `vault_log_path` | `/var/log/vault` | Log path |
| `vault_user` | `vault` | OS user |
| `vault_group` | `bin` | OS group |
| `vault_datacenter` | `dc1` | Datacenter label |
| `vault_log_level` | `INFO` | Log level |
| `vault_syslog_enable` | `true` | Log to syslog |
| `vault_iface` | `eth1` | Network interface |
| `vault_address` | `{{ hostvars[inventory_hostname]['ansible_eth1']['ipv4']['address'] }}` | Primary interface address |
| `vault_port` | `8200` | TCP port number to use |
| `vault_node_name` | `{{ inventory_hostname_short }}` | Short node name |
| `vault_main_config` | `{{ vault_config_path }}/vault_main.hcl` | Main configuration file path |
| `vault_consul` | `127.0.0.1:8500` | Address of Consul backend |
| `vault_consul_path` | `vault` | Consul path to use |

### OS Distribution Variables

The `consul` binary works on most Linux platforms and is not distribution
specific. However, some distributions require installation of specific OS
packages with different naming, so this role was built with support for
popular Linux distributions and defines these variables to deal with the
differences acros distros:

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `vault_pkg` | `{{ vault_version }}_linux_amd64.zip` | Vault package filename |
| `vault_centos_url` | `{{ vault_zip_url }}` | Vault package download URL |
| `vault_sha256` | SHA256 SUM | Vault download SHA256 summary |
| `vault_centos_os_packages` | list | List of OS packages to install |
| `vault_pkg` | `{{ vault_version }}_linux_amd64.zip` | Vault package filename |
| `vault_debian_url` | `{{ vault_zip_url }}` | Vault package download URL |
| `vault_sha256` | SHA256 SUM | Vault download SHA256 summary |
| `vault_debian_os_packages` | list | List of OS packages to install |
| `vault_pkg` | `{{ vault_version }}_linux_amd64.zip` | Vault package filename |
| `vault_redhat_url` | `{{ vault_zip_url }}` | Vault package download URL |
| `vault_sha256` | SHA256 SUM | Vault download SHA256 summary |
| `vault_redhat_os_packages` | list | List of OS packages to install |
| `vault_pkg` | `{{ vault_version }}_linux_amd64.zip` | Vault package filename |
| `vault_ubuntu_url` | `{{ vault_zip_url }}` | Vault package download URL |
| `vault_sha256` | SHA256 SUM | Vault download SHA256 summary |
| `vault_ubuntu_os_packages` | list | List of OS packages to install |

## Dependencies

Ansible requires GNU tar and this role performs some local use of the
unarchive module, so ensure that your system has `gtar` installed.

## Example Playbook

Basic installation is possible using the included `site.yml` playbook:

```
ansible-playbook -i hosts site.yml
```

You can also pass variables in using the `--extra-vars` option to the
`ansible-playbook` command:

```
ansible-playbook -i hosts site.yml --extra-vars "vault_datacenter=maui"
```

### Vagrant and VirtualBox

See `examples/README_VAGRANT.md` for details on quick Vagrant deployments
under VirtualBox for testing, etc.

## License

BSD

## Author Information

[Brian Shumate](http://brianshumate.com)

## Contributors

Special thanks to the folks listed in [CONTRIBUTORS.md](https://github.com/brianshumate/ansible-vault/blob/master/CONTRIBUTORS.md) for their
contributions to this project.
