# opentelemetry-demo

![Version: 0.33.1](https://img.shields.io/badge/Version-0.33.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.12.0](https://img.shields.io/badge/AppVersion-1.12.0-informational?style=flat-square)

opentelemetry demo helm chart

**Homepage:** <https://opentelemetry.io/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| dmitryax |  |  |
| jaronoff97 |  |  |
| puckpuck |  |  |
| tylerhelmuth |  |  |

## Source Code

* <https://github.com/open-telemetry/opentelemetry-demo>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://grafana.github.io/helm-charts | grafana | 8.5.6 |
| https://jaegertracing.github.io/helm-charts | jaeger | 3.3.1 |
| https://open-telemetry.github.io/opentelemetry-helm-charts | opentelemetry-collector | 0.107.0 |
| https://opensearch-project.github.io/helm-charts | opensearch | 2.26.0 |
| https://prometheus-community.github.io/helm-charts | prometheus | 25.27.0 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| components.accountingService.enabled | bool | `false` |  |
| components.accountingService.env[0].name | string | `"KAFKA_SERVICE_ADDR"` |  |
| components.accountingService.env[0].value | string | `"{{ include \"otel-demo.name\" . }}-kafka:9092"` |  |
| components.accountingService.env[1].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.accountingService.env[1].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.accountingService.initContainers[0].command[0] | string | `"sh"` |  |
| components.accountingService.initContainers[0].command[1] | string | `"-c"` |  |
| components.accountingService.initContainers[0].command[2] | string | `"until nc -z -v -w30 {{ include \"otel-demo.name\" . }}-kafka 9092; do echo waiting for kafka; sleep 2; done;"` |  |
| components.accountingService.initContainers[0].image | string | `"busybox:latest"` |  |
| components.accountingService.initContainers[0].name | string | `"wait-for-kafka"` |  |
| components.accountingService.resources.limits.memory | string | `"120Mi"` |  |
| components.accountingService.useDefault.env | bool | `true` |  |
| components.adService.enabled | bool | `false` |  |
| components.adService.env[0].name | string | `"AD_SERVICE_PORT"` |  |
| components.adService.env[0].value | string | `"8080"` |  |
| components.adService.env[1].name | string | `"FLAGD_HOST"` |  |
| components.adService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.adService.env[2].name | string | `"FLAGD_PORT"` |  |
| components.adService.env[2].value | string | `"8013"` |  |
| components.adService.env[3].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.adService.env[3].value | string | `"http://$(OTEL_COLLECTOR_NAME):4318"` |  |
| components.adService.env[4].name | string | `"OTEL_LOGS_EXPORTER"` |  |
| components.adService.env[4].value | string | `"otlp"` |  |
| components.adService.resources.limits.memory | string | `"300Mi"` |  |
| components.adService.service.port | int | `8080` |  |
| components.adService.useDefault.env | bool | `true` |  |
| components.cartService.enabled | bool | `false` |  |
| components.cartService.env[0].name | string | `"CART_SERVICE_PORT"` |  |
| components.cartService.env[0].value | string | `"8080"` |  |
| components.cartService.env[1].name | string | `"ASPNETCORE_URLS"` |  |
| components.cartService.env[1].value | string | `"http://*:$(CART_SERVICE_PORT)"` |  |
| components.cartService.env[2].name | string | `"VALKEY_ADDR"` |  |
| components.cartService.env[2].value | string | `"{{ include \"otel-demo.name\" . }}-valkey:6379"` |  |
| components.cartService.env[3].name | string | `"FLAGD_HOST"` |  |
| components.cartService.env[3].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.cartService.env[4].name | string | `"FLAGD_PORT"` |  |
| components.cartService.env[4].value | string | `"8013"` |  |
| components.cartService.env[5].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.cartService.env[5].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.cartService.initContainers[0].command[0] | string | `"sh"` |  |
| components.cartService.initContainers[0].command[1] | string | `"-c"` |  |
| components.cartService.initContainers[0].command[2] | string | `"until nc -z -v -w30 {{ include \"otel-demo.name\" . }}-valkey 6379; do echo waiting for valkey; sleep 2; done;"` |  |
| components.cartService.initContainers[0].image | string | `"busybox:latest"` |  |
| components.cartService.initContainers[0].name | string | `"wait-for-valkey"` |  |
| components.cartService.resources.limits.memory | string | `"160Mi"` |  |
| components.cartService.service.port | int | `8080` |  |
| components.cartService.useDefault.env | bool | `true` |  |
| components.checkoutService.enabled | bool | `false` |  |
| components.checkoutService.env[0].name | string | `"CHECKOUT_SERVICE_PORT"` |  |
| components.checkoutService.env[0].value | string | `"8080"` |  |
| components.checkoutService.env[10].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.checkoutService.env[10].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.checkoutService.env[1].name | string | `"CART_SERVICE_ADDR"` |  |
| components.checkoutService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-cartservice:8080"` |  |
| components.checkoutService.env[2].name | string | `"CURRENCY_SERVICE_ADDR"` |  |
| components.checkoutService.env[2].value | string | `"{{ include \"otel-demo.name\" . }}-currencyservice:8080"` |  |
| components.checkoutService.env[3].name | string | `"EMAIL_SERVICE_ADDR"` |  |
| components.checkoutService.env[3].value | string | `"http://{{ include \"otel-demo.name\" . }}-emailservice:8080"` |  |
| components.checkoutService.env[4].name | string | `"PAYMENT_SERVICE_ADDR"` |  |
| components.checkoutService.env[4].value | string | `"{{ include \"otel-demo.name\" . }}-paymentservice:8080"` |  |
| components.checkoutService.env[5].name | string | `"PRODUCT_CATALOG_SERVICE_ADDR"` |  |
| components.checkoutService.env[5].value | string | `"{{ include \"otel-demo.name\" . }}-productcatalogservice:8080"` |  |
| components.checkoutService.env[6].name | string | `"SHIPPING_SERVICE_ADDR"` |  |
| components.checkoutService.env[6].value | string | `"{{ include \"otel-demo.name\" . }}-shippingservice:8080"` |  |
| components.checkoutService.env[7].name | string | `"KAFKA_SERVICE_ADDR"` |  |
| components.checkoutService.env[7].value | string | `"{{ include \"otel-demo.name\" . }}-kafka:9092"` |  |
| components.checkoutService.env[8].name | string | `"FLAGD_HOST"` |  |
| components.checkoutService.env[8].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.checkoutService.env[9].name | string | `"FLAGD_PORT"` |  |
| components.checkoutService.env[9].value | string | `"8013"` |  |
| components.checkoutService.initContainers[0].command[0] | string | `"sh"` |  |
| components.checkoutService.initContainers[0].command[1] | string | `"-c"` |  |
| components.checkoutService.initContainers[0].command[2] | string | `"until nc -z -v -w30 {{ include \"otel-demo.name\" . }}-kafka 9092; do echo waiting for kafka; sleep 2; done;"` |  |
| components.checkoutService.initContainers[0].image | string | `"busybox:latest"` |  |
| components.checkoutService.initContainers[0].name | string | `"wait-for-kafka"` |  |
| components.checkoutService.resources.limits.memory | string | `"20Mi"` |  |
| components.checkoutService.service.port | int | `8080` |  |
| components.checkoutService.useDefault.env | bool | `true` |  |
| components.currencyService.enabled | bool | `false` |  |
| components.currencyService.env[0].name | string | `"CURRENCY_SERVICE_PORT"` |  |
| components.currencyService.env[0].value | string | `"8080"` |  |
| components.currencyService.env[1].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.currencyService.env[1].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.currencyService.env[2].name | string | `"VERSION"` |  |
| components.currencyService.env[2].value | string | `"{{ .Chart.AppVersion }}"` |  |
| components.currencyService.resources.limits.memory | string | `"20Mi"` |  |
| components.currencyService.service.port | int | `8080` |  |
| components.currencyService.useDefault.env | bool | `true` |  |
| components.emailService.enabled | bool | `false` |  |
| components.emailService.env[0].name | string | `"EMAIL_SERVICE_PORT"` |  |
| components.emailService.env[0].value | string | `"8080"` |  |
| components.emailService.env[1].name | string | `"APP_ENV"` |  |
| components.emailService.env[1].value | string | `"production"` |  |
| components.emailService.env[2].name | string | `"OTEL_EXPORTER_OTLP_TRACES_ENDPOINT"` |  |
| components.emailService.env[2].value | string | `"http://$(OTEL_COLLECTOR_NAME):4318/v1/traces"` |  |
| components.emailService.resources.limits.memory | string | `"100Mi"` |  |
| components.emailService.service.port | int | `8080` |  |
| components.emailService.useDefault.env | bool | `true` |  |
| components.flagd.additionalVolumes[0].configMap.name | string | `"{{ include \"otel-demo.name\" . }}-flagd-config"` |  |
| components.flagd.additionalVolumes[0].name | string | `"config-ro"` |  |
| components.flagd.command[0] | string | `"/flagd-build"` |  |
| components.flagd.command[1] | string | `"start"` |  |
| components.flagd.command[2] | string | `"--uri"` |  |
| components.flagd.command[3] | string | `"file:./etc/flagd/demo.flagd.json"` |  |
| components.flagd.enabled | bool | `false` |  |
| components.flagd.env[0].name | string | `"FLAGD_METRICS_EXPORTER"` |  |
| components.flagd.env[0].value | string | `"otel"` |  |
| components.flagd.env[1].name | string | `"FLAGD_OTEL_COLLECTOR_URI"` |  |
| components.flagd.env[1].value | string | `"$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.flagd.imageOverride.repository | string | `"ghcr.io/open-feature/flagd"` |  |
| components.flagd.imageOverride.tag | string | `"v0.11.1"` |  |
| components.flagd.initContainers[0].command[0] | string | `"sh"` |  |
| components.flagd.initContainers[0].command[1] | string | `"-c"` |  |
| components.flagd.initContainers[0].command[2] | string | `"cp /config-ro/demo.flagd.json /config-rw/demo.flagd.json && cat /config-rw/demo.flagd.json"` |  |
| components.flagd.initContainers[0].image | string | `"busybox"` |  |
| components.flagd.initContainers[0].name | string | `"init-config"` |  |
| components.flagd.initContainers[0].volumeMounts[0].mountPath | string | `"/config-ro"` |  |
| components.flagd.initContainers[0].volumeMounts[0].name | string | `"config-ro"` |  |
| components.flagd.initContainers[0].volumeMounts[1].mountPath | string | `"/config-rw"` |  |
| components.flagd.initContainers[0].volumeMounts[1].name | string | `"config-rw"` |  |
| components.flagd.mountedEmptyDirs[0].mountPath | string | `"/etc/flagd"` |  |
| components.flagd.mountedEmptyDirs[0].name | string | `"config-rw"` |  |
| components.flagd.replicas | int | `1` |  |
| components.flagd.resources.limits.memory | string | `"50Mi"` |  |
| components.flagd.service.port | int | `8013` |  |
| components.flagd.sidecarContainers[0].env[0].name | string | `"FLAGD_METRICS_EXPORTER"` |  |
| components.flagd.sidecarContainers[0].env[0].value | string | `"otel"` |  |
| components.flagd.sidecarContainers[0].env[1].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.flagd.sidecarContainers[0].env[1].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.flagd.sidecarContainers[0].name | string | `"flagd-ui"` |  |
| components.flagd.sidecarContainers[0].resources.limits.memory | string | `"150Mi"` |  |
| components.flagd.sidecarContainers[0].service.port | int | `4000` |  |
| components.flagd.sidecarContainers[0].useDefault.env | bool | `true` |  |
| components.flagd.sidecarContainers[0].volumeMounts[0].mountPath | string | `"/app/data"` |  |
| components.flagd.sidecarContainers[0].volumeMounts[0].name | string | `"config-rw"` |  |
| components.flagd.useDefault.env | bool | `true` |  |
| components.frauddetectionService.enabled | bool | `false` |  |
| components.frauddetectionService.env[0].name | string | `"KAFKA_SERVICE_ADDR"` |  |
| components.frauddetectionService.env[0].value | string | `"{{ include \"otel-demo.name\" . }}-kafka:9092"` |  |
| components.frauddetectionService.env[1].name | string | `"FLAGD_HOST"` |  |
| components.frauddetectionService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.frauddetectionService.env[2].name | string | `"FLAGD_PORT"` |  |
| components.frauddetectionService.env[2].value | string | `"8013"` |  |
| components.frauddetectionService.env[3].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.frauddetectionService.env[3].value | string | `"http://$(OTEL_COLLECTOR_NAME):4318"` |  |
| components.frauddetectionService.initContainers[0].command[0] | string | `"sh"` |  |
| components.frauddetectionService.initContainers[0].command[1] | string | `"-c"` |  |
| components.frauddetectionService.initContainers[0].command[2] | string | `"until nc -z -v -w30 {{ include \"otel-demo.name\" . }}-kafka 9092; do echo waiting for kafka; sleep 2; done;"` |  |
| components.frauddetectionService.initContainers[0].image | string | `"busybox:latest"` |  |
| components.frauddetectionService.initContainers[0].name | string | `"wait-for-kafka"` |  |
| components.frauddetectionService.resources.limits.memory | string | `"300Mi"` |  |
| components.frauddetectionService.useDefault.env | bool | `true` |  |
| components.frontend.enabled | bool | `false` |  |
| components.frontend.env[0].name | string | `"FRONTEND_PORT"` |  |
| components.frontend.env[0].value | string | `"8080"` |  |
| components.frontend.env[10].name | string | `"FLAGD_PORT"` |  |
| components.frontend.env[10].value | string | `"8013"` |  |
| components.frontend.env[11].name | string | `"OTEL_COLLECTOR_HOST"` |  |
| components.frontend.env[11].value | string | `"$(OTEL_COLLECTOR_NAME)"` |  |
| components.frontend.env[12].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.frontend.env[12].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.frontend.env[13].name | string | `"WEB_OTEL_SERVICE_NAME"` |  |
| components.frontend.env[13].value | string | `"frontend-web"` |  |
| components.frontend.env[14].name | string | `"PUBLIC_OTEL_EXPORTER_OTLP_TRACES_ENDPOINT"` |  |
| components.frontend.env[14].value | string | `"http://localhost:8080/otlp-http/v1/traces"` |  |
| components.frontend.env[1].name | string | `"FRONTEND_ADDR"` |  |
| components.frontend.env[1].value | string | `":8080"` |  |
| components.frontend.env[2].name | string | `"AD_SERVICE_ADDR"` |  |
| components.frontend.env[2].value | string | `"{{ include \"otel-demo.name\" . }}-adservice:8080"` |  |
| components.frontend.env[3].name | string | `"CART_SERVICE_ADDR"` |  |
| components.frontend.env[3].value | string | `"{{ include \"otel-demo.name\" . }}-cartservice:8080"` |  |
| components.frontend.env[4].name | string | `"CHECKOUT_SERVICE_ADDR"` |  |
| components.frontend.env[4].value | string | `"{{ include \"otel-demo.name\" . }}-checkoutservice:8080"` |  |
| components.frontend.env[5].name | string | `"CURRENCY_SERVICE_ADDR"` |  |
| components.frontend.env[5].value | string | `"{{ include \"otel-demo.name\" . }}-currencyservice:8080"` |  |
| components.frontend.env[6].name | string | `"PRODUCT_CATALOG_SERVICE_ADDR"` |  |
| components.frontend.env[6].value | string | `"{{ include \"otel-demo.name\" . }}-productcatalogservice:8080"` |  |
| components.frontend.env[7].name | string | `"RECOMMENDATION_SERVICE_ADDR"` |  |
| components.frontend.env[7].value | string | `"{{ include \"otel-demo.name\" . }}-recommendationservice:8080"` |  |
| components.frontend.env[8].name | string | `"SHIPPING_SERVICE_ADDR"` |  |
| components.frontend.env[8].value | string | `"{{ include \"otel-demo.name\" . }}-shippingservice:8080"` |  |
| components.frontend.env[9].name | string | `"FLAGD_HOST"` |  |
| components.frontend.env[9].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.frontend.resources.limits.memory | string | `"250Mi"` |  |
| components.frontend.securityContext.runAsGroup | int | `1001` |  |
| components.frontend.securityContext.runAsNonRoot | bool | `true` |  |
| components.frontend.securityContext.runAsUser | int | `1001` |  |
| components.frontend.service.port | int | `8080` |  |
| components.frontend.useDefault.env | bool | `true` |  |
| components.frontendProxy.enabled | bool | `true` |  |
| components.frontendProxy.env[0].name | string | `"ENVOY_PORT"` |  |
| components.frontendProxy.env[0].value | string | `"8080"` |  |
| components.frontendProxy.env[10].name | string | `"IMAGE_PROVIDER_PORT"` |  |
| components.frontendProxy.env[10].value | string | `"8081"` |  |
| components.frontendProxy.env[11].name | string | `"JAEGER_SERVICE_HOST"` |  |
| components.frontendProxy.env[11].value | string | `"{{ include \"otel-demo.name\" . }}-jaeger-query"` |  |
| components.frontendProxy.env[12].name | string | `"JAEGER_SERVICE_PORT"` |  |
| components.frontendProxy.env[12].value | string | `"16686"` |  |
| components.frontendProxy.env[13].name | string | `"LOCUST_WEB_HOST"` |  |
| components.frontendProxy.env[13].value | string | `"{{ include \"otel-demo.name\" . }}-loadgenerator"` |  |
| components.frontendProxy.env[14].name | string | `"LOCUST_WEB_PORT"` |  |
| components.frontendProxy.env[14].value | string | `"8089"` |  |
| components.frontendProxy.env[15].name | string | `"OTEL_COLLECTOR_HOST"` |  |
| components.frontendProxy.env[15].value | string | `"$(OTEL_COLLECTOR_NAME)"` |  |
| components.frontendProxy.env[16].name | string | `"OTEL_COLLECTOR_PORT_GRPC"` |  |
| components.frontendProxy.env[16].value | string | `"4317"` |  |
| components.frontendProxy.env[17].name | string | `"OTEL_COLLECTOR_PORT_HTTP"` |  |
| components.frontendProxy.env[17].value | string | `"4318"` |  |
| components.frontendProxy.env[1].name | string | `"FLAGD_HOST"` |  |
| components.frontendProxy.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.frontendProxy.env[2].name | string | `"FLAGD_PORT"` |  |
| components.frontendProxy.env[2].value | string | `"8013"` |  |
| components.frontendProxy.env[3].name | string | `"FLAGD_UI_HOST"` |  |
| components.frontendProxy.env[3].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.frontendProxy.env[4].name | string | `"FLAGD_UI_PORT"` |  |
| components.frontendProxy.env[4].value | string | `"4000"` |  |
| components.frontendProxy.env[5].name | string | `"FRONTEND_HOST"` |  |
| components.frontendProxy.env[5].value | string | `"{{ include \"otel-demo.name\" . }}-frontend"` |  |
| components.frontendProxy.env[6].name | string | `"FRONTEND_PORT"` |  |
| components.frontendProxy.env[6].value | string | `"8080"` |  |
| components.frontendProxy.env[7].name | string | `"GRAFANA_SERVICE_HOST"` |  |
| components.frontendProxy.env[7].value | string | `"{{ include \"otel-demo.name\" . }}-grafana"` |  |
| components.frontendProxy.env[8].name | string | `"GRAFANA_SERVICE_PORT"` |  |
| components.frontendProxy.env[8].value | string | `"80"` |  |
| components.frontendProxy.env[9].name | string | `"IMAGE_PROVIDER_HOST"` |  |
| components.frontendProxy.env[9].value | string | `"{{ include \"otel-demo.name\" . }}-imageprovider"` |  |
| components.frontendProxy.ingress.enabled | bool | `true` |  |
| components.frontendProxy.ingress.hosts[0].host | string | `"monitoring.caiser.ornlkdi.org"` |  |
| components.frontendProxy.ingress.hosts[0].paths[0].path | string | `"/"` |  |
| components.frontendProxy.ingress.hosts[0].paths[0].pathType | string | `"Prefix"` |  |
| components.frontendProxy.ingress.hosts[0].paths[0].port | int | `8080` |  |
| components.frontendProxy.ingress.ingressClassName | string | `"nginx"` |  |
| components.frontendProxy.resources.limits.memory | string | `"50Mi"` |  |
| components.frontendProxy.securityContext.runAsGroup | int | `101` |  |
| components.frontendProxy.securityContext.runAsNonRoot | bool | `true` |  |
| components.frontendProxy.securityContext.runAsUser | int | `101` |  |
| components.frontendProxy.service.port | int | `8080` |  |
| components.frontendProxy.useDefault.env | bool | `true` |  |
| components.imageprovider.enabled | bool | `false` |  |
| components.imageprovider.env[0].name | string | `"IMAGE_PROVIDER_PORT"` |  |
| components.imageprovider.env[0].value | string | `"8081"` |  |
| components.imageprovider.env[1].name | string | `"OTEL_COLLECTOR_PORT_GRPC"` |  |
| components.imageprovider.env[1].value | string | `"4317"` |  |
| components.imageprovider.env[2].name | string | `"OTEL_COLLECTOR_HOST"` |  |
| components.imageprovider.env[2].value | string | `"$(OTEL_COLLECTOR_NAME)"` |  |
| components.imageprovider.resources.limits.memory | string | `"50Mi"` |  |
| components.imageprovider.service.port | int | `8081` |  |
| components.imageprovider.useDefault.env | bool | `true` |  |
| components.kafka.enabled | bool | `false` |  |
| components.kafka.env[0].name | string | `"KAFKA_ADVERTISED_LISTENERS"` |  |
| components.kafka.env[0].value | string | `"PLAINTEXT://{{ include \"otel-demo.name\" . }}-kafka:9092"` |  |
| components.kafka.env[1].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.kafka.env[1].value | string | `"http://$(OTEL_COLLECTOR_NAME):4318"` |  |
| components.kafka.env[2].name | string | `"KAFKA_HEAP_OPTS"` |  |
| components.kafka.env[2].value | string | `"-Xmx400M -Xms400M"` |  |
| components.kafka.ports[0].name | string | `"plaintext"` |  |
| components.kafka.ports[0].value | int | `9092` |  |
| components.kafka.ports[1].name | string | `"controller"` |  |
| components.kafka.ports[1].value | int | `9093` |  |
| components.kafka.replicas | int | `1` |  |
| components.kafka.resources.limits.memory | string | `"600Mi"` |  |
| components.kafka.securityContext.runAsGroup | int | `1000` |  |
| components.kafka.securityContext.runAsNonRoot | bool | `true` |  |
| components.kafka.securityContext.runAsUser | int | `1000` |  |
| components.kafka.useDefault.env | bool | `true` |  |
| components.loadgenerator.enabled | bool | `false` |  |
| components.loadgenerator.env[0].name | string | `"LOCUST_WEB_PORT"` |  |
| components.loadgenerator.env[0].value | string | `"8089"` |  |
| components.loadgenerator.env[10].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.loadgenerator.env[10].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.loadgenerator.env[1].name | string | `"LOCUST_USERS"` |  |
| components.loadgenerator.env[1].value | string | `"10"` |  |
| components.loadgenerator.env[2].name | string | `"LOCUST_SPAWN_RATE"` |  |
| components.loadgenerator.env[2].value | string | `"1"` |  |
| components.loadgenerator.env[3].name | string | `"LOCUST_HOST"` |  |
| components.loadgenerator.env[3].value | string | `"http://{{ include \"otel-demo.name\" . }}-frontendproxy:8080"` |  |
| components.loadgenerator.env[4].name | string | `"LOCUST_HEADLESS"` |  |
| components.loadgenerator.env[4].value | string | `"false"` |  |
| components.loadgenerator.env[5].name | string | `"LOCUST_AUTOSTART"` |  |
| components.loadgenerator.env[5].value | string | `"true"` |  |
| components.loadgenerator.env[6].name | string | `"LOCUST_BROWSER_TRAFFIC_ENABLED"` |  |
| components.loadgenerator.env[6].value | string | `"true"` |  |
| components.loadgenerator.env[7].name | string | `"PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION"` |  |
| components.loadgenerator.env[7].value | string | `"python"` |  |
| components.loadgenerator.env[8].name | string | `"FLAGD_HOST"` |  |
| components.loadgenerator.env[8].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.loadgenerator.env[9].name | string | `"FLAGD_PORT"` |  |
| components.loadgenerator.env[9].value | string | `"8013"` |  |
| components.loadgenerator.resources.limits.memory | string | `"1Gi"` |  |
| components.loadgenerator.service.port | int | `8089` |  |
| components.loadgenerator.useDefault.env | bool | `true` |  |
| components.paymentService.enabled | bool | `false` |  |
| components.paymentService.env[0].name | string | `"PAYMENT_SERVICE_PORT"` |  |
| components.paymentService.env[0].value | string | `"8080"` |  |
| components.paymentService.env[1].name | string | `"FLAGD_HOST"` |  |
| components.paymentService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.paymentService.env[2].name | string | `"FLAGD_PORT"` |  |
| components.paymentService.env[2].value | string | `"8013"` |  |
| components.paymentService.env[3].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.paymentService.env[3].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.paymentService.resources.limits.memory | string | `"120Mi"` |  |
| components.paymentService.securityContext.runAsGroup | int | `1000` |  |
| components.paymentService.securityContext.runAsNonRoot | bool | `true` |  |
| components.paymentService.securityContext.runAsUser | int | `1000` |  |
| components.paymentService.service.port | int | `8080` |  |
| components.paymentService.useDefault.env | bool | `true` |  |
| components.productCatalogService.enabled | bool | `false` |  |
| components.productCatalogService.env[0].name | string | `"PRODUCT_CATALOG_SERVICE_PORT"` |  |
| components.productCatalogService.env[0].value | string | `"8080"` |  |
| components.productCatalogService.env[1].name | string | `"FLAGD_HOST"` |  |
| components.productCatalogService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.productCatalogService.env[2].name | string | `"FLAGD_PORT"` |  |
| components.productCatalogService.env[2].value | string | `"8013"` |  |
| components.productCatalogService.env[3].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.productCatalogService.env[3].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.productCatalogService.resources.limits.memory | string | `"20Mi"` |  |
| components.productCatalogService.service.port | int | `8080` |  |
| components.productCatalogService.useDefault.env | bool | `true` |  |
| components.quoteService.enabled | bool | `false` |  |
| components.quoteService.env[0].name | string | `"QUOTE_SERVICE_PORT"` |  |
| components.quoteService.env[0].value | string | `"8080"` |  |
| components.quoteService.env[1].name | string | `"OTEL_PHP_AUTOLOAD_ENABLED"` |  |
| components.quoteService.env[1].value | string | `"true"` |  |
| components.quoteService.env[2].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.quoteService.env[2].value | string | `"http://$(OTEL_COLLECTOR_NAME):4318"` |  |
| components.quoteService.resources.limits.memory | string | `"40Mi"` |  |
| components.quoteService.securityContext.runAsGroup | int | `33` |  |
| components.quoteService.securityContext.runAsNonRoot | bool | `true` |  |
| components.quoteService.securityContext.runAsUser | int | `33` |  |
| components.quoteService.service.port | int | `8080` |  |
| components.quoteService.useDefault.env | bool | `true` |  |
| components.recommendationService.enabled | bool | `false` |  |
| components.recommendationService.env[0].name | string | `"RECOMMENDATION_SERVICE_PORT"` |  |
| components.recommendationService.env[0].value | string | `"8080"` |  |
| components.recommendationService.env[1].name | string | `"PRODUCT_CATALOG_SERVICE_ADDR"` |  |
| components.recommendationService.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-productcatalogservice:8080"` |  |
| components.recommendationService.env[2].name | string | `"OTEL_PYTHON_LOG_CORRELATION"` |  |
| components.recommendationService.env[2].value | string | `"true"` |  |
| components.recommendationService.env[3].name | string | `"PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION"` |  |
| components.recommendationService.env[3].value | string | `"python"` |  |
| components.recommendationService.env[4].name | string | `"FLAGD_HOST"` |  |
| components.recommendationService.env[4].value | string | `"{{ include \"otel-demo.name\" . }}-flagd"` |  |
| components.recommendationService.env[5].name | string | `"FLAGD_PORT"` |  |
| components.recommendationService.env[5].value | string | `"8013"` |  |
| components.recommendationService.env[6].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.recommendationService.env[6].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.recommendationService.resources.limits.memory | string | `"500Mi"` |  |
| components.recommendationService.service.port | int | `8080` |  |
| components.recommendationService.useDefault.env | bool | `true` |  |
| components.shippingService.enabled | bool | `false` |  |
| components.shippingService.env[0].name | string | `"SHIPPING_SERVICE_PORT"` |  |
| components.shippingService.env[0].value | string | `"8080"` |  |
| components.shippingService.env[1].name | string | `"QUOTE_SERVICE_ADDR"` |  |
| components.shippingService.env[1].value | string | `"http://{{ include \"otel-demo.name\" . }}-quoteservice:8080"` |  |
| components.shippingService.env[2].name | string | `"OTEL_EXPORTER_OTLP_ENDPOINT"` |  |
| components.shippingService.env[2].value | string | `"http://$(OTEL_COLLECTOR_NAME):4317"` |  |
| components.shippingService.resources.limits.memory | string | `"20Mi"` |  |
| components.shippingService.service.port | int | `8080` |  |
| components.shippingService.useDefault.env | bool | `true` |  |
| components.valkey.enabled | bool | `false` |  |
| components.valkey.imageOverride.repository | string | `"valkey/valkey"` |  |
| components.valkey.imageOverride.tag | string | `"7.2-alpine"` |  |
| components.valkey.ports[0].name | string | `"valkey"` |  |
| components.valkey.ports[0].value | int | `6379` |  |
| components.valkey.replicas | int | `1` |  |
| components.valkey.resources.limits.memory | string | `"20Mi"` |  |
| components.valkey.securityContext.runAsGroup | int | `1000` |  |
| components.valkey.securityContext.runAsNonRoot | bool | `true` |  |
| components.valkey.securityContext.runAsUser | int | `999` |  |
| components.valkey.useDefault.env | bool | `true` |  |
| default.envOverrides[0].name | string | `"OTEL_COLLECTOR_NAME"` |  |
| default.envOverrides[0].value | string | `"$(OTEL_K8S_NODE_NAME)"` |  |
| default.env[0].name | string | `"OTEL_SERVICE_NAME"` |  |
| default.env[0].valueFrom.fieldRef.apiVersion | string | `"v1"` |  |
| default.env[0].valueFrom.fieldRef.fieldPath | string | `"metadata.labels['app.kubernetes.io/component']"` |  |
| default.env[1].name | string | `"OTEL_COLLECTOR_NAME"` |  |
| default.env[1].value | string | `"{{ include \"otel-demo.name\" . }}-otelcol"` |  |
| default.env[2].name | string | `"OTEL_EXPORTER_OTLP_METRICS_TEMPORALITY_PREFERENCE"` |  |
| default.env[2].value | string | `"cumulative"` |  |
| default.env[3].name | string | `"OTEL_RESOURCE_ATTRIBUTES"` |  |
| default.env[3].value | string | `"service.name=$(OTEL_SERVICE_NAME),service.namespace=opentelemetry-demo,service.version={{ .Chart.AppVersion }}"` |  |
| default.image.pullPolicy | string | `"Always"` |  |
| default.image.pullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| default.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/open-telemetry/demo"` |  |
| default.image.tag | string | `"1.12.0"` |  |
| default.replicas | int | `1` |  |
| default.revisionHistoryLimit | int | `10` |  |
| default.schedulingRules.affinity | object | `{}` |  |
| default.schedulingRules.nodeSelector | object | `{}` |  |
| default.schedulingRules.tolerations | list | `[]` |  |
| default.securityContext | object | `{}` |  |
| grafana."grafana.ini"."auth.anonymous".enabled | bool | `true` |  |
| grafana."grafana.ini"."auth.anonymous".org_name | string | `"Main Org."` |  |
| grafana."grafana.ini"."auth.anonymous".org_role | string | `"Admin"` |  |
| grafana."grafana.ini".auth.disable_login_form | bool | `false` |  |
| grafana."grafana.ini".server.root_url | string | `"%(protocol)s://%(domain)s:%(http_port)s/grafana"` |  |
| grafana."grafana.ini".server.serve_from_sub_path | bool | `true` |  |
| grafana.adminPassword | string | `"admin"` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".apiVersion | int | `1` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].disableDeletion | bool | `false` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].editable | bool | `true` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].folder | string | `""` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].name | string | `"default"` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].options.path | string | `"/var/lib/grafana/dashboards/default"` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].orgId | int | `1` |  |
| grafana.dashboardProviders."dashboardproviders.yaml".providers[0].type | string | `"file"` |  |
| grafana.dashboardsConfigMaps.default | string | `"{{ include \"otel-demo.name\" . }}-grafana-dashboards"` |  |
| grafana.datasources."datasources.yaml".apiVersion | int | `1` |  |
| grafana.datasources."datasources.yaml".datasources[0].editable | bool | `true` |  |
| grafana.datasources."datasources.yaml".datasources[0].isDefault | bool | `true` |  |
| grafana.datasources."datasources.yaml".datasources[0].jsonData.exemplarTraceIdDestinations[0].datasourceUid | string | `"webstore-traces"` |  |
| grafana.datasources."datasources.yaml".datasources[0].jsonData.exemplarTraceIdDestinations[0].name | string | `"trace_id"` |  |
| grafana.datasources."datasources.yaml".datasources[0].jsonData.exemplarTraceIdDestinations[1].name | string | `"trace_id"` |  |
| grafana.datasources."datasources.yaml".datasources[0].jsonData.exemplarTraceIdDestinations[1].url | string | `"http://localhost:8080/jaeger/ui/trace/$${__value.raw}"` |  |
| grafana.datasources."datasources.yaml".datasources[0].jsonData.exemplarTraceIdDestinations[1].urlDisplayLabel | string | `"View in Jaeger UI"` |  |
| grafana.datasources."datasources.yaml".datasources[0].name | string | `"Prometheus"` |  |
| grafana.datasources."datasources.yaml".datasources[0].type | string | `"prometheus"` |  |
| grafana.datasources."datasources.yaml".datasources[0].uid | string | `"webstore-metrics"` |  |
| grafana.datasources."datasources.yaml".datasources[0].url | string | `"http://{{ include \"otel-demo.name\" . }}-prometheus-server:9090"` |  |
| grafana.datasources."datasources.yaml".datasources[1].editable | bool | `true` |  |
| grafana.datasources."datasources.yaml".datasources[1].isDefault | bool | `false` |  |
| grafana.datasources."datasources.yaml".datasources[1].name | string | `"Jaeger"` |  |
| grafana.datasources."datasources.yaml".datasources[1].type | string | `"jaeger"` |  |
| grafana.datasources."datasources.yaml".datasources[1].uid | string | `"webstore-traces"` |  |
| grafana.datasources."datasources.yaml".datasources[1].url | string | `"http://{{ include \"otel-demo.name\" . }}-jaeger-query:16686/jaeger/ui"` |  |
| grafana.enabled | bool | `true` |  |
| grafana.image.pullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| grafana.image.registry | string | `"code-caiser.caiser.ornlkdi.org:5050"` |  |
| grafana.image.repository | string | `"inl001/coreii-data-lake/grafana/grafana"` |  |
| grafana.image.tag | string | `"main-17-01-25"` |  |
| grafana.resources.limits.memory | string | `"150Mi"` |  |
| jaeger.agent.enabled | bool | `false` |  |
| jaeger.allInOne.args[0] | string | `"--memory.max-traces=5000"` |  |
| jaeger.allInOne.args[1] | string | `"--query.base-path=/jaeger/ui"` |  |
| jaeger.allInOne.args[2] | string | `"--prometheus.server-url=http://{{ include \"otel-demo.name\" . }}-prometheus-server:9090"` |  |
| jaeger.allInOne.args[3] | string | `"--prometheus.query.normalize-calls=true"` |  |
| jaeger.allInOne.args[4] | string | `"--prometheus.query.normalize-duration=true"` |  |
| jaeger.allInOne.enabled | bool | `true` |  |
| jaeger.allInOne.extraEnv[0].name | string | `"METRICS_STORAGE_TYPE"` |  |
| jaeger.allInOne.extraEnv[0].value | string | `"prometheus"` |  |
| jaeger.allInOne.extraEnv[1].name | string | `"COLLECTOR_OTLP_GRPC_HOST_PORT"` |  |
| jaeger.allInOne.extraEnv[1].value | string | `"0.0.0.0:4317"` |  |
| jaeger.allInOne.extraEnv[2].name | string | `"COLLECTOR_OTLP_HTTP_HOST_PORT"` |  |
| jaeger.allInOne.extraEnv[2].value | string | `"0.0.0.0:4318"` |  |
| jaeger.allInOne.image.pullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| jaeger.allInOne.image.registry | string | `"code-caiser.caiser.ornlkdi.org:5050"` |  |
| jaeger.allInOne.image.repository | string | `"inl001/coreii-data-lake/jaegertracing/all-in-one"` |  |
| jaeger.allInOne.image.tag | string | `"1.65.0-17_01_25"` |  |
| jaeger.allInOne.resources.limits.memory | string | `"400Mi"` |  |
| jaeger.collector.enabled | bool | `false` |  |
| jaeger.enabled | bool | `true` |  |
| jaeger.provisionDataStore.cassandra | bool | `false` |  |
| jaeger.query.enabled | bool | `false` |  |
| jaeger.storage.type | string | `"memory"` |  |
| opensearch.clusterName | string | `"demo-cluster"` |  |
| opensearch.enabled | bool | `false` |  |
| opensearch.extraEnvs[0].name | string | `"bootstrap.memory_lock"` |  |
| opensearch.extraEnvs[0].value | string | `"true"` |  |
| opensearch.extraEnvs[1].name | string | `"DISABLE_INSTALL_DEMO_CONFIG"` |  |
| opensearch.extraEnvs[1].value | string | `"true"` |  |
| opensearch.extraEnvs[2].name | string | `"DISABLE_SECURITY_PLUGIN"` |  |
| opensearch.extraEnvs[2].value | string | `"true"` |  |
| opensearch.fullnameOverride | string | `"otel-demo-opensearch"` |  |
| opensearch.nodeGroup | string | `"otel-demo"` |  |
| opensearch.opensearchJavaOpts | string | `"-Xms300m -Xmx300m"` |  |
| opensearch.persistence.enabled | bool | `false` |  |
| opensearch.resources.limits.memory | string | `"1Gi"` |  |
| opensearch.singleNode | bool | `true` |  |
| opentelemetry-collector.config.connectors.spanmetrics | object | `{}` |  |
| opentelemetry-collector.config.exporters.opensearch.http.endpoint | string | `"http://otel-demo-opensearch:9200"` |  |
| opentelemetry-collector.config.exporters.opensearch.http.tls.insecure | bool | `true` |  |
| opentelemetry-collector.config.exporters.opensearch.logs_index | string | `"otel"` |  |
| opentelemetry-collector.config.exporters.otlp.endpoint | string | `"{{ include \"otel-demo.name\" . }}-jaeger-collector:4317"` |  |
| opentelemetry-collector.config.exporters.otlp.tls.insecure | bool | `true` |  |
| opentelemetry-collector.config.exporters.otlphttp/prometheus.endpoint | string | `"http://{{ include \"otel-demo.name\" . }}-prometheus-server:9090/api/v1/otlp"` |  |
| opentelemetry-collector.config.exporters.otlphttp/prometheus.tls.insecure | bool | `true` |  |
| opentelemetry-collector.config.processors.resource.attributes[0].action | string | `"insert"` |  |
| opentelemetry-collector.config.processors.resource.attributes[0].from_attribute | string | `"k8s.pod.uid"` |  |
| opentelemetry-collector.config.processors.resource.attributes[0].key | string | `"service.instance.id"` |  |
| opentelemetry-collector.config.processors.transform.error_mode | string | `"ignore"` |  |
| opentelemetry-collector.config.processors.transform.trace_statements[0].context | string | `"span"` |  |
| opentelemetry-collector.config.processors.transform.trace_statements[0].statements[0] | string | `"replace_pattern(name, \"\\\\?.*\", \"\")"` |  |
| opentelemetry-collector.config.processors.transform.trace_statements[0].statements[1] | string | `"replace_match(name, \"GET /api/products/*\", \"GET /api/products/{productId}\")"` |  |
| opentelemetry-collector.config.receivers.httpcheck/frontendproxy.targets[0].endpoint | string | `"http://{{ include \"otel-demo.name\" . }}-frontendproxy:8080"` |  |
| opentelemetry-collector.config.receivers.otlp.protocols.http.cors.allowed_origins[0] | string | `"http://*"` |  |
| opentelemetry-collector.config.receivers.otlp.protocols.http.cors.allowed_origins[1] | string | `"https://*"` |  |
| opentelemetry-collector.config.receivers.redis.collection_interval | string | `"10s"` |  |
| opentelemetry-collector.config.receivers.redis.endpoint | string | `"valkey-cart:6379"` |  |
| opentelemetry-collector.config.service.pipelines.logs.exporters[0] | string | `"opensearch"` |  |
| opentelemetry-collector.config.service.pipelines.logs.exporters[1] | string | `"debug"` |  |
| opentelemetry-collector.config.service.pipelines.logs.processors[0] | string | `"memory_limiter"` |  |
| opentelemetry-collector.config.service.pipelines.logs.processors[1] | string | `"resource"` |  |
| opentelemetry-collector.config.service.pipelines.logs.processors[2] | string | `"batch"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.exporters[0] | string | `"otlphttp/prometheus"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.exporters[1] | string | `"debug"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.processors[0] | string | `"memory_limiter"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.processors[1] | string | `"resource"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.processors[2] | string | `"k8sattributes"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.processors[3] | string | `"batch"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.receivers[0] | string | `"httpcheck/frontendproxy"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.receivers[1] | string | `"redis"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.receivers[2] | string | `"otlp"` |  |
| opentelemetry-collector.config.service.pipelines.metrics.receivers[3] | string | `"spanmetrics"` |  |
| opentelemetry-collector.config.service.pipelines.traces.exporters[0] | string | `"otlp"` |  |
| opentelemetry-collector.config.service.pipelines.traces.exporters[1] | string | `"debug"` |  |
| opentelemetry-collector.config.service.pipelines.traces.exporters[2] | string | `"spanmetrics"` |  |
| opentelemetry-collector.config.service.pipelines.traces.processors[0] | string | `"memory_limiter"` |  |
| opentelemetry-collector.config.service.pipelines.traces.processors[1] | string | `"resource"` |  |
| opentelemetry-collector.config.service.pipelines.traces.processors[2] | string | `"transform"` |  |
| opentelemetry-collector.config.service.pipelines.traces.processors[3] | string | `"batch"` |  |
| opentelemetry-collector.enabled | bool | `true` |  |
| opentelemetry-collector.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/open-telemetry/opentelemetry-collector-contrib"` |  |
| opentelemetry-collector.image.tag | string | `"0.117.0-17-01-25"` |  |
| opentelemetry-collector.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| opentelemetry-collector.mode | string | `"daemonset"` |  |
| opentelemetry-collector.podAnnotations."prometheus.io/port" | string | `"9464"` |  |
| opentelemetry-collector.podAnnotations."prometheus.io/scrape" | string | `"true"` |  |
| opentelemetry-collector.podAnnotations.opentelemetry_community_demo | string | `"true"` |  |
| opentelemetry-collector.ports.metrics.enabled | bool | `true` |  |
| opentelemetry-collector.ports.prometheus.containerPort | int | `9464` |  |
| opentelemetry-collector.ports.prometheus.enabled | bool | `true` |  |
| opentelemetry-collector.ports.prometheus.protocol | string | `"TCP"` |  |
| opentelemetry-collector.ports.prometheus.servicePort | int | `9464` |  |
| opentelemetry-collector.presets.hostMetrics.enabled | bool | `true` |  |
| opentelemetry-collector.presets.kubeletMetrics.enabled | bool | `true` |  |
| opentelemetry-collector.presets.kubernetesAttributes.enabled | bool | `true` |  |
| opentelemetry-collector.presets.logsCollection.enabled | bool | `true` |  |
| opentelemetry-collector.presets.logsCollection.includeCollectorLogs | bool | `false` |  |
| opentelemetry-collector.presets.logsCollection.storeCheckpoints | bool | `true` |  |
| opentelemetry-collector.resources.limits.memory | string | `"200Mi"` |  |
| opentelemetry-collector.securityContext.allowPrivilegeEscalation | bool | `true` |  |
| opentelemetry-collector.securityContext.privileged | bool | `true` |  |
| opentelemetry-collector.securityContext.runAsGroup | int | `0` |  |
| opentelemetry-collector.securityContext.runAsUser | int | `0` |  |
| opentelemetry-collector.service.type | string | `"ClusterIP"` |  |
| prometheus.alertmanager.enabled | bool | `true` |  |
| prometheus.alertmanager.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/prometheus/alertmanager"` |  |
| prometheus.alertmanager.image.tag | string | `"main"` |  |
| prometheus.alertmanager.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| prometheus.alertmanager.service.type | string | `"NodePort"` |  |
| prometheus.configmapReload.prometheus.enabled | bool | `true` |  |
| prometheus.configmapReload.prometheus.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/prometheus-operator_prometheus-config-reloader"` |  |
| prometheus.configmapReload.prometheus.image.tag | string | `"main-20-01-25"` |  |
| prometheus.enabled | bool | `true` |  |
| prometheus.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| prometheus.kube-state-metrics.enabled | bool | `true` |  |
| prometheus.kube-state-metrics.image.registry | string | `"code-caiser.caiser.ornlkdi.org:5050"` |  |
| prometheus.kube-state-metrics.image.repository | string | `"inl001/coreii-data-lake/kube-state-metrics"` |  |
| prometheus.kube-state-metrics.image.tag | string | `"v2.14.0-20-01-25"` |  |
| prometheus.kube-state-metrics.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| prometheus.prometheus-node-exporter.enabled | bool | `true` |  |
| prometheus.prometheus-node-exporter.image.registry | string | `"code-caiser.caiser.ornlkdi.org:5050"` |  |
| prometheus.prometheus-node-exporter.image.repository | string | `"inl001/coreii-data-lake/prometheus_node-exporter"` |  |
| prometheus.prometheus-node-exporter.image.tag | string | `"1.8.2"` |  |
| prometheus.prometheus-node-exporter.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| prometheus.prometheus-pushgateway.enabled | bool | `true` |  |
| prometheus.prometheus-pushgateway.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/prometheus/pushgateway"` |  |
| prometheus.prometheus-pushgateway.image.tag | string | `"master"` |  |
| prometheus.prometheus-pushgateway.imagePullSecrets[0].name | string | `"gitlab-image-creds"` |  |
| prometheus.server.extraFlags[0] | string | `"enable-feature=exemplar-storage"` |  |
| prometheus.server.extraFlags[1] | string | `"enable-feature=otlp-write-receiver"` |  |
| prometheus.server.global.evaluation_interval | string | `"30s"` |  |
| prometheus.server.global.scrape_interval | string | `"5s"` |  |
| prometheus.server.global.scrape_timeout | string | `"3s"` |  |
| prometheus.server.image.repository | string | `"code-caiser.caiser.ornlkdi.org:5050/inl001/coreii-data-lake/prometheus"` |  |
| prometheus.server.image.tag | string | `"main-20-01-25"` |  |
| prometheus.server.persistentVolume.enabled | bool | `true` |  |
| prometheus.server.persistentVolume.size | string | `"15Gi"` |  |
| prometheus.server.service.servicePort | int | `9090` |  |
| prometheus.server.service.type | string | `"NodePort"` |  |
| prometheus.server.tsdb.out_of_order_time_window | string | `"30m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].name | string | `"postgresql-alerts"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].alert | string | `"PostgresqlHighRateDeadlock"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].annotations.description | string | `"Postgres detected deadlocks\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].annotations.summary | string | `"Postgresql high rate deadlock (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].expr | string | `"increase(postgresql_errors_total{type=\"deadlock_detected\"}[1m]) > 1"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].for | string | `"0m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[0].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].alert | string | `"PostgresqlNotEnoughConnections"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].annotations.description | string | `"PostgreSQL instance should have more connections (> 5)\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].annotations.summary | string | `"Postgresql not enough connections (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].expr | string | `"sum by (datname) (pg_stat_activity_count{datname!~\"template.*|postgres\"}) < 5"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[1].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].alert | string | `"PostgresqlTooManyConnections"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].annotations.description | string | `"PostgreSQL instance has too many connections (> 80%).\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].annotations.summary | string | `"Postgresql too many connections (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].expr | string | `"sum by (instance, job, server) (pg_stat_activity_count) > min by (instance, job, server) (pg_settings_max_connections * 0.8)"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[2].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].alert | string | `"PostgresqlExporterError"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].annotations.description | string | `"Postgresql exporter is showing errors. A query may be buggy in query.yaml\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].annotations.summary | string | `"Postgresql exporter error (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].expr | string | `"pg_exporter_last_scrape_error > 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].for | string | `"0m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[3].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].alert | string | `"PostgresqlDown"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].annotations.description | string | `"Postgresql instance is down\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].annotations.summary | string | `"Postgresql down (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].expr | string | `"pg_up == 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].for | string | `"0m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[0].rules[4].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].name | string | `"gpu_alerts"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].alert | string | `"HighTotalEnergyConsumption"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].annotations.description | string | `"Total energy consumption is above 1000 Joules for more than 5 minutes."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].annotations.summary | string | `"High Total Energy Consumption"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].expr | string | `"DCGM_FI_DEV_TOTAL_ENERGY_CONSUMPTION > 1000"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[0].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].alert | string | `"LowGpuClockSpeed"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].annotations.description | string | `"GPU clock speed is below 1000 MHz for more than 5 minutes."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].annotations.summary | string | `"Low GPU Clock Speed on {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].expr | string | `"avg by (instance, gpu) (DCGM_FI_DEV_SM_CLOCK) < 1000"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[1].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].alert | string | `"HighPowerUsage"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].annotations.description | string | `"Power usage is above 300 Watts for more than 5 minutes. {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].annotations.summary | string | `"High Power Usage 0n {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].expr | string | `"avg by (instance, gpu) (DCGM_FI_DEV_POWER_USAGE) > 100"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[2].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].alert | string | `"HighGpuTemperature"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].annotations.description | string | `"GPU temperature exceeded 80°C on instance {{ $labels.instance }}, GPU {{ $labels.gpu }}."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].annotations.summary | string | `"High GPU Temperature on {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].expr | string | `"avg by (instance, gpu) (DCGM_FI_DEV_GPU_TEMP) > 80"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[3].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].alert | string | `"HighMemoryUsage"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].annotations.description | string | `"GPU memory exceeded 90% on instance {{ $labels.instance }}, GPU {{ $labels.gpu }}."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].annotations.summary | string | `"High GPU Memory Usage on {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].expr | string | `"avg by (instance, gpu) (DCGM_FI_DEV_MEM_COPY_UTIL) > 90"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[4].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].alert | string | `"HighGpuUtilization"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].annotations.description | string | `"GPU utilization is above 90% for more than 5 minutes.  {{ $labels.instance }}, GPU {{ $labels.gpu }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].annotations.summary | string | `"High GPU Utilization on  {{ $labels.instance }} (GPU {{ $labels.gpu }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].expr | string | `"avg by (instance, gpu) (DCGM_FI_DEV_GPU_UTIL) > 90"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[1].rules[5].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].name | string | `"velero-alerts"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[0].alert | string | `"VeleroBackupFailures"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[0].annotations.message | string | `"Velero backup {{ $labels.schedule }} has {{ $value | humanizePercentage }} failed backups."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[0].expr | string | `"velero_backup_failure_total / velero_backup_attempt_total > 0.50"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[0].for | string | `"15m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[0].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[1].alert | string | `"VeleroBackupPartialFailures"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[1].annotations.message | string | `"Velero backup {{ $labels.schedule }} has {{ $value | humanizePercentage }} partialy failed backups."` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[1].expr | string | `"velero_backup_partial_failure_total / velero_backup_attempt_total > 0.50"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[1].for | string | `"15m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[2].rules[1].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].name | string | `"minio-alerts"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].alert | string | `"NodesOffline"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].annotations.description | string | `"Node(s) in cluster {{ $labels.instance }} offline for more than 5 minutes"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].annotations.summary | string | `"Node down in MinIO deployment"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].expr | string | `"minio_cluster_nodes_offline_total > 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].for | string | `"10m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[0].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].alert | string | `"DisksOffline"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].annotations.description | string | `"Disks(s) in cluster {{ $labels.instance }} offline for more than 5 minutes"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].annotations.summary | string | `"Disks down in MinIO deployment"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].expr | string | `"minio_cluster_drive_offline_total > 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].for | string | `"10m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[3].rules[1].labels.severity | string | `"warn"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].name | string | `"Kubernetes"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].alert | string | `"ContainerHighCpuUtilization"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].annotations.description | string | `"Container CPU utilization is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].annotations.summary | string | `"Container High CPU utilization (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].expr | string | `"(sum(rate(container_cpu_usage_seconds_total{container!=\"\"}[5m])) by (pod, container) / sum(container_spec_cpu_quota{container!=\"\"}/container_spec_cpu_period{container!=\"\"}) by (pod, container) * 100) > 80"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[0].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].alert | string | `"KubernetesVolumeFullInFourDays"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].annotations.description | string | `"Volume under {{ $labels.namespace }}/{{ $labels.persistentvolumeclaim }} is expected to fill up within four days. Currently {{ $value | humanize }}% is available.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].annotations.summary | string | `"Kubernetes Volume full in four days (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].expr | string | `"predict_linear(kubelet_volume_stats_available_bytes[6h:5m], 4 * 24 * 3600) < 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].for | string | `"0m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[10].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].alert | string | `"KubernetesPodCrashLooping"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].annotations.description | string | `"Pod {{ $labels.namespace }}/{{ $labels.pod }} is crash looping\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].annotations.summary | string | `"Kubernetes pod crash looping (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].expr | string | `"increase(kube_pod_container_status_restarts_total[1m]) > 3"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[11].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].alert | string | `"ContainerHighMemoryUsage"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].annotations.description | string | `"Container Memory usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].annotations.summary | string | `"Container High Memory usage (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].expr | string | `"(sum(container_memory_working_set_bytes{name!=\"\"}) BY (instance, name) / sum(container_spec_memory_limit_bytes > 0) BY (instance, name) * 100) > 80"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[12].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].alert | string | `"HostHighCpuLoad"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].annotations.description | string | `"CPU load is > 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].annotations.summary | string | `"Host high CPU load (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].expr | string | `"(sum by (instance) (avg by (mode, instance) (rate(node_cpu_seconds_total{mode!=\"idle\"}[2m]))) > 0.8) * on(instance) group_left (nodename) node_uname_info{nodename=~\".+\"}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].for | string | `"10m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[13].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].alert | string | `"HighHostMemoryUsage"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].annotations.description | string | `"Host memory usage is above 80% for more than 5 minutes. VALUE = {{ $value }} HOST = {{ $labels.instance }}\n"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].annotations.summary | string | `"High memory usage on host"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].expr | string | `"(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes > 0.8"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].for | string | `"5m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[14].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].alert | string | `"ContainerHighMemoryUsage"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].annotations.description | string | `"Container Memory usage is above 80%\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].annotations.summary | string | `"Container High Memory usage (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].expr | string | `"(sum(container_memory_working_set_bytes{container!=\"\"}) BY (instance, container) / sum(container_spec_memory_limit_bytes > 0) BY (instance, container) * 100) > 80"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[1].labels.severity | string | `"warning"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].alert | string | `"KubernetesPodNotHealthy"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].annotations.description | string | `"Pod {{ $labels.namespace }}/{{ $labels.pod }} has been in a non-running state for longer than 15 minutes.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].annotations.summary | string | `"Kubernetes Pod not healthy (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].expr | string | `"sum by (namespace, pod) (kube_pod_status_phase{phase=~\"Pending|Unknown|Failed\"}) > 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].for | string | `"15m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[2].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].alert | string | `"KubernetesNodeMemoryPressure"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].annotations.description | string | `"Node {{ $labels.node }} has MemoryPressure condition\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].annotations.summary | string | `"Kubernetes Node memory pressure (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].expr | string | `"kube_node_status_condition{condition=\"MemoryPressure\",status=\"true\"} == 1"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[3].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].alert | string | `"KubernetesNodeNotReady"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].annotations.description | string | `"Node {{ $labels.node }} has been unready for a long time\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].annotations.summary | string | `"Kubernetes Node not ready (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].expr | string | `"kube_node_status_condition{condition=\"Ready\",status=\"true\"} == 0"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].for | string | `"10m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[4].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].alert | string | `"KubernetesNodeDiskPressure"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].annotations.description | string | `"Node {{ $labels.node }} has DiskPressure condition\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].annotations.summary | string | `"Kubernetes Node disk pressure (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].expr | string | `"kube_node_status_condition{condition=\"DiskPressure\",status=\"true\"} == 1"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[5].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].alert | string | `"KubernetesNodeOutOfPodCapacity"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].annotations.description | string | `"Node {{ $labels.node }} is out of pod capacity\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].annotations.summary | string | `"Kubernetes Node out of pod capacity (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].expr | string | `"sum by (node) ((kube_pod_status_phase{phase=\"Running\"} == 1) + on(uid) group_left(node) (0 * kube_pod_info{pod_template_hash=\"\"})) / sum by (node) (kube_node_status_allocatable{resource=\"pods\"}) * 100 > 90"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[6].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].alert | string | `"KubernetesContainerOomKiller"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].annotations.description | string | `"Container {{ $labels.container }} in pod {{ $labels.namespace }}/{{ $labels.pod }} has been OOMKilled {{ $value }} times in the last 10 minutes.\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].annotations.summary | string | `"Kubernetes Container oom killer (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].expr | string | `"(kube_pod_container_status_restarts_total - kube_pod_container_status_restarts_total offset 10m >= 1) and ignoring (reason) min_over_time(kube_pod_container_status_last_terminated_reason{reason=\"OOMKilled\"}[10m]) == 1"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].for | string | `"0m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[7].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].alert | string | `"KubernetesPersistentvolumeclaimPending"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].annotations.description | string | `"PersistentVolumeClaim {{ $labels.namespace }}/{{ $labels.persistentvolumeclaim }} is pending\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].annotations.summary | string | `"Kubernetes PersistentVolumeClaim pending (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].expr | string | `"kube_persistentvolumeclaim_status_phase{phase=\"Pending\"} == 1"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[8].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].alert | string | `"KubernetesVolumeOutOfDiskSpace"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].annotations.description | string | `"Volume is almost full (< 10% left)\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].annotations.summary | string | `"Kubernetes Volume out of disk space (instance {{ $labels.instance }})"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].expr | string | `"kubelet_volume_stats_available_bytes / kubelet_volume_stats_capacity_bytes * 100 < 10"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].for | string | `"2m"` |  |
| prometheus.serverFiles."alerting_rules.yml".groups[4].rules[9].labels.severity | string | `"critical"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[0].job_name | string | `"DCGM-Exporter"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[0].metrics_path | string | `"/metrics"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[0].static_configs[0].targets[0] | string | `"dcgm-exporter.monitoring.svc:9400"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].job_name | string | `"kubernetes-service-endpoints-slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].kubernetes_sd_configs[0].role | string | `"endpoints"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_scrape_slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[1].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[1].regex | string | `"(https?)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[1].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_scheme"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[1].target_label | string | `"__scheme__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[2].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[2].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_path"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[2].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].regex | string | `"(.+?)(?::\\d+)?;(\\d+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].replacement | string | `"$1:$2"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].source_labels[0] | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].source_labels[1] | string | `"__meta_kubernetes_service_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[3].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[4].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[4].regex | string | `"__meta_kubernetes_service_annotation_prometheus_io_param_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[4].replacement | string | `"__param_$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[5].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[5].regex | string | `"__meta_kubernetes_service_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[6].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[6].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[6].target_label | string | `"namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[7].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[7].source_labels[0] | string | `"__meta_kubernetes_service_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[7].target_label | string | `"service"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[8].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[8].source_labels[0] | string | `"__meta_kubernetes_pod_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].relabel_configs[8].target_label | string | `"node"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].scrape_interval | string | `"5m"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[10].scrape_timeout | string | `"30s"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].job_name | string | `"prometheus-pushgateway"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].kubernetes_sd_configs[0].role | string | `"service"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].relabel_configs[0].regex | string | `"pushgateway"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[11].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_probe"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].job_name | string | `"kubernetes-services"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].kubernetes_sd_configs[0].role | string | `"service"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].metrics_path | string | `"/probe"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].params.module[0] | string | `"http_2xx"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_probe"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[1].source_labels[0] | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[1].target_label | string | `"__param_target"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[2].replacement | string | `"blackbox"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[2].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[3].source_labels[0] | string | `"__param_target"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[3].target_label | string | `"instance"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[4].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[4].regex | string | `"__meta_kubernetes_service_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[5].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[5].target_label | string | `"namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[6].source_labels[0] | string | `"__meta_kubernetes_service_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[12].relabel_configs[6].target_label | string | `"service"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].job_name | string | `"kubernetes-pods"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].kubernetes_sd_configs[0].role | string | `"pod"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_scrape"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[10].action | string | `"drop"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[10].regex | string | `"Pending|Succeeded|Failed|Completed"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[10].source_labels[0] | string | `"__meta_kubernetes_pod_phase"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[11].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[11].source_labels[0] | string | `"__meta_kubernetes_pod_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[11].target_label | string | `"node"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[1].action | string | `"drop"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[1].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[1].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_scrape_slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[2].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[2].regex | string | `"(https?)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_scheme"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[2].target_label | string | `"__scheme__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[3].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[3].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[3].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_path"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[3].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].regex | string | `"(\\d+);(([A-Fa-f0-9]{1,4}::?){1,7}[A-Fa-f0-9]{1,4})"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].replacement | string | `"[$2]:$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].source_labels[1] | string | `"__meta_kubernetes_pod_ip"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[4].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].regex | string | `"(\\d+);((([0-9]+?)(\\.|$)){4})"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].replacement | string | `"$2:$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].source_labels[1] | string | `"__meta_kubernetes_pod_ip"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[5].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[6].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[6].regex | string | `"__meta_kubernetes_pod_annotation_prometheus_io_param_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[6].replacement | string | `"__param_$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[7].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[7].regex | string | `"__meta_kubernetes_pod_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[8].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[8].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[8].target_label | string | `"namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[9].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[9].source_labels[0] | string | `"__meta_kubernetes_pod_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[13].relabel_configs[9].target_label | string | `"pod"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].job_name | string | `"kubernetes-pods-slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].kubernetes_sd_configs[0].role | string | `"pod"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_scrape_slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[10].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[10].source_labels[0] | string | `"__meta_kubernetes_pod_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[10].target_label | string | `"node"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[1].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[1].regex | string | `"(https?)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[1].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_scheme"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[1].target_label | string | `"__scheme__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[2].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[2].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_path"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[2].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].regex | string | `"(\\d+);(([A-Fa-f0-9]{1,4}::?){1,7}[A-Fa-f0-9]{1,4})"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].replacement | string | `"[$2]:$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].source_labels[1] | string | `"__meta_kubernetes_pod_ip"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[3].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].regex | string | `"(\\d+);((([0-9]+?)(\\.|$)){4})"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].replacement | string | `"$2:$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].source_labels[1] | string | `"__meta_kubernetes_pod_ip"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[4].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[5].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[5].regex | string | `"__meta_kubernetes_pod_annotation_prometheus_io_param_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[5].replacement | string | `"__param_$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[6].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[6].regex | string | `"__meta_kubernetes_pod_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[7].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[7].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[7].target_label | string | `"namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[8].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[8].source_labels[0] | string | `"__meta_kubernetes_pod_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[8].target_label | string | `"pod"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[9].action | string | `"drop"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[9].regex | string | `"Pending|Succeeded|Failed|Completed"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].relabel_configs[9].source_labels[0] | string | `"__meta_kubernetes_pod_phase"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].scrape_interval | string | `"5m"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[14].scrape_timeout | string | `"30s"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[1].job_name | string | `"postgresql"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[1].metrics_path | string | `"/metrics"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[1].static_configs[0].targets[0] | string | `"prometheus-postgres-exporter.monitoring.svc:80"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[2].job_name | string | `"velero"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[2].metrics_path | string | `"/metrics"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[2].static_configs[0].targets[0] | string | `"velero.velero.svc:8085"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[3].job_name | string | `"minio-job"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[3].metrics_path | string | `"/minio/v2/metrics/cluster"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[3].scheme | string | `"http"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[3].static_configs[0].targets[0] | string | `"myminio-console.minio.svc:9090"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].job_name | string | `"otel-collector"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].kubernetes_sd_configs[0].namespaces.own_namespace | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].kubernetes_sd_configs[0].role | string | `"pod"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[4].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_pod_annotation_opentelemetry_community_demo"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[5].job_name | string | `"prometheus"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[5].static_configs[0].targets[0] | string | `"localhost:9090"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].bearer_token_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/token"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].job_name | string | `"kubernetes-apiservers"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].kubernetes_sd_configs[0].role | string | `"endpoints"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].relabel_configs[0].regex | string | `"default;kubernetes;https"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].relabel_configs[0].source_labels[1] | string | `"__meta_kubernetes_service_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].relabel_configs[0].source_labels[2] | string | `"__meta_kubernetes_endpoint_port_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].scheme | string | `"https"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].tls_config.ca_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/ca.crt"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[6].tls_config.insecure_skip_verify | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].bearer_token_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/token"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].job_name | string | `"kubernetes-nodes"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].kubernetes_sd_configs[0].role | string | `"node"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[0].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[0].regex | string | `"__meta_kubernetes_node_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[1].replacement | string | `"kubernetes.default.svc:443"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[1].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[2].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[2].replacement | string | `"/api/v1/nodes/$1/proxy/metrics"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].relabel_configs[2].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].scheme | string | `"https"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].tls_config.ca_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/ca.crt"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[7].tls_config.insecure_skip_verify | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].bearer_token_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/token"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].job_name | string | `"kubernetes-nodes-cadvisor"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].kubernetes_sd_configs[0].role | string | `"node"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[0].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[0].regex | string | `"__meta_kubernetes_node_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[1].replacement | string | `"kubernetes.default.svc:443"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[1].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[2].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[2].replacement | string | `"/api/v1/nodes/$1/proxy/metrics/cadvisor"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].relabel_configs[2].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].scheme | string | `"https"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].tls_config.ca_file | string | `"/var/run/secrets/kubernetes.io/serviceaccount/ca.crt"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[8].tls_config.insecure_skip_verify | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].honor_labels | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].job_name | string | `"kubernetes-service-endpoints"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].kubernetes_sd_configs[0].role | string | `"endpoints"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[0].action | string | `"keep"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[0].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[0].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_scrape"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[1].action | string | `"drop"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[1].regex | bool | `true` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[1].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_scrape_slow"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[2].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[2].regex | string | `"(https?)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[2].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_scheme"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[2].target_label | string | `"__scheme__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[3].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[3].regex | string | `"(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[3].source_labels[0] | string | `"__meta_kubernetes_service_annotation_prometheus_io_path"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[3].target_label | string | `"__metrics_path__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].regex | string | `"(.+?)(?::\\d+)?;(\\d+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].replacement | string | `"$1:$2"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].source_labels[0] | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].source_labels[1] | string | `"__meta_kubernetes_service_annotation_prometheus_io_port"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[4].target_label | string | `"__address__"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[5].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[5].regex | string | `"__meta_kubernetes_service_annotation_prometheus_io_param_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[5].replacement | string | `"__param_$1"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[6].action | string | `"labelmap"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[6].regex | string | `"__meta_kubernetes_service_label_(.+)"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[7].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[7].source_labels[0] | string | `"__meta_kubernetes_namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[7].target_label | string | `"namespace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[8].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[8].source_labels[0] | string | `"__meta_kubernetes_service_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[8].target_label | string | `"service"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[9].action | string | `"replace"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[9].source_labels[0] | string | `"__meta_kubernetes_pod_node_name"` |  |
| prometheus.serverFiles."prometheus.yml".scrape_configs[9].relabel_configs[9].target_label | string | `"node"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `""` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
