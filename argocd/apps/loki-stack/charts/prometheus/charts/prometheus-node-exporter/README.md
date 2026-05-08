# prometheus-node-exporter

![Version: 4.8.1](https://img.shields.io/badge/Version-4.8.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.5.0](https://img.shields.io/badge/AppVersion-1.5.0-informational?style=flat-square)

A Helm chart for prometheus node-exporter

**Homepage:** <https://github.com/prometheus/node_exporter/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| gianrubio | <gianrubio@gmail.com> |  |
| zanhsieh | <zanhsieh@gmail.com> |  |

## Source Code

* <https://github.com/prometheus/node_exporter/>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| configmaps | list | `[]` |  |
| containerSecurityContext | object | `{}` |  |
| daemonsetAnnotations | object | `{}` |  |
| dnsConfig | object | `{}` |  |
| endpoints | list | `[]` |  |
| env | object | `{}` |  |
| extraArgs | list | `[]` |  |
| extraHostVolumeMounts | list | `[]` |  |
| extraInitContainers | list | `[]` |  |
| hostNetwork | bool | `true` |  |
| hostPID | bool | `true` |  |
| hostRootFsMount.enabled | bool | `true` |  |
| hostRootFsMount.mountPropagation | string | `"HostToContainer"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"quay.io/prometheus/node-exporter"` |  |
| image.sha | string | `""` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| livenessProbe.failureThreshold | int | `3` |  |
| livenessProbe.httpGet.httpHeaders | list | `[]` |  |
| livenessProbe.httpGet.scheme | string | `"http"` |  |
| livenessProbe.initialDelaySeconds | int | `0` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `1` |  |
| namespaceOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations."cluster-autoscaler.kubernetes.io/safe-to-evict" | string | `"true"` |  |
| podLabels | object | `{}` |  |
| prometheus.monitor.additionalLabels | object | `{}` |  |
| prometheus.monitor.apiVersion | string | `""` |  |
| prometheus.monitor.basicAuth | object | `{}` |  |
| prometheus.monitor.bearerTokenFile | string | `nil` |  |
| prometheus.monitor.enabled | bool | `false` |  |
| prometheus.monitor.interval | string | `""` |  |
| prometheus.monitor.jobLabel | string | `""` |  |
| prometheus.monitor.labelLimit | int | `0` |  |
| prometheus.monitor.labelNameLengthLimit | int | `0` |  |
| prometheus.monitor.labelValueLengthLimit | int | `0` |  |
| prometheus.monitor.metricRelabelings | list | `[]` |  |
| prometheus.monitor.namespace | string | `""` |  |
| prometheus.monitor.proxyUrl | string | `""` |  |
| prometheus.monitor.relabelings | list | `[]` |  |
| prometheus.monitor.sampleLimit | int | `0` |  |
| prometheus.monitor.scheme | string | `"http"` |  |
| prometheus.monitor.scrapeTimeout | string | `"10s"` |  |
| prometheus.monitor.selectorOverride | object | `{}` |  |
| prometheus.monitor.targetLimit | int | `0` |  |
| prometheus.monitor.tlsConfig | object | `{}` |  |
| rbac.create | bool | `true` |  |
| rbac.pspAnnotations | object | `{}` |  |
| rbac.pspEnabled | bool | `true` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.httpGet.httpHeaders | list | `[]` |  |
| readinessProbe.httpGet.scheme | string | `"http"` |  |
| readinessProbe.initialDelaySeconds | int | `0` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `1` |  |
| releaseLabel | bool | `false` |  |
| resources | object | `{}` |  |
| secrets | list | `[]` |  |
| securityContext.fsGroup | int | `65534` |  |
| securityContext.runAsGroup | int | `65534` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `65534` |  |
| service.annotations."prometheus.io/scrape" | string | `"true"` |  |
| service.listenOnAllInterfaces | bool | `true` |  |
| service.nodePort | string | `nil` |  |
| service.port | int | `9100` |  |
| service.portName | string | `"metrics"` |  |
| service.targetPort | int | `9100` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automountServiceAccountToken | bool | `false` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.imagePullSecrets | list | `[]` |  |
| serviceAccount.name | string | `nil` |  |
| sidecarHostVolumeMounts | list | `[]` |  |
| sidecarVolumeMount | list | `[]` |  |
| sidecars | list | `[]` |  |
| tolerations[0].effect | string | `"NoSchedule"` |  |
| tolerations[0].operator | string | `"Exists"` |  |
| updateStrategy.rollingUpdate.maxUnavailable | int | `1` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |
| verticalPodAutoscaler.controlledResources | list | `[]` |  |
| verticalPodAutoscaler.enabled | bool | `false` |  |
| verticalPodAutoscaler.maxAllowed | object | `{}` |  |
| verticalPodAutoscaler.minAllowed | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
