# nvidia role

The `nvidia` role handles the installation of the NVIDIA drivers and applications.
The roles runs the `common` role as a dependency

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

Requires `root` privileges

## Role Variables

The `nvidia` role does not support any variables

## Example Playbook

```yaml
- name: Setup Secure Ollama with K8S Certificate Manager
  hosts: all
  become: true
  tasks:
  - name: Install NVIDIA drivers and applications
    ansible.builtin.include_role:
      name: nvidia
    when: install_nvidia
```
