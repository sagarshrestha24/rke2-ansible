# opensearch

![Version: 2.26.0](https://img.shields.io/badge/Version-2.26.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.17.1](https://img.shields.io/badge/AppVersion-2.17.1-informational?style=flat-square)

A Helm chart for OpenSearch

**Homepage:** <https://opensearch.org>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| DandyDeveloper |  |  |
| gaiksaya |  |  |
| peterzhuamazon |  |  |
| prudhvigodithi |  |  |
| TheAlgo |  |  |

## Source Code

* <https://github.com/opensearch-project/opensearch>
* <https://github.com/opensearch-project/helm-charts>

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| antiAffinity | string | `"soft"` |  |
| antiAffinityTopologyKey | string | `"kubernetes.io/hostname"` |  |
| clusterName | string | `"opensearch-cluster"` |  |
| config."opensearch.yml" | string | `"cluster.name: opensearch-cluster\n\n# Bind to all interfaces because we don't know what IP address Docker will assign to us.\nnetwork.host: 0.0.0.0\n\n# Setting network.host to a non-loopback address enables the annoying bootstrap checks. \"Single-node\" mode disables them again.\n# Implicitly done if \".singleNode\" is set to \"true\".\n# discovery.type: single-node\n\n# Start OpenSearch Security Demo Configuration\n# WARNING: revise all the lines below before you go into production\nplugins:\n  security:\n    ssl:\n      transport:\n        pemcert_filepath: esnode.pem\n        pemkey_filepath: esnode-key.pem\n        pemtrustedcas_filepath: root-ca.pem\n        enforce_hostname_verification: false\n      http:\n        enabled: true\n        pemcert_filepath: esnode.pem\n        pemkey_filepath: esnode-key.pem\n        pemtrustedcas_filepath: root-ca.pem\n    allow_unsafe_democertificates: true\n    allow_default_init_securityindex: true\n    authcz:\n      admin_dn:\n        - CN=kirk,OU=client,O=client,L=test,C=de\n    audit.type: internal_opensearch\n    enable_snapshot_restore_privilege: true\n    check_snapshot_restore_write_privileges: true\n    restapi:\n      roles_enabled: [\"all_access\", \"security_rest_api_access\"]\n    system_indices:\n      enabled: true\n      indices:\n        [\n          \".opendistro-alerting-config\",\n          \".opendistro-alerting-alert*\",\n          \".opendistro-anomaly-results*\",\n          \".opendistro-anomaly-detector*\",\n          \".opendistro-anomaly-checkpoints\",\n          \".opendistro-anomaly-detection-state\",\n          \".opendistro-reports-*\",\n          \".opendistro-notifications-*\",\n          \".opendistro-notebooks\",\n          \".opendistro-asynchronous-search-response*\",\n        ]\n######## End OpenSearch Security Demo Configuration ########\n"` |  |
| customAntiAffinity | object | `{}` |  |
| enableServiceLinks | bool | `true` |  |
| envFrom | list | `[]` |  |
| extraContainers | list | `[]` |  |
| extraEnvs | list | `[]` |  |
| extraInitContainers | list | `[]` |  |
| extraObjects | list | `[]` | Array of extra K8s manifests to deploy |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fsGroup | string | `""` |  |
| fullnameOverride | string | `""` |  |
| global.dockerRegistry | string | `""` |  |
| hostAliases | list | `[]` |  |
| httpHostPort | string | `""` |  |
| httpPort | int | `9200` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"opensearchproject/opensearch"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0] | string | `"chart-example.local"` |  |
| ingress.ingressLabels | object | `{}` |  |
| ingress.path | string | `"/"` |  |
| ingress.tls | list | `[]` |  |
| initResources | object | `{}` |  |
| keystore | list | `[]` |  |
| labels | object | `{}` |  |
| lifecycle | object | `{}` |  |
| livenessProbe | object | `{}` |  |
| majorVersion | string | `""` |  |
| masterService | string | `"opensearch-cluster-master"` |  |
| masterTerminationFix | bool | `false` |  |
| maxUnavailable | int | `1` |  |
| metricsPort | int | `9600` |  |
| nameOverride | string | `""` |  |
| networkHost | string | `"0.0.0.0"` |  |
| networkPolicy.create | bool | `false` |  |
| networkPolicy.http.enabled | bool | `false` |  |
| nodeAffinity | object | `{}` |  |
| nodeGroup | string | `"master"` |  |
| nodeSelector | object | `{}` |  |
| openSearchAnnotations | object | `{}` |  |
| opensearchHome | string | `"/usr/share/opensearch"` |  |
| opensearchJavaOpts | string | `"-Xmx512M -Xms512M"` |  |
| opensearchLifecycle | object | `{}` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.annotations | object | `{}` |  |
| persistence.enableInitChown | bool | `true` |  |
| persistence.enabled | bool | `true` |  |
| persistence.labels.additionalLabels | object | `{}` |  |
| persistence.labels.enabled | bool | `false` |  |
| persistence.size | string | `"8Gi"` |  |
| plugins.enabled | bool | `false` |  |
| plugins.installList | list | `[]` |  |
| podAffinity | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podManagementPolicy | string | `"Parallel"` |  |
| podSecurityContext.fsGroup | int | `1000` |  |
| podSecurityContext.runAsUser | int | `1000` |  |
| podSecurityPolicy.create | bool | `false` |  |
| podSecurityPolicy.name | string | `""` |  |
| podSecurityPolicy.spec.fsGroup.rule | string | `"RunAsAny"` |  |
| podSecurityPolicy.spec.privileged | bool | `true` |  |
| podSecurityPolicy.spec.runAsUser.rule | string | `"RunAsAny"` |  |
| podSecurityPolicy.spec.seLinux.rule | string | `"RunAsAny"` |  |
| podSecurityPolicy.spec.supplementalGroups.rule | string | `"RunAsAny"` |  |
| podSecurityPolicy.spec.volumes[0] | string | `"secret"` |  |
| podSecurityPolicy.spec.volumes[1] | string | `"configMap"` |  |
| podSecurityPolicy.spec.volumes[2] | string | `"persistentVolumeClaim"` |  |
| podSecurityPolicy.spec.volumes[3] | string | `"emptyDir"` |  |
| priorityClassName | string | `""` |  |
| protocol | string | `"https"` |  |
| rbac.automountServiceAccountToken | bool | `false` |  |
| rbac.create | bool | `false` |  |
| rbac.serviceAccountAnnotations | object | `{}` |  |
| rbac.serviceAccountName | string | `""` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.periodSeconds | int | `5` |  |
| readinessProbe.tcpSocket.port | int | `9200` |  |
| readinessProbe.timeoutSeconds | int | `3` |  |
| replicas | int | `3` |  |
| resources.requests.cpu | string | `"1000m"` |  |
| resources.requests.memory | string | `"100Mi"` |  |
| roles[0] | string | `"master"` |  |
| roles[1] | string | `"ingest"` |  |
| roles[2] | string | `"data"` |  |
| roles[3] | string | `"remote_cluster_client"` |  |
| schedulerName | string | `""` |  |
| secretMounts | list | `[]` |  |
| securityConfig.actionGroupsSecret | string | `nil` |  |
| securityConfig.config.data | object | `{}` |  |
| securityConfig.config.dataComplete | bool | `true` |  |
| securityConfig.config.securityConfigSecret | string | `""` |  |
| securityConfig.configSecret | string | `nil` |  |
| securityConfig.enabled | bool | `true` |  |
| securityConfig.internalUsersSecret | string | `nil` |  |
| securityConfig.path | string | `"/usr/share/opensearch/config/opensearch-security"` |  |
| securityConfig.rolesMappingSecret | string | `nil` |  |
| securityConfig.rolesSecret | string | `nil` |  |
| securityConfig.tenantsSecret | string | `nil` |  |
| securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `1000` |  |
| service.annotations | object | `{}` |  |
| service.externalTrafficPolicy | string | `""` |  |
| service.headless.annotations | object | `{}` |  |
| service.httpPortName | string | `"http"` |  |
| service.labels | object | `{}` |  |
| service.labelsHeadless | object | `{}` |  |
| service.loadBalancerIP | string | `""` |  |
| service.loadBalancerSourceRanges | list | `[]` |  |
| service.metricsPortName | string | `"metrics"` |  |
| service.nodePort | string | `""` |  |
| service.transportPortName | string | `"transport"` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.interval | string | `"10s"` |  |
| serviceMonitor.labels | object | `{}` |  |
| serviceMonitor.path | string | `"/_prometheus/metrics"` |  |
| sidecarResources | object | `{}` |  |
| singleNode | bool | `false` |  |
| startupProbe.failureThreshold | int | `30` |  |
| startupProbe.initialDelaySeconds | int | `5` |  |
| startupProbe.periodSeconds | int | `10` |  |
| startupProbe.tcpSocket.port | int | `9200` |  |
| startupProbe.timeoutSeconds | int | `3` |  |
| sysctl.enabled | bool | `false` |  |
| sysctlInit.enabled | bool | `false` |  |
| sysctlVmMaxMapCount | int | `262144` |  |
| terminationGracePeriod | int | `120` |  |
| tolerations | list | `[]` |  |
| topologySpreadConstraints | list | `[]` |  |
| transportHostPort | string | `""` |  |
| transportPort | int | `9300` |  |
| updateStrategy | string | `"RollingUpdate"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
