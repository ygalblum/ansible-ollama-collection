# ollama role

The `ollama` role handles the installation and configuration of Ollama

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

## Role Variables

### `ollama_models`

List of LLM models to preload.

Default `['mistral']`

## Example Playbook

```yaml
- name: Setup Ollama
  hosts: ollama
  roles:
  - name: ollama
```
