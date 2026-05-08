# jaeger

![Version: 3.3.1](https://img.shields.io/badge/Version-3.3.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.53.0](https://img.shields.io/badge/AppVersion-1.53.0-informational?style=flat-square)

A Jaeger Helm chart for Kubernetes

**Homepage:** <https://jaegertracing.io>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| dvonthenen | <david.vonthenen@dell.com> |  |
| mehta-ankit | <ankit.mehta@appian.com> |  |
| mikelorant | <michael.lorant@fairfaxmedia.com.au> |  |
| naseemkullah | <naseem@transit.app> |  |
| pavelnikolov | <me@pavelnikolov.net> |  |
| jkowall | <jkowall@kowall.net> |  |

## Source Code

* <https://hub.docker.com/u/jaegertracing/>

## Requirements

Kubernetes: `>= 1.21-0`

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | common | 2.x.x |
| https://charts.bitnami.com/bitnami | elasticsearch | 20.0.4 |
| https://charts.bitnami.com/bitnami | kafka | 26.6.2 |
| https://charts.helm.sh/incubator | cassandra | 0.15.3 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| agent.affinity | object | `{}` |  |
| agent.annotations | object | `{}` |  |
| agent.cmdlineParams | object | `{}` |  |
| agent.daemonset.updateStrategy | object | `{}` |  |
| agent.daemonset.useHostPort | bool | `false` |  |
| agent.dnsPolicy | string | `"ClusterFirst"` |  |
| agent.enabled | bool | `true` |  |
| agent.envFrom | list | `[]` |  |
| agent.extraConfigmapMounts | list | `[]` |  |
| agent.extraEnv | list | `[]` |  |
| agent.extraSecretMounts | list | `[]` |  |
| agent.image.digest | string | `""` |  |
| agent.image.pullPolicy | string | `"IfNotPresent"` |  |
| agent.image.pullSecrets | list | `[]` |  |
| agent.image.registry | string | `""` |  |
| agent.image.repository | string | `"jaegertracing/jaeger-agent"` |  |
| agent.image.tag | string | `""` |  |
| agent.initContainers | list | `[]` |  |
| agent.nodeSelector | object | `{}` |  |
| agent.podAnnotations | object | `{}` |  |
| agent.podLabels | object | `{}` |  |
| agent.podSecurityContext | object | `{}` |  |
| agent.priorityClassName | string | `""` |  |
| agent.resources | object | `{}` |  |
| agent.securityContext | object | `{}` |  |
| agent.service.annotations | object | `{}` |  |
| agent.service.binaryPort | int | `6832` |  |
| agent.service.compactPort | int | `6831` |  |
| agent.service.loadBalancerSourceRanges | list | `[]` |  |
| agent.service.samplingPort | int | `5778` |  |
| agent.service.type | string | `"ClusterIP"` |  |
| agent.service.zipkinThriftPort | int | `5775` |  |
| agent.serviceAccount.annotations | object | `{}` |  |
| agent.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| agent.serviceAccount.create | bool | `true` |  |
| agent.serviceAccount.name | string | `nil` |  |
| agent.serviceMonitor.additionalLabels | object | `{}` |  |
| agent.serviceMonitor.enabled | bool | `false` |  |
| agent.serviceMonitor.metricRelabelings | list | `[]` | ServiceMonitor metric relabel configs to apply to samples before ingestion https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint |
| agent.serviceMonitor.relabelings | list | `[]` |  |
| agent.tolerations | list | `[]` |  |
| agent.useHostNetwork | bool | `false` |  |
| allInOne.affinity | object | `{}` |  |
| allInOne.args | list | `[]` |  |
| allInOne.enabled | bool | `false` |  |
| allInOne.extraEnv | list | `[]` |  |
| allInOne.extraSecretMounts | list | `[]` |  |
| allInOne.image.digest | string | `""` |  |
| allInOne.image.pullPolicy | string | `"IfNotPresent"` |  |
| allInOne.image.pullSecrets | list | `[]` |  |
| allInOne.image.registry | string | `""` |  |
| allInOne.image.repository | string | `"jaegertracing/all-in-one"` |  |
| allInOne.image.tag | string | `""` |  |
| allInOne.ingress.annotations | object | `{}` |  |
| allInOne.ingress.enabled | bool | `false` |  |
| allInOne.ingress.labels | object | `{}` |  |
| allInOne.ingress.pathType | string | `nil` |  |
| allInOne.nodeSelector | object | `{}` |  |
| allInOne.podSecurityContext.fsGroup | int | `10001` |  |
| allInOne.podSecurityContext.runAsGroup | int | `10001` |  |
| allInOne.podSecurityContext.runAsUser | int | `10001` |  |
| allInOne.replicas | int | `1` |  |
| allInOne.securityContext | object | `{}` |  |
| allInOne.service.collector.otlp.grpc.name | string | `"otlp-grpc"` |  |
| allInOne.service.collector.otlp.http.name | string | `"otlp-http"` |  |
| allInOne.service.headless | bool | `true` |  |
| allInOne.serviceAccount.annotations | object | `{}` |  |
| allInOne.serviceAccount.automountServiceAccountToken | bool | `true` |  |
| allInOne.tolerations | list | `[]` |  |
| allInOne.topologySpreadContraints | list | `[]` |  |
| cassandra.config.cluster_name | string | `"jaeger"` |  |
| cassandra.config.dc_name | string | `"dc1"` |  |
| cassandra.config.endpoint_snitch | string | `"GossipingPropertyFileSnitch"` |  |
| cassandra.config.rack_name | string | `"rack1"` |  |
| cassandra.config.seed_size | int | `1` |  |
| cassandra.persistence.enabled | bool | `false` |  |
| collector.affinity | object | `{}` |  |
| collector.annotations | object | `{}` |  |
| collector.autoscaling.behavior | object | `{}` |  |
| collector.autoscaling.enabled | bool | `false` |  |
| collector.autoscaling.maxReplicas | int | `10` |  |
| collector.autoscaling.minReplicas | int | `2` |  |
| collector.basePath | string | `"/"` |  |
| collector.cmdlineParams | object | `{}` |  |
| collector.dnsPolicy | string | `"ClusterFirst"` |  |
| collector.enabled | bool | `true` |  |
| collector.envFrom | list | `[]` |  |
| collector.extraConfigmapMounts | list | `[]` |  |
| collector.extraEnv | list | `[]` |  |
| collector.extraSecretMounts | list | `[]` |  |
| collector.image.digest | string | `""` |  |
| collector.image.pullPolicy | string | `"IfNotPresent"` |  |
| collector.image.pullSecrets | list | `[]` |  |
| collector.image.registry | string | `""` |  |
| collector.image.repository | string | `"jaegertracing/jaeger-collector"` |  |
| collector.image.tag | string | `""` |  |
| collector.ingress.annotations | object | `{}` |  |
| collector.ingress.enabled | bool | `false` |  |
| collector.ingress.labels | object | `{}` |  |
| collector.ingress.pathType | string | `nil` |  |
| collector.initContainers | list | `[]` |  |
| collector.networkPolicy.enabled | bool | `false` |  |
| collector.nodeSelector | object | `{}` |  |
| collector.podAnnotations | object | `{}` |  |
| collector.podLabels | object | `{}` |  |
| collector.podSecurityContext | object | `{}` |  |
| collector.priorityClassName | string | `""` |  |
| collector.replicaCount | int | `1` |  |
| collector.resources | object | `{}` |  |
| collector.securityContext | object | `{}` |  |
| collector.service.admin.name | string | `"admin"` |  |
| collector.service.admin.targetPort | string | `"admin"` |  |
| collector.service.annotations | object | `{}` |  |
| collector.service.clusterIP | string | `""` |  |
| collector.service.grpc.port | int | `14250` |  |
| collector.service.http.port | int | `14268` |  |
| collector.service.loadBalancerIP | string | `""` |  |
| collector.service.loadBalancerSourceRanges | list | `[]` |  |
| collector.service.otlp.grpc | object | `{}` |  |
| collector.service.otlp.http | object | `{}` |  |
| collector.service.type | string | `"ClusterIP"` |  |
| collector.service.zipkin | object | `{}` |  |
| collector.serviceAccount.annotations | object | `{}` |  |
| collector.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| collector.serviceAccount.create | bool | `true` |  |
| collector.serviceAccount.name | string | `nil` |  |
| collector.serviceMonitor.additionalLabels | object | `{}` |  |
| collector.serviceMonitor.enabled | bool | `false` |  |
| collector.serviceMonitor.metricRelabelings | list | `[]` | ServiceMonitor metric relabel configs to apply to samples before ingestion https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint |
| collector.serviceMonitor.relabelings | list | `[]` |  |
| collector.tolerations | list | `[]` |  |
| elasticsearch | object | `{}` |  |
| esIndexCleaner.affinity | object | `{}` |  |
| esIndexCleaner.annotations | object | `{}` |  |
| esIndexCleaner.cmdlineParams | object | `{}` |  |
| esIndexCleaner.concurrencyPolicy | string | `"Forbid"` |  |
| esIndexCleaner.enabled | bool | `false` |  |
| esIndexCleaner.extraConfigmapMounts | list | `[]` |  |
| esIndexCleaner.extraEnv | list | `[]` |  |
| esIndexCleaner.extraSecretMounts | list | `[]` |  |
| esIndexCleaner.failedJobsHistoryLimit | int | `3` |  |
| esIndexCleaner.image.digest | string | `""` |  |
| esIndexCleaner.image.pullPolicy | string | `"IfNotPresent"` |  |
| esIndexCleaner.image.pullSecrets | list | `[]` |  |
| esIndexCleaner.image.registry | string | `""` |  |
| esIndexCleaner.image.repository | string | `"jaegertracing/jaeger-es-index-cleaner"` |  |
| esIndexCleaner.image.tag | string | `""` |  |
| esIndexCleaner.nodeSelector | object | `{}` |  |
| esIndexCleaner.numberOfDays | int | `7` |  |
| esIndexCleaner.podAnnotations | object | `{}` |  |
| esIndexCleaner.podLabels | object | `{}` |  |
| esIndexCleaner.podSecurityContext.runAsUser | int | `1000` |  |
| esIndexCleaner.resources | object | `{}` |  |
| esIndexCleaner.schedule | string | `"55 23 * * *"` |  |
| esIndexCleaner.securityContext.runAsUser | int | `1000` |  |
| esIndexCleaner.serviceAccount.annotations | object | `{}` |  |
| esIndexCleaner.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| esIndexCleaner.serviceAccount.create | bool | `true` |  |
| esIndexCleaner.serviceAccount.name | string | `nil` |  |
| esIndexCleaner.successfulJobsHistoryLimit | int | `3` |  |
| esIndexCleaner.tolerations | list | `[]` |  |
| esLookback.affinity | object | `{}` |  |
| esLookback.annotations | object | `{}` |  |
| esLookback.cmdlineParams | object | `{}` |  |
| esLookback.concurrencyPolicy | string | `"Forbid"` |  |
| esLookback.enabled | bool | `false` |  |
| esLookback.extraConfigmapMounts | list | `[]` |  |
| esLookback.extraEnv[0].name | string | `"UNIT"` |  |
| esLookback.extraEnv[0].value | string | `"days"` |  |
| esLookback.extraEnv[1].name | string | `"UNIT_COUNT"` |  |
| esLookback.extraEnv[1].value | string | `"7"` |  |
| esLookback.extraSecretMounts | list | `[]` |  |
| esLookback.failedJobsHistoryLimit | int | `3` |  |
| esLookback.image.digest | string | `""` |  |
| esLookback.image.pullPolicy | string | `"IfNotPresent"` |  |
| esLookback.image.pullSecrets | list | `[]` |  |
| esLookback.image.registry | string | `""` |  |
| esLookback.image.repository | string | `"jaegertracing/jaeger-es-rollover"` |  |
| esLookback.image.tag | string | `""` |  |
| esLookback.nodeSelector | object | `{}` |  |
| esLookback.podAnnotations | object | `{}` |  |
| esLookback.podLabels | object | `{}` |  |
| esLookback.podSecurityContext.runAsUser | int | `1000` |  |
| esLookback.resources | object | `{}` |  |
| esLookback.schedule | string | `"5 0 * * *"` |  |
| esLookback.securityContext | object | `{}` |  |
| esLookback.serviceAccount.annotations | object | `{}` |  |
| esLookback.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| esLookback.serviceAccount.create | bool | `true` |  |
| esLookback.serviceAccount.name | string | `nil` |  |
| esLookback.successfulJobsHistoryLimit | int | `3` |  |
| esLookback.tolerations | list | `[]` |  |
| esRollover.affinity | object | `{}` |  |
| esRollover.annotations | object | `{}` |  |
| esRollover.cmdlineParams | object | `{}` |  |
| esRollover.concurrencyPolicy | string | `"Forbid"` |  |
| esRollover.enabled | bool | `false` |  |
| esRollover.extraConfigmapMounts | list | `[]` |  |
| esRollover.extraEnv[0].name | string | `"CONDITIONS"` |  |
| esRollover.extraEnv[0].value | string | `"{\"max_age\": \"1d\"}"` |  |
| esRollover.extraSecretMounts | list | `[]` |  |
| esRollover.failedJobsHistoryLimit | int | `3` |  |
| esRollover.image.digest | string | `""` |  |
| esRollover.image.pullPolicy | string | `"IfNotPresent"` |  |
| esRollover.image.pullSecrets | list | `[]` |  |
| esRollover.image.registry | string | `""` |  |
| esRollover.image.repository | string | `"jaegertracing/jaeger-es-rollover"` |  |
| esRollover.image.tag | string | `""` |  |
| esRollover.initHook.annotations | object | `{}` |  |
| esRollover.initHook.extraEnv | list | `[]` |  |
| esRollover.initHook.podAnnotations | object | `{}` |  |
| esRollover.initHook.podLabels | object | `{}` |  |
| esRollover.initHook.ttlSecondsAfterFinished | int | `120` |  |
| esRollover.nodeSelector | object | `{}` |  |
| esRollover.podAnnotations | object | `{}` |  |
| esRollover.podLabels | object | `{}` |  |
| esRollover.podSecurityContext.runAsUser | int | `1000` |  |
| esRollover.resources | object | `{}` |  |
| esRollover.schedule | string | `"10 0 * * *"` |  |
| esRollover.securityContext | object | `{}` |  |
| esRollover.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| esRollover.serviceAccount.create | bool | `true` |  |
| esRollover.serviceAccount.name | string | `nil` |  |
| esRollover.successfulJobsHistoryLimit | int | `3` |  |
| esRollover.tolerations | list | `[]` |  |
| extraObjects | list | `[]` |  |
| fullnameOverride | string | `""` |  |
| global.imageRegistry | string | `nil` |  |
| hotrod.affinity | object | `{}` |  |
| hotrod.args[0] | string | `"all"` |  |
| hotrod.enabled | bool | `false` |  |
| hotrod.extraArgs | list | `[]` |  |
| hotrod.extraEnv | list | `[]` |  |
| hotrod.image.digest | string | `""` |  |
| hotrod.image.pullPolicy | string | `"IfNotPresent"` |  |
| hotrod.image.pullSecrets | list | `[]` |  |
| hotrod.image.registry | string | `""` |  |
| hotrod.image.repository | string | `"jaegertracing/example-hotrod"` |  |
| hotrod.image.tag | string | `""` |  |
| hotrod.ingress.annotations | object | `{}` |  |
| hotrod.ingress.enabled | bool | `false` |  |
| hotrod.ingress.hosts[0] | string | `"chart-example.local"` |  |
| hotrod.ingress.pathType | string | `nil` |  |
| hotrod.ingress.tls | string | `nil` |  |
| hotrod.nodeSelector | object | `{}` |  |
| hotrod.podSecurityContext | object | `{}` |  |
| hotrod.replicaCount | int | `1` |  |
| hotrod.resources | object | `{}` |  |
| hotrod.securityContext | object | `{}` |  |
| hotrod.service.annotations | object | `{}` |  |
| hotrod.service.loadBalancerSourceRanges | list | `[]` |  |
| hotrod.service.name | string | `"hotrod"` |  |
| hotrod.service.port | int | `80` |  |
| hotrod.service.type | string | `"ClusterIP"` |  |
| hotrod.serviceAccount.annotations | object | `{}` |  |
| hotrod.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| hotrod.serviceAccount.create | bool | `true` |  |
| hotrod.serviceAccount.name | string | `nil` |  |
| hotrod.tolerations | list | `[]` |  |
| hotrod.tracing.host | string | `nil` |  |
| hotrod.tracing.port | int | `6831` |  |
| ingester.affinity | object | `{}` |  |
| ingester.annotations | object | `{}` |  |
| ingester.autoscaling.behavior | object | `{}` |  |
| ingester.autoscaling.enabled | bool | `false` |  |
| ingester.autoscaling.maxReplicas | int | `10` |  |
| ingester.autoscaling.minReplicas | int | `2` |  |
| ingester.cmdlineParams | object | `{}` |  |
| ingester.dnsPolicy | string | `"ClusterFirst"` |  |
| ingester.enabled | bool | `false` |  |
| ingester.envFrom | list | `[]` |  |
| ingester.extraConfigmapMounts | list | `[]` |  |
| ingester.extraEnv | list | `[]` |  |
| ingester.extraSecretMounts | list | `[]` |  |
| ingester.image.digest | string | `""` |  |
| ingester.image.pullPolicy | string | `"IfNotPresent"` |  |
| ingester.image.pullSecrets | list | `[]` |  |
| ingester.image.registry | string | `""` |  |
| ingester.image.repository | string | `"jaegertracing/jaeger-ingester"` |  |
| ingester.image.tag | string | `""` |  |
| ingester.initContainers | list | `[]` |  |
| ingester.nodeSelector | object | `{}` |  |
| ingester.podAnnotations | object | `{}` |  |
| ingester.podLabels | object | `{}` |  |
| ingester.podSecurityContext | object | `{}` |  |
| ingester.replicaCount | int | `1` |  |
| ingester.resources | object | `{}` |  |
| ingester.securityContext | object | `{}` |  |
| ingester.service.annotations | object | `{}` |  |
| ingester.service.loadBalancerSourceRanges | list | `[]` |  |
| ingester.service.type | string | `"ClusterIP"` |  |
| ingester.serviceAccount.annotations | object | `{}` |  |
| ingester.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| ingester.serviceAccount.create | bool | `true` |  |
| ingester.serviceAccount.name | string | `nil` |  |
| ingester.serviceMonitor.additionalLabels | object | `{}` |  |
| ingester.serviceMonitor.enabled | bool | `false` |  |
| ingester.serviceMonitor.metricRelabelings | list | `[]` | ServiceMonitor metric relabel configs to apply to samples before ingestion https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint |
| ingester.serviceMonitor.relabelings | list | `[]` |  |
| ingester.tolerations | list | `[]` |  |
| kafka.controller.extraConfig | string | `"auto.create.topics.enable=true\n"` |  |
| kafka.controller.replicaCount | int | `3` |  |
| kafka.listeners.client.protocol | string | `"PLAINTEXT"` |  |
| kafka.listeners.controller.protocol | string | `"PLAINTEXT"` |  |
| kafka.listeners.external.protocol | string | `"PLAINTEXT"` |  |
| kafka.listeners.interbroker.protocol | string | `"PLAINTEXT"` |  |
| nameOverride | string | `""` |  |
| networkPolicy.enabled | bool | `false` |  |
| provisionDataStore.cassandra | bool | `true` |  |
| provisionDataStore.elasticsearch | bool | `false` |  |
| provisionDataStore.kafka | bool | `false` |  |
| query.affinity | object | `{}` |  |
| query.agentSidecar.enabled | bool | `true` |  |
| query.annotations | object | `{}` |  |
| query.basePath | string | `"/"` |  |
| query.cmdlineParams | object | `{}` |  |
| query.dnsPolicy | string | `"ClusterFirst"` |  |
| query.enabled | bool | `true` |  |
| query.envFrom | list | `[]` |  |
| query.extraConfigmapMounts | list | `[]` |  |
| query.extraEnv | list | `[]` |  |
| query.extraVolumes | list | `[]` |  |
| query.image.digest | string | `""` |  |
| query.image.pullPolicy | string | `"IfNotPresent"` |  |
| query.image.pullSecrets | list | `[]` |  |
| query.image.registry | string | `""` |  |
| query.image.repository | string | `"jaegertracing/jaeger-query"` |  |
| query.image.tag | string | `""` |  |
| query.ingress.annotations | object | `{}` |  |
| query.ingress.enabled | bool | `false` |  |
| query.ingress.health.exposed | bool | `false` |  |
| query.ingress.labels | object | `{}` |  |
| query.ingress.pathType | string | `nil` |  |
| query.initContainers | list | `[]` |  |
| query.networkPolicy.enabled | bool | `false` |  |
| query.nodeSelector | object | `{}` |  |
| query.oAuthSidecar.args | list | `[]` |  |
| query.oAuthSidecar.containerPort | int | `4180` |  |
| query.oAuthSidecar.enabled | bool | `false` |  |
| query.oAuthSidecar.extraConfigmapMounts | list | `[]` |  |
| query.oAuthSidecar.extraEnv | list | `[]` |  |
| query.oAuthSidecar.extraSecretMounts | list | `[]` |  |
| query.oAuthSidecar.image.digest | string | `""` |  |
| query.oAuthSidecar.image.pullPolicy | string | `"IfNotPresent"` |  |
| query.oAuthSidecar.image.pullSecrets | list | `[]` |  |
| query.oAuthSidecar.image.registry | string | `"quay.io"` |  |
| query.oAuthSidecar.image.repository | string | `"oauth2-proxy/oauth2-proxy"` |  |
| query.oAuthSidecar.image.tag | string | `"v7.6.0"` |  |
| query.oAuthSidecar.resources | object | `{}` |  |
| query.podAnnotations | object | `{}` |  |
| query.podLabels | object | `{}` |  |
| query.podSecurityContext | object | `{}` |  |
| query.priorityClassName | string | `""` |  |
| query.replicaCount | int | `1` |  |
| query.resources | object | `{}` |  |
| query.securityContext | object | `{}` |  |
| query.service.admin.name | string | `"admin"` |  |
| query.service.admin.targetPort | string | `"admin"` |  |
| query.service.annotations | object | `{}` |  |
| query.service.loadBalancerSourceRanges | list | `[]` |  |
| query.service.port | int | `80` |  |
| query.service.type | string | `"ClusterIP"` |  |
| query.serviceAccount.annotations | object | `{}` |  |
| query.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| query.serviceAccount.create | bool | `true` |  |
| query.serviceAccount.name | string | `nil` |  |
| query.serviceMonitor.additionalLabels | object | `{}` |  |
| query.serviceMonitor.enabled | bool | `false` |  |
| query.serviceMonitor.metricRelabelings | list | `[]` | ServiceMonitor metric relabel configs to apply to samples before ingestion https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint |
| query.serviceMonitor.relabelings | list | `[]` |  |
| query.sidecars | list | `[]` |  |
| query.tolerations | list | `[]` |  |
| schema.activeDeadlineSeconds | int | `300` |  |
| schema.annotations | object | `{}` |  |
| schema.extraEnv | list | `[]` |  |
| schema.image.digest | string | `""` |  |
| schema.image.pullPolicy | string | `"IfNotPresent"` |  |
| schema.image.pullSecrets | list | `[]` |  |
| schema.image.registry | string | `""` |  |
| schema.image.repository | string | `"jaegertracing/jaeger-cassandra-schema"` |  |
| schema.image.tag | string | `""` |  |
| schema.podAnnotations | object | `{}` |  |
| schema.podLabels | object | `{}` |  |
| schema.podSecurityContext | object | `{}` |  |
| schema.resources | object | `{}` |  |
| schema.securityContext | object | `{}` |  |
| schema.serviceAccount.automountServiceAccountToken | bool | `true` |  |
| schema.serviceAccount.create | bool | `true` |  |
| schema.serviceAccount.name | string | `nil` |  |
| schema.tolerations | list | `[]` |  |
| spark.affinity | object | `{}` |  |
| spark.annotations | object | `{}` |  |
| spark.cmdlineParams | object | `{}` |  |
| spark.concurrencyPolicy | string | `"Forbid"` |  |
| spark.enabled | bool | `false` |  |
| spark.extraConfigmapMounts | list | `[]` |  |
| spark.extraEnv | list | `[]` |  |
| spark.extraSecretMounts | list | `[]` |  |
| spark.failedJobsHistoryLimit | int | `5` |  |
| spark.image.digest | string | `""` |  |
| spark.image.pullPolicy | string | `"IfNotPresent"` |  |
| spark.image.pullSecrets | list | `[]` |  |
| spark.image.registry | string | `""` |  |
| spark.image.repository | string | `"jaegertracing/spark-dependencies"` |  |
| spark.image.tag | string | `"latest"` |  |
| spark.nodeSelector | object | `{}` |  |
| spark.podAnnotations | object | `{}` |  |
| spark.podLabels | object | `{}` |  |
| spark.podSecurityContext | object | `{}` |  |
| spark.resources | object | `{}` |  |
| spark.schedule | string | `"49 23 * * *"` |  |
| spark.securityContext | object | `{}` |  |
| spark.serviceAccount.annotations | object | `{}` |  |
| spark.serviceAccount.automountServiceAccountToken | bool | `false` |  |
| spark.serviceAccount.create | bool | `true` |  |
| spark.serviceAccount.name | string | `nil` |  |
| spark.successfulJobsHistoryLimit | int | `5` |  |
| spark.tolerations | list | `[]` |  |
| storage.badger.ephemeral | bool | `true` |  |
| storage.badger.extraEnv | list | `[]` |  |
| storage.badger.persistence.mountPath | string | `"/mnt/data"` |  |
| storage.badger.persistence.useExistingPvcName | string | `""` |  |
| storage.cassandra.cmdlineParams | object | `{}` |  |
| storage.cassandra.extraEnv | list | `[]` |  |
| storage.cassandra.host | string | `"cassandra"` |  |
| storage.cassandra.keyspace | string | `"jaeger_v1_test"` |  |
| storage.cassandra.password | string | `"password"` |  |
| storage.cassandra.port | int | `9042` |  |
| storage.cassandra.schemaJobEnabled | bool | `true` |  |
| storage.cassandra.tls.enabled | bool | `false` |  |
| storage.cassandra.tls.secretName | string | `"cassandra-tls-secret"` |  |
| storage.cassandra.usePassword | bool | `true` |  |
| storage.cassandra.user | string | `"user"` |  |
| storage.elasticsearch.anonymous | bool | `false` |  |
| storage.elasticsearch.cmdlineParams | object | `{}` |  |
| storage.elasticsearch.extraEnv | list | `[]` |  |
| storage.elasticsearch.host | string | `"elasticsearch-master"` |  |
| storage.elasticsearch.nodesWanOnly | bool | `false` |  |
| storage.elasticsearch.password | string | `"changeme"` |  |
| storage.elasticsearch.port | int | `9200` |  |
| storage.elasticsearch.scheme | string | `"http"` |  |
| storage.elasticsearch.tls.ca | string | `"/es-tls/ca-cert.pem"` |  |
| storage.elasticsearch.tls.enabled | bool | `false` |  |
| storage.elasticsearch.tls.mountPath | string | `"/es-tls/ca-cert.pem"` |  |
| storage.elasticsearch.tls.secretName | string | `"es-tls-secret"` |  |
| storage.elasticsearch.tls.subPath | string | `"ca-cert.pem"` |  |
| storage.elasticsearch.usePassword | bool | `true` |  |
| storage.elasticsearch.user | string | `"elastic"` |  |
| storage.grpcPlugin.extraEnv | list | `[]` |  |
| storage.kafka.authentication | string | `"none"` |  |
| storage.kafka.brokers[0] | string | `"kafka:9092"` |  |
| storage.kafka.extraEnv | list | `[]` |  |
| storage.kafka.topic | string | `"jaeger_v1_test"` |  |
| storage.memory.extraEnv | list | `[]` |  |
| storage.type | string | `"cassandra"` |  |
| tag | string | `""` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
