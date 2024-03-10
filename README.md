# Ollama Ansible Collection

## Overview

Use this Ansible Collection to provision [Ollama](https://ollama.com/) on your system

## Requirements

### Ansible Version

This collection requires ansible from version `2.14.0` and above

### Collections

This collection depends on the following collections:
- community.general: "*"
- containers.podman: "*"
- kubernetes.core: "*"

## Roles

The collection includes a single role

- [`ollama`](./roles/ollama/README.md) - Install and configure `Ollama`

## Installation Playbook

The collection includes a playbook for the installation
- [install](./playbooks/install.yml) for provisioning ollama with an insecure port. By default, the port is exposed only within the local network

To use the installer playbook create an inventory file indicating the machine type - `ollama`.

### Sample Inventory

```yaml
all:
  hosts:
  children:
    ollama:
      hosts:
        ollama.example.com:
```

### Sample Installation Options

#### Local server

This is the default installation. No extra parameters are required

#### Server with non-secure port

If you can limit the access to the port, you may choose to open the non-secure port to the external network

```yaml
ollama_expose_insecure_port_only_local: false
```

#### Server with mTLS - Local Certificates

```yaml
ollama_expose_insecure_port: false
ollama_expose_secured_port: true
ollama_certificate_ca_file: "/path/to/ca"
ollama_certificate_cert_file: "/path/to/crt"
ollama_certificate_key_file: "/path/to//key"
```

#### Server with mTLS - Kubernetes Certificate Manager

```yaml
ollama_expose_insecure_port: false
ollama_expose_secured_port: true
ollama_use_k8s_cert_manager: true
ollama_certificate_namespace: < Namespace of the CA Issuer and Certificate >
ollama_certificate_ca_issuer: < Name of the CA Issuer >
ollama_fqdn: < Server FQDN >
```

### Using the installer

```bash
ansible-playbook -i  </path/to/inventory> -e @</path/to/env_file> ygalblum.ollama.install
```

## Installing the collection from Ansible Galaxy

Before using this collection, you need to install it with the Ansible Galaxy command-line tool:

```bash
ansible-galaxy collection install ygalblum.ollama
```

You can also include it in a `requirements.yml` file and install it with `ansible-galaxy collection install -r requirements.yml`, using the format:

```yaml
---
collections:
  - name: ygalblum.ollama
```

Note that if you install the collection from Ansible Galaxy, it will not be upgraded automatically when you upgrade the `ansible` package.
To upgrade the collection to the latest available version, run the following command:

```bash
ansible-galaxy collection install ygalblum.ollama --upgrade
```

You can also install a specific version of the collection.
For example, if you need to downgrade when something is broken in the latest version (please report an issue in this repository).
Use the following syntax to install version `1.0.0`:

```bash
ansible-galaxy collection install ygalblum.ollama:==1.0.0
```

See [Using Ansible collections](https://docs.ansible.com/ansible/devel/user_guide/collections_using.html) for more details.

## Contributing

We appreciate participation from any new contributors. Get started by opening an issue or pull request.

Refer to our [contribution guide](./CONTRIBUTING.md) for more information

## Reporting issues

Please open a [new issue](https://github.com/ygalblum/ansible-collection-ollama/issues/new/choose) for any bugs or security vulnerabilities you may encounter.
We also invite you to open an issue if you have ideas on how we can improve the solution or want to make a suggestion for enhancement.

## Release notes

See the [changelog](https://github.com/ygalblum/ansible-collection-ollama/tree/main/CHANGELOG.rst).

## Licensing

See [LICENSE](./LICENSE) to see the full text.
