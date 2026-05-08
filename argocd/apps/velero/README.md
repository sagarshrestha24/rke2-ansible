# velero

![Version: 7.2.1](https://img.shields.io/badge/Version-7.2.1-informational?style=flat-square) ![AppVersion: 1.14.1](https://img.shields.io/badge/AppVersion-1.14.1-informational?style=flat-square)

A Helm chart for velero

**Homepage:** <https://github.com/vmware-tanzu/velero>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| jenting | <hsiaoairplane@gmail.com> |  |
| reasonerjt | <jiangd@vmware.com> |  |
| qiuming-best | <mqiu@vmware.com> |  |
| ywk253100 | <yinw@vmware.com> |  |

## Source Code

* <https://github.com/vmware-tanzu/velero>

## Requirements

Kubernetes: `>=1.16.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| annotations | object | `{}` |  |
| backupsEnabled | bool | `true` |  |
| cleanUpCRDs | bool | `false` |  |
| configMaps | object | `{}` |  |
| configuration.backupStorageLocation[0].accessMode | string | `"ReadWrite"` |  |
| configuration.backupStorageLocation[0].annotations | object | `{}` |  |
| configuration.backupStorageLocation[0].bucket | string | `"velero"` |  |
| configuration.backupStorageLocation[0].caCert | string | `nil` |  |
| configuration.backupStorageLocation[0].config.region | string | `"minio"` |  |
| configuration.backupStorageLocation[0].config.s3ForcePathStyle | bool | `true` |  |
| configuration.backupStorageLocation[0].config.s3Url | string | `"http://myminio-hl.minio.svc:9000"` |  |
| configuration.backupStorageLocation[0].default | bool | `true` |  |
| configuration.backupStorageLocation[0].name | string | `"velero"` |  |
| configuration.backupStorageLocation[0].prefix | string | `nil` |  |
| configuration.backupStorageLocation[0].provider | string | `"aws"` |  |
| configuration.backupStorageLocation[0].validationFrequency | string | `nil` |  |
| configuration.backupSyncPeriod | string | `nil` |  |
| configuration.clientBurst | string | `nil` |  |
| configuration.clientPageSize | string | `nil` |  |
| configuration.clientQPS | string | `nil` |  |
| configuration.defaultBackupStorageLocation | string | `nil` |  |
| configuration.defaultBackupTTL | string | `nil` |  |
| configuration.defaultItemOperationTimeout | string | `nil` |  |
| configuration.defaultRepoMaintainFrequency | string | `nil` |  |
| configuration.defaultSnapshotMoveData | string | `nil` |  |
| configuration.defaultVolumeSnapshotLocations | string | `nil` |  |
| configuration.defaultVolumesToFsBackup | string | `nil` |  |
| configuration.disableControllers | string | `nil` |  |
| configuration.disableInformerCache | bool | `false` |  |
| configuration.extraArgs | list | `[]` |  |
| configuration.extraEnvVars | object | `{}` |  |
| configuration.features | string | `nil` |  |
| configuration.fsBackupTimeout | string | `nil` |  |
| configuration.garbageCollectionFrequency | string | `nil` |  |
| configuration.logFormat | string | `nil` |  |
| configuration.logLevel | string | `nil` |  |
| configuration.metricsAddress | string | `nil` |  |
| configuration.namespace | string | `nil` |  |
| configuration.pluginDir | string | `nil` |  |
| configuration.profilerAddress | string | `nil` |  |
| configuration.repositoryMaintenanceJob.latestJobsCount | int | `3` |  |
| configuration.repositoryMaintenanceJob.limits | string | `nil` |  |
| configuration.repositoryMaintenanceJob.requests | string | `nil` |  |
| configuration.restoreOnlyMode | string | `nil` |  |
| configuration.restoreResourcePriorities | string | `nil` |  |
| configuration.storeValidationFrequency | string | `nil` |  |
| configuration.terminatingResourceTimeout | string | `nil` |  |
| configuration.uploaderType | string | `nil` | ------------------ `velero server` default: kopia |
| configuration.volumeSnapshotLocation[0].annotations | object | `{}` |  |
| configuration.volumeSnapshotLocation[0].config.region | string | `"minio"` |  |
| configuration.volumeSnapshotLocation[0].config.s3ForcePathStyle | bool | `true` |  |
| configuration.volumeSnapshotLocation[0].config.s3Url | string | `"http://myminio-hl.minio.svc:9000"` |  |
| configuration.volumeSnapshotLocation[0].name | string | `"velero"` |  |
| configuration.volumeSnapshotLocation[0].provider | string | `"aws"` |  |
| containerSecurityContext | object | `{}` |  |
| credentials.existingSecret | string | `nil` |  |
| credentials.extraEnvVars | object | `{}` |  |
| credentials.extraSecretRef | string | `""` |  |
| credentials.name | string | `"velero"` |  |
| credentials.secretContents.cloud | string | `"[default]\naws_access_key_id=jBt9NZq8rfGNcN9sZ1fA\naws_secret_access_key=vCRT0CPve44V3dNZr16AVvjlmLnEgUXrPewdodWP\n"` |  |
| credentials.useSecret | bool | `true` |  |
| deployNodeAgent | bool | `false` |  |
| dnsConfig | object | `{}` |  |
| dnsPolicy | string | `"ClusterFirst"` |  |
| extraObjects | list | `[]` |  |
| extraVolumeMounts | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| image.imagePullSecrets | list | `[]` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"velero/velero"` |  |
| image.tag | string | `"v1.14.1"` |  |
| initContainers | string | `nil` |  |
| kubectl.annotations | object | `{}` |  |
| kubectl.containerSecurityContext | object | `{}` |  |
| kubectl.image.repository | string | `"docker.io/bitnami/kubectl"` |  |
| kubectl.labels | object | `{}` |  |
| kubectl.resources | object | `{}` |  |
| labels | object | `{}` |  |
| lifecycle | object | `{}` |  |
| livenessProbe.failureThreshold | int | `5` |  |
| livenessProbe.httpGet.path | string | `"/metrics"` |  |
| livenessProbe.httpGet.port | string | `"http-monitoring"` |  |
| livenessProbe.httpGet.scheme | string | `"HTTP"` |  |
| livenessProbe.initialDelaySeconds | int | `10` |  |
| livenessProbe.periodSeconds | int | `30` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| metrics.enabled | bool | `true` |  |
| metrics.nodeAgentPodMonitor.additionalLabels | object | `{}` |  |
| metrics.nodeAgentPodMonitor.annotations | object | `{}` |  |
| metrics.nodeAgentPodMonitor.autodetect | bool | `true` |  |
| metrics.nodeAgentPodMonitor.enabled | bool | `false` |  |
| metrics.podAnnotations."prometheus.io/path" | string | `"/metrics"` |  |
| metrics.podAnnotations."prometheus.io/port" | string | `"8085"` |  |
| metrics.podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| metrics.prometheusRule.additionalLabels | object | `{}` |  |
| metrics.prometheusRule.autodetect | bool | `true` |  |
| metrics.prometheusRule.enabled | bool | `false` |  |
| metrics.prometheusRule.spec | list | `[]` |  |
| metrics.scrapeInterval | string | `"30s"` |  |
| metrics.scrapeTimeout | string | `"10s"` |  |
| metrics.service.annotations | object | `{}` |  |
| metrics.service.labels | object | `{}` |  |
| metrics.serviceMonitor.additionalLabels | object | `{}` |  |
| metrics.serviceMonitor.annotations | object | `{}` |  |
| metrics.serviceMonitor.autodetect | bool | `true` |  |
| metrics.serviceMonitor.enabled | bool | `false` |  |
| nameOverride | string | `""` |  |
| namespace.labels | object | `{}` |  |
| nodeAgent.affinity | object | `{}` |  |
| nodeAgent.annotations | object | `{}` |  |
| nodeAgent.containerSecurityContext | object | `{}` |  |
| nodeAgent.dnsConfig | object | `{}` |  |
| nodeAgent.dnsPolicy | string | `"ClusterFirst"` |  |
| nodeAgent.extraArgs | list | `[]` |  |
| nodeAgent.extraEnvVars | object | `{}` |  |
| nodeAgent.extraVolumeMounts | list | `[]` |  |
| nodeAgent.extraVolumes | list | `[]` |  |
| nodeAgent.labels | object | `{}` |  |
| nodeAgent.lifecycle | object | `{}` |  |
| nodeAgent.nodeSelector | object | `{}` |  |
| nodeAgent.podSecurityContext.runAsUser | int | `0` |  |
| nodeAgent.podVolumePath | string | `"/var/lib/kubelet/pods"` |  |
| nodeAgent.priorityClassName | string | `""` |  |
| nodeAgent.resources | object | `{}` |  |
| nodeAgent.tolerations | list | `[]` |  |
| nodeAgent.useScratchEmptyDir | bool | `true` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClassName | string | `""` |  |
| rbac.clusterAdministrator | bool | `true` |  |
| rbac.clusterAdministratorName | string | `"cluster-admin"` |  |
| rbac.create | bool | `true` |  |
| readinessProbe.failureThreshold | int | `5` |  |
| readinessProbe.httpGet.path | string | `"/metrics"` |  |
| readinessProbe.httpGet.port | string | `"http-monitoring"` |  |
| readinessProbe.httpGet.scheme | string | `"HTTP"` |  |
| readinessProbe.initialDelaySeconds | int | `10` |  |
| readinessProbe.periodSeconds | int | `30` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `5` |  |
| resources | object | `{}` |  |
| schedules | object | `{}` |  |
| secretAnnotations | object | `{}` |  |
| serviceAccount.server.annotations | string | `nil` |  |
| serviceAccount.server.create | bool | `true` |  |
| serviceAccount.server.imagePullSecrets | list | `[]` |  |
| serviceAccount.server.labels | string | `nil` |  |
| serviceAccount.server.name | string | `nil` |  |
| snapshotsEnabled | bool | `true` |  |
| terminationGracePeriodSeconds | int | `3600` |  |
| tolerations | list | `[]` |  |
| upgradeCRDs | bool | `true` |  |
| upgradeCRDsJob.extraEnvVars | object | `{}` |  |
| upgradeCRDsJob.extraVolumeMounts | list | `[]` |  |
| upgradeCRDsJob.extraVolumes | list | `[]` |  |
| upgradeJobResources | object | `{}` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
