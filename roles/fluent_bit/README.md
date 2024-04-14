# fluent_bit role

The `fluent_bit` role handles the installation of Fluent-Bit and configuring it to monitor the local machine

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

Requires `root` privileges.

## Role Variables

### `fluent_bit_expose_insecure`

Expose the FluentBit port to the external network (without mTLS).

Default `false`

## Example Playbook

```yaml
- name: Setup Secure Ollama with K8S Certificate Manager
  hosts: all
  vars:
  roles:
  - name: fluent_bit
```
