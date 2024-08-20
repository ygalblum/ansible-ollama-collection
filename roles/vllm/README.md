# vllm role

The `vllm` role handles the installation and configuration of vLLM

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

## Role Variables

### `vllm_api_token`

API Token to protect the access to the server

Mandatory

### `vllm_model`

LLM model for vLLM to use

Default `mistralai/Mistral-7B-Instruct-v0.2`

## Example Playbook

```yaml
- name: Setup vLLm
  hosts: vllm
  vars:
    vllm_api_token: my-token
  roles:
  - name: vllm
```
