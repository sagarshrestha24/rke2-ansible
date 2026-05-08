# nvidia-device-plugin

![Version: 0.17.0](https://img.shields.io/badge/Version-0.17.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.17.0](https://img.shields.io/badge/AppVersion-0.17.0-informational?style=flat-square)

A Helm chart for the nvidia-device-plugin on Kubernetes

**Homepage:** <https://github.com/NVIDIA/k8s-device-plugin>

## Requirements

Kubernetes: `>= 1.10.0-0`

| Repository | Name | Version |
|------------|------|---------|
| https://kubernetes-sigs.github.io/node-feature-discovery/charts | nfd(node-feature-discovery) | 0.16.6 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].key | string | `"feature.node.kubernetes.io/pci-10de.present"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].operator | string | `"In"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].values[0] | string | `"true"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[1].matchExpressions[0].key | string | `"feature.node.kubernetes.io/cpu-model.vendor_id"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[1].matchExpressions[0].operator | string | `"In"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[1].matchExpressions[0].values[0] | string | `"NVIDIA"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[2].matchExpressions[0].key | string | `"nvidia.com/gpu.present"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[2].matchExpressions[0].operator | string | `"In"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[2].matchExpressions[0].values[0] | string | `"true"` |  |
| allowDefaultNamespace | bool | `false` |  |
| cdi.nvidiaHookPath | string | `nil` |  |
| compatWithCPUManager | string | `nil` |  |
| config.default | string | `""` |  |
| config.fallbackStrategies[0] | string | `"named"` |  |
| config.fallbackStrategies[1] | string | `"single"` |  |
| config.map | object | `{}` |  |
| config.name | string | `""` |  |
| deviceDiscoveryStrategy | string | `nil` |  |
| deviceIDStrategy | string | `nil` |  |
| deviceListStrategy | string | `nil` |  |
| devicePlugin.enabled | bool | `true` |  |
| failOnInitError | string | `nil` |  |
| fullnameOverride | string | `""` |  |
| gdsEnabled | string | `nil` |  |
| gfd.enabled | bool | `false` |  |
| gfd.nameOverride | string | `"gpu-feature-discovery"` |  |
| gfd.namespaceOverride | string | `""` |  |
| gfd.noTimestamp | string | `nil` |  |
| gfd.securityContext.privileged | bool | `true` |  |
| gfd.sleepInterval | string | `nil` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"nvcr.io/nvidia/k8s-device-plugin"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| migStrategy | string | `nil` |  |
| mofedEnabled | string | `nil` |  |
| mps.enableHostPID | bool | `true` |  |
| mps.root | string | `"/run/nvidia/mps"` |  |
| nameOverride | string | `""` |  |
| namespaceOverride | string | `""` |  |
| nfd.enableNodeFeatureApi | bool | `false` |  |
| nfd.master.config.extraLabelNs[0] | string | `"nvidia.com"` |  |
| nfd.master.serviceAccount.create | bool | `true` |  |
| nfd.master.serviceAccount.name | string | `"node-feature-discovery"` |  |
| nfd.nameOverride | string | `"node-feature-discovery"` |  |
| nfd.worker.config.sources.pci.deviceClassWhitelist[0] | string | `"02"` |  |
| nfd.worker.config.sources.pci.deviceClassWhitelist[1] | string | `"03"` |  |
| nfd.worker.config.sources.pci.deviceLabelFields[0] | string | `"vendor"` |  |
| nfd.worker.tolerations[0].effect | string | `"NoSchedule"` |  |
| nfd.worker.tolerations[0].key | string | `"node-role.kubernetes.io/master"` |  |
| nfd.worker.tolerations[0].operator | string | `"Equal"` |  |
| nfd.worker.tolerations[0].value | string | `""` |  |
| nfd.worker.tolerations[1].effect | string | `"NoSchedule"` |  |
| nfd.worker.tolerations[1].key | string | `"nvidia.com/gpu"` |  |
| nfd.worker.tolerations[1].operator | string | `"Equal"` |  |
| nfd.worker.tolerations[1].value | string | `"present"` |  |
| nodeSelector | object | `{}` |  |
| nvidiaDriverRoot | string | `nil` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClassName | string | `"system-node-critical"` |  |
| resources | object | `{}` |  |
| runtimeClassName | string | `nil` |  |
| securityContext | object | `{}` |  |
| selectorLabelsOverride | object | `{}` |  |
| tolerations[0].key | string | `"CriticalAddonsOnly"` |  |
| tolerations[0].operator | string | `"Exists"` |  |
| tolerations[1].effect | string | `"NoSchedule"` |  |
| tolerations[1].key | string | `"nvidia.com/gpu"` |  |
| tolerations[1].operator | string | `"Exists"` |  |
| updateStrategy.type | string | `"RollingUpdate"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
