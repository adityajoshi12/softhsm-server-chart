# SoftHSM Server Helm Chart

This Helm chart deploys a SoftHSM server on Kubernetes.

## Prerequisites

- Kubernetes 1.12+
- Helm 3+

## Installation

To install the chart with the release name `my-release`:

```bash
helm install my-release softhsm-server-chart
```

If you want to specify a namespace:

```bash
helm install my-release softhsm-server-chart -n my-namespace
```

## Configuration

The following table lists the configurable parameters of the `softhsm-server-chart` and their default values.

| Parameter                     | Description                                | Default                        |
|-------------------------------|--------------------------------------------|--------------------------------|
| `replicaCount`                | Number of replicas                         | `1`                            |
| `image.repository`            | Image repository                           | `vegardit/softhsm2-pkcs11-proxy`|
| `image.tag`                   | Image tag                                  | `latest-debian`                |
| `image.pullPolicy`            | Image pull policy                          | `Always`                       |
| `service.type`                | Service type                               | `ClusterIP`                    |
| `service.port`                | Service port                               | `2345`                         |
| `persistence.enabled`         | Enable persistence                         | `true`                         |
| `persistence.storageClass`    | Storage class                              | `standard-hdd`                 |
| `persistence.accessMode`      | Access mode                                | `ReadWriteOnce`                |
| `persistence.size`            | Storage size                               | `1Gi`                          |
| `secret.pkcs11_proxy_psk`     | PKCS11 proxy PSK                           | `cHNrX2lkZW50aXR5OjI3NjA0M2JjMjkwMWIyMTU3ZTRlZDAwMjNiMjJiOWMxOTY1NGRlNDlmZTIzZWEwMTdkZDQ5MGFjNzliNzdlMDI=` |
| `secret.token_import_test_data`| Token import test data                    | `MAo=`                         |
| `secret.token_so_pin`         | Token SO PIN                               | `alVMQ2JwTVVYdmpI`             |
| `secret.token_user_pin`       | Token user PIN                             | `alVMQ2JwTVVYdmpI`             |
| `config.softhsm2_conf`        | SoftHSM2 configuration                     | See `values.yaml`              |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash
helm install my-release softhsm-server-chart --set replicaCount=2
```

Alternatively, you can provide a YAML file that specifies the values while installing the chart. For example:

```bash
helm install my-release softhsm-server-chart -f values.yaml
```



## Uninstallation
To uninstall/delete the my-release deployment:
```bash
helm uninstall my-release
```
The command removes all the Kubernetes components associated with the chart and deletes the release.

## Persistence

The chart mounts a [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) for the SoftHSM tokens. The volume is created using dynamic volume provisioning. If you want to disable persistence, you can set `persistence.enabled` to `false`.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
