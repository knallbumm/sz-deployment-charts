# smunzl-deployment

![Version: 0.10.0](https://img.shields.io/badge/Version-0.10.0-informational?style=flat-square)

A Chart for deploying services and apps inside the smunzl cluster

## Install smunzl-deployment chart

### Prerequisites

Before installing this chart you need to make sure that

- [istio](https://istio.io/) is installed.
- a namespace for the service is present.

## Chart Configuration Parameters

The following table lists the configurable parameters of the chart and its default values (generated with [helm-docs](https://github.com/norwoodj/helm-docs)).

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| deployment.autoscaling.enabled | bool | `false` |  |
| deployment.autoscaling.maxReplicas | int | `2` |  |
| deployment.autoscaling.metrics.additionalMetrics | object | `{}` | raw HorizontalPodAutoscaler metrics |
| deployment.autoscaling.metrics.averageUtilizationCpu | string | `""` | average cpu utilization, see [kubernetes hpa docs](https://kubernetes.io/de/docs/tasks/run-application/horizontal-pod-autoscale/#details-zum-algorithmus) |
| deployment.autoscaling.minReplicas | int | `1` |  |
| deployment.configmap.enabled | bool | `false` |  |
| deployment.configmap.values | object | `{}` | Values for configmap. The values will be passed as container envs, exactly matching the key names. |
| deployment.enabled | bool | `true` | whether to create deployment, service, ... |
| deployment.env | list | `[]` | Additional [kubernetes container envs](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/) |
| deployment.image | string | `"nginxinc/nginx-unprivileged"` | Docker image uri |
| deployment.port | int | `8080` | Container-port to expose per Service |
| deployment.replicas | int | `1` | Deployment Replicas |
| deployment.resources.requests | object | `{"cpu":"0","memory":"0"}` | See [kubernetes requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-requests-and-limits-of-pod-and-container) |
| deployment.template.metadata | object | `{"annotations":{},"labels":{}}` | template metadata |
| deployment.template.spec | object | `{}` | template specs |
| deployment.volumeMounts | object | `{}` | Container volume mounts |
| gateway.enabled | bool | `false` |  |
| gateway.hosts | list | `[]` | List of usable hosts |
| gateway.name | string | `{{ .Release.Name }}-gateway` | Name of Gateway Resource |
| gateway.tls.credentialName | string | `{{ .Release.Name }}-tls` | the name of the TLS-Certificate secret |
| gateway.tls.enabled | bool | `false` | Whether to create and apply a TLS-Certificate |
| gateway.tls.httpsRedirect | bool | `false` | Whether to redirect all traffic from http to https |
| gateway.tls.issuerRef | object | `{"kind":"ClusterIssuer","name":"letsencrypt-staging"}` | Certificate Resource spec.issuerRef |
| routing.additionalHttp | list | `[]` | Additional HTTPRoutes, see [istio request routing](https://istio.io/latest/docs/tasks/traffic-management/request-routing/) |
| routing.deploymentRoute | object | `{"match":[{"uri":{"prefix":"/"}}]}` | HTTPRoute config for deployment, see [istio HTTPRoute](https://istio.io/latest/docs/reference/config/networking/virtual-service/#HTTPRoute) |
| routing.enabled | bool | `false` |  |
| routing.gateways | list | `[]` | Gateways for the VirtualService. Will always include this charts' Gateway, if used. |
| routing.hostRedirect | string, object | `{"redirectCode":301,"redirectFromHosts":[],"targetHost":"33-prozent.com"}` | configures which host to redirect to. |
| routing.hostRedirect.redirectCode | int | `301` | code to use on redirect |
| routing.hostRedirect.redirectFromHosts | list | `{{ .gateway.hosts }}` | hosts to redirect off of |
| routing.hostRedirect.targetHost | string | `"33-prozent.com"` | host to redirect to |
| routing.hosts | list | `["*"]` | Hosts, the VirtualService should listen too |
