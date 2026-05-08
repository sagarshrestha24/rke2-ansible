# kube-state-metrics

![Version: 4.30.0](https://img.shields.io/badge/Version-4.30.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.8.0](https://img.shields.io/badge/AppVersion-2.8.0-informational?style=flat-square)

Install kube-state-metrics to generate and expose cluster-level metrics

**Homepage:** <https://github.com/kubernetes/kube-state-metrics/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| tariq1890 | <tariq.ibrahim@mulesoft.com> |  |
| mrueg | <manuel@rueg.eu> |  |
| dotdc | <david@0xdc.me> |  |

## Source Code

* <https://github.com/kubernetes/kube-state-metrics/>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| annotations | object | `{}` |  |
| autosharding.enabled | bool | `false` |  |
| collectors[0] | string | `"certificatesigningrequests"` |  |
| collectors[10] | string | `"limitranges"` |  |
| collectors[11] | string | `"mutatingwebhookconfigurations"` |  |
| collectors[12] | string | `"namespaces"` |  |
| collectors[13] | string | `"networkpolicies"` |  |
| collectors[14] | string | `"nodes"` |  |
| collectors[15] | string | `"persistentvolumeclaims"` |  |
| collectors[16] | string | `"persistentvolumes"` |  |
| collectors[17] | string | `"poddisruptionbudgets"` |  |
| collectors[18] | string | `"pods"` |  |
| collectors[19] | string | `"replicasets"` |  |
| collectors[1] | string | `"configmaps"` |  |
| collectors[20] | string | `"replicationcontrollers"` |  |
| collectors[21] | string | `"resourcequotas"` |  |
| collectors[22] | string | `"secrets"` |  |
| collectors[23] | string | `"services"` |  |
| collectors[24] | string | `"statefulsets"` |  |
| collectors[25] | string | `"storageclasses"` |  |
| collectors[26] | string | `"validatingwebhookconfigurations"` |  |
| collectors[27] | string | `"volumeattachments"` |  |
| collectors[2] | string | `"cronjobs"` |  |
| collectors[3] | string | `"daemonsets"` |  |
| collectors[4] | string | `"deployments"` |  |
| collectors[5] | string | `"endpoints"` |  |
| collectors[6] | string | `"horizontalpodautoscalers"` |  |
| collectors[7] | string | `"ingresses"` |  |
| collectors[8] | string | `"jobs"` |  |
| collectors[9] | string | `"leases"` |  |
| containerSecurityContext | object | `{}` |  |
| customLabels | object | `{}` |  |
| extraArgs | list | `[]` |  |
| global.imagePullSecrets | list | `[]` |  |
| hostNetwork | bool | `false` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"registry.k8s.io/kube-state-metrics/kube-state-metrics"` |  |
| image.sha | string | `""` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| kubeRBACProxy.containerSecurityContext | object | `{}` |  |
| kubeRBACProxy.enabled | bool | `false` |  |
| kubeRBACProxy.extraArgs | list | `[]` |  |
| kubeRBACProxy.image.pullPolicy | string | `"IfNotPresent"` |  |
| kubeRBACProxy.image.repository | string | `"quay.io/brancz/kube-rbac-proxy"` |  |
| kubeRBACProxy.image.sha | string | `""` |  |
| kubeRBACProxy.image.tag | string | `"v0.14.0"` |  |
| kubeRBACProxy.resources | object | `{}` |  |
| kubeTargetVersionOverride | string | `""` |  |
| kubeconfig.enabled | bool | `false` |  |
| kubeconfig.secret | string | `nil` |  |
| metricAllowlist | list | `[]` |  |
| metricAnnotationsAllowList | list | `[]` |  |
| metricDenylist | list | `[]` |  |
| metricLabelsAllowlist | list | `[]` |  |
| namespaceOverride | string | `""` |  |
| namespaces | string | `""` |  |
| namespacesDenylist | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podDisruptionBudget | object | `{}` |  |
| podSecurityPolicy.additionalVolumes | list | `[]` |  |
| podSecurityPolicy.annotations | object | `{}` |  |
| podSecurityPolicy.enabled | bool | `false` |  |
| prometheus.monitor.additionalLabels | object | `{}` |  |
| prometheus.monitor.enabled | bool | `false` |  |
| prometheus.monitor.honorLabels | bool | `false` |  |
| prometheus.monitor.interval | string | `""` |  |
| prometheus.monitor.jobLabel | string | `""` |  |
| prometheus.monitor.labelLimit | int | `0` |  |
| prometheus.monitor.labelNameLengthLimit | int | `0` |  |
| prometheus.monitor.labelValueLengthLimit | int | `0` |  |
| prometheus.monitor.metricRelabelings | list | `[]` |  |
| prometheus.monitor.namespace | string | `""` |  |
| prometheus.monitor.podTargetLabels | list | `[]` |  |
| prometheus.monitor.proxyUrl | string | `""` |  |
| prometheus.monitor.relabelings | list | `[]` |  |
| prometheus.monitor.sampleLimit | int | `0` |  |
| prometheus.monitor.scheme | string | `""` |  |
| prometheus.monitor.scrapeTimeout | string | `""` |  |
| prometheus.monitor.selectorOverride | object | `{}` |  |
| prometheus.monitor.targetLabels | list | `[]` |  |
| prometheus.monitor.targetLimit | int | `0` |  |
| prometheus.monitor.tlsConfig | object | `{}` |  |
| prometheusScrape | bool | `true` |  |
| rbac.create | bool | `true` |  |
| rbac.extraRules | list | `[]` |  |
| rbac.useClusterRole | bool | `true` |  |
| releaseLabel | bool | `false` |  |
| releaseNamespace | bool | `false` |  |
| replicas | int | `1` |  |
| resources | object | `{}` |  |
| securityContext.enabled | bool | `true` |  |
| securityContext.fsGroup | int | `65534` |  |
| securityContext.runAsGroup | int | `65534` |  |
| securityContext.runAsUser | int | `65534` |  |
| selectorOverride | object | `{}` |  |
| selfMonitor.enabled | bool | `false` |  |
| service.annotations | object | `{}` |  |
| service.clusterIP | string | `""` |  |
| service.loadBalancerIP | string | `""` |  |
| service.loadBalancerSourceRanges | list | `[]` |  |
| service.nodePort | int | `0` |  |
| service.port | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.imagePullSecrets | list | `[]` |  |
| serviceAccount.name | string | `nil` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` |  |
| verticalPodAutoscaler.controlledResources | list | `[]` |  |
| verticalPodAutoscaler.enabled | bool | `false` |  |
| verticalPodAutoscaler.maxAllowed | object | `{}` |  |
| verticalPodAutoscaler.minAllowed | object | `{}` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
