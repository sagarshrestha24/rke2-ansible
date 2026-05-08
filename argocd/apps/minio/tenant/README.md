# tenant

![Version: 6.0.4](https://img.shields.io/badge/Version-6.0.4-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: v6.0.4](https://img.shields.io/badge/AppVersion-v6.0.4-informational?style=flat-square)

A Helm chart for MinIO Operator

**Homepage:** <https://min.io>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| MinIO, Inc | <dev@minio.io> |  |

## Source Code

* <https://github.com/minio/operator>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| containers.operator.image | string | `"sagark24/minio-operator"` |  |
| containers.operator.tag | string | `"latest"` |  |
| ingress.api.annotations | object | `{}` |  |
| ingress.api.enabled | bool | `false` |  |
| ingress.api.host | string | `"minio.local"` |  |
| ingress.api.ingressClassName | string | `""` |  |
| ingress.api.labels | object | `{}` |  |
| ingress.api.path | string | `"/"` |  |
| ingress.api.pathType | string | `"Prefix"` |  |
| ingress.api.tls | list | `[]` |  |
| ingress.console.enabled | bool | `true` |  |
| ingress.console.host | string | `"minio-console.coreii.labenv.ai"` |  |
| ingress.console.ingressClassName | string | `"nginx"` |  |
| ingress.console.labels | object | `{}` |  |
| ingress.console.path | string | `"/"` |  |
| ingress.console.pathType | string | `"Prefix"` |  |
| ingress.console.tls | list | `[]` |  |
| tenant.additionalVolumeMounts | list | `[]` |  |
| tenant.additionalVolumes | list | `[]` |  |
| tenant.buckets[0].name | string | `"velero-test"` |  |
| tenant.buckets[0].objectLock | bool | `false` |  |
| tenant.certificate.certConfig | object | `{}` |  |
| tenant.certificate.externalCaCertSecret | list | `[]` |  |
| tenant.certificate.externalCertSecret | list | `[]` |  |
| tenant.certificate.requestAutoCert | bool | `false` |  |
| tenant.configSecret.accessKey | string | `"minio"` |  |
| tenant.configSecret.name | string | `"myminio-env-configuration"` |  |
| tenant.configSecret.secretKey | string | `"minio123"` |  |
| tenant.configuration.name | string | `"myminio-env-configuration"` |  |
| tenant.env[0].name | string | `"MINIO_PROMETHEUS_AUTH_TYPE"` |  |
| tenant.env[0].value | string | `"public"` |  |
| tenant.exposeServices | object | `{}` |  |
| tenant.features.bucketDNS | bool | `false` |  |
| tenant.features.domains | object | `{}` |  |
| tenant.features.enableSFTP | bool | `false` |  |
| tenant.image.pullPolicy | string | `"IfNotPresent"` |  |
| tenant.image.repository | string | `"sagark24/minio"` |  |
| tenant.image.tag | string | `"v1"` |  |
| tenant.imagePullSecret | object | `{}` |  |
| tenant.lifecycle | object | `{}` |  |
| tenant.liveness | object | `{}` |  |
| tenant.logging | object | `{}` |  |
| tenant.metrics.enabled | bool | `true` |  |
| tenant.metrics.port | int | `9000` |  |
| tenant.metrics.protocol | string | `"http"` |  |
| tenant.mountPath | string | `"/export"` |  |
| tenant.name | string | `"myminio"` |  |
| tenant.podManagementPolicy | string | `"Parallel"` |  |
| tenant.pools[0].affinity | object | `{}` |  |
| tenant.pools[0].annotations | object | `{}` |  |
| tenant.pools[0].containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| tenant.pools[0].containerSecurityContext.capabilities.drop[0] | string | `"ALL"` |  |
| tenant.pools[0].containerSecurityContext.runAsGroup | int | `1000` |  |
| tenant.pools[0].containerSecurityContext.runAsNonRoot | bool | `true` |  |
| tenant.pools[0].containerSecurityContext.runAsUser | int | `1000` |  |
| tenant.pools[0].containerSecurityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| tenant.pools[0].labels | object | `{}` |  |
| tenant.pools[0].name | string | `"pool-0"` |  |
| tenant.pools[0].nodeSelector | object | `{}` |  |
| tenant.pools[0].resources | object | `{}` |  |
| tenant.pools[0].securityContext.fsGroup | int | `1000` |  |
| tenant.pools[0].securityContext.fsGroupChangePolicy | string | `"OnRootMismatch"` |  |
| tenant.pools[0].securityContext.runAsGroup | int | `1000` |  |
| tenant.pools[0].securityContext.runAsNonRoot | bool | `true` |  |
| tenant.pools[0].securityContext.runAsUser | int | `1000` |  |
| tenant.pools[0].servers | int | `1` |  |
| tenant.pools[0].size | string | `"5Gi"` |  |
| tenant.pools[0].storageAnnotations | object | `{}` |  |
| tenant.pools[0].storageClassName | string | `"longhorn"` |  |
| tenant.pools[0].tolerations | list | `[]` |  |
| tenant.pools[0].topologySpreadConstraints | list | `[]` |  |
| tenant.pools[0].volumesPerServer | int | `1` |  |
| tenant.priorityClassName | string | `""` |  |
| tenant.prometheusOperator | bool | `false` |  |
| tenant.readiness | object | `{}` |  |
| tenant.scheduler | object | `{}` |  |
| tenant.serviceAccountName | string | `""` |  |
| tenant.serviceMetadata | object | `{}` |  |
| tenant.startup | object | `{}` |  |
| tenant.subPath | string | `"/data"` |  |
| tenant.users[0].name | string | `"velero"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
