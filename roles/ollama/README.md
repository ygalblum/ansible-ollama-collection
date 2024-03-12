# ollama role

The `ollama` role handles the installation and configuration of Ollama

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

## Role Variables

### `ollama_models`

List of LLM models to preload.

Default `['mistral']`

### `ollama_expose_secured_port`

Expose `Ollama` via a secure port via [Envoy Proxy](https://www.envoyproxy.io/)

Default `false`

### `ollama_secured_port`

Set the port number for the secure port.

Default `11435`

### `ollama_use_k8s_cert_manager`

Use K8S [Certificate Manager](https://cert-manager.io/) to obtain the certificate.

If set to `True`, the role will access Kubernetes from the localhost

Default `false`

### `ollama_certificate_namespace`

Kubernetes Namespace for the CA issuer and the created certificate

Required when `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_ca_issuer`

Name of the Kubernetes Cert-Manager CA Issuer resource

Required when `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_fqdn`

FQDN for the Server to use for the certificate `dnsNames`

Required when `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_ca_file`

Path for the CA Certificate on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_cert_file`

Path for the Certificate on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_certificate_key_file`

Path for the Key on the localhost

Required unless `ollama_use_k8s_cert_manager` is set to `True`

### `ollama_proxy_admin_expose_insecure`

Expose the proxy admin insecure port.

Default `false`

### `ollama_proxy_admin_expose_secure`

Expose the proxy admin port as a secure port using the same certificates

Default `false`

### `ollama_proxy_admin_secure_port`

Set the port number for the proxy admin secure port.

Default `19901`

### `ollama_fluentbit_enable`

Provision [FluentBit](https://fluentbit.io/) to scrape metrics and act as a Prometheus exporter

Default `false`

### `ollama_fluentbit_expose_insecure`

Expose the FluentBit insecure port.

Default `false`

### `ollama_fluentbit_expose_secure`

Expose the FluentBit port as a secure port using the same certificates

Default `false`

### `ollama_fluentbit_expose_secure_port`

Set the port number for the FluentBit secure port.

Default `12021`

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
