# proxy role

The `proxy` role handles the installation and configuration of Evnoy Proxy.
The proxy is used to expose the application and monitoring ports using mTLS

## Requirements

### Target Machine Operating System

Currently, the collection is aimed at RPM based operating systems.

## Role Variables

### `proxy_model_server_local_port`

Set the port number of the local port at which the Model server is listening

### `proxy_model_server_secure_port`

Set the port number for the secure port for the Model server

### `proxy_use_k8s_cert_manager`

Use K8S [Certificate Manager](https://cert-manager.io/) to obtain the certificate.

If set to `True`, the role will access Kubernetes from the localhost

Default `false`

### `proxy_certificate_namespace`

Kubernetes Namespace for the CA issuer and the created certificate

Required when `proxy_use_k8s_cert_manager` is set to `True`

### `proxy_certificate_ca_issuer`

Name of the Kubernetes Cert-Manager CA Issuer resource

Required when `proxy_use_k8s_cert_manager` is set to `True`

### `proxy_fqdn`

FQDN for the Server to use for the certificate `dnsNames`

Required when `proxy_use_k8s_cert_manager` is set to `True`

### `proxy_certificate_ca_file`

Path for the CA Certificate on the localhost

Required unless `proxy_use_k8s_cert_manager` is set to `False`

### `proxy_certificate_cert_file`

Path for the Certificate on the localhost

Required unless `proxy_use_k8s_cert_manager` is set to `False`

### `proxy_certificate_key_file`

Path for the Key on the localhost

Required unless `proxy_use_k8s_cert_manager` is set to `False`

### `proxy_admin_expose_insecure`

Expose the proxy admin insecure port.

Default `false`

### `proxy_admin_expose_secure`

Expose the proxy admin port as a secure port using the same certificates

Default `false`

### `proxy_admin_secure_port`

Set the port number for the proxy admin secure port.

Default `19901`

### `proxy_fluentbit_expose_secure`

Expose the FluentBit port as a secure port using the same certificates

Default `false`

### `proxy_fluentbit_expose_secure_port`

Set the port number for the FluentBit secure port.

Default `12021`

## Example Playbook

```yaml
- name: Setup Secure Ollama with K8S Certificate Manager
  hosts: all
  vars:
    proxy_use_k8s_cert_manager: True
    proxy_certificate_namespace: "my-space"
    proxy_certificate_ca_issuer: "private-issuer"
    proxy_fqdn: "proxy.example.com"
  roles:
  - name: proxy
```
