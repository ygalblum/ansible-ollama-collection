# ollama role

The `ollama` role handles the installation and configuration of Ollama

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

## Role Variables

### `ollama_quadlet_directory`

Location to save the Quadlet files.

By default, the role runs ollama as rootless and therefore will use `~/.config/containers/systemd/`

### `ollama_container_image_tag`

Ollama container image tag.

Default `latest`.

For more details see [Ollama Docker image](https://hub.docker.com/r/ollama/ollama)

### `ollama_models`

List of LLM models to preload.

Default `mistral`

### `ollama_expose_insecure_port`

Expose the insecure port `11434` from container.

Default `True`

### `ollama_expose_insecure_port_only_local`

Expose the insecure port `11434` from container only to the localhost.

Default `True`

### `ollama_expose_secured_port`

Expose `Ollama` via a secure port by running a sidecar container running [Envoy Proxy](https://www.envoyproxy.io/)

Default `False`

### `ollama_secured_port`

Set the port number for the secure port.

Default `11435`

### `ollama_use_k8s_cert_manager`

Use K8S [Certificate Manager](https://cert-manager.io/) to obtain the certificate.

If set to `True`, the role will access Kubernetes from the localhost

Default `False`

### `ollama_certificate_ca_file`

Path for the CA Certificate on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_cert_file`

Path for the Certificate on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_key_file`

Path for the Key on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`


## Example Playbook

```yaml
- name: Setup Secure Ollama with K8S Certificate Manager
  hosts: ollama
  vars:
    ollama_expose_secured_port: True
    ollama_use_k8s_cert_manager: True
  roles:
  - name: ollama
```
