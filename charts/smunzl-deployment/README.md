# smunzl-deployment

![Version: 0.7.7](https://img.shields.io/badge/Version-0.7.7-informational?style=flat-square) 

A Chart for deploying services and apps inside the smunzl cluster

## Install smunzl-deployment chart

### Prerequisites

Before installing this chart you need to make sure that

- [istio](https://istio.io/) is installed.
- a namespace for the service is present.

## Chart Configuration Parameters

The following table lists the configurable parameters of the chart and its default values.

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
| deployment.replicas | int | `1` | serviceAccount for pods to use |
| deployment.resources.requests | object | `{"cpu":"0","memory":"0"}` | See [kubernetes requests](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-requests-and-limits-of-pod-and-container) |
| deployment.template.metadata | object | `{"annotations":{},"labels":{}}` | template metadata |
| deployment.template.spec | object | `{}` | template specs |
| deployment.volumeMounts | object | `{}` | Container volume mounts |
| gateway.enabled | bool | `false` |  |
| gateway.hosts | list | `[]` | List of usable hosts |
| gateway.name | string | `""` | Name of Gateway Resource. Defaults to: {{ .Release.Name }}-gateway |
| gateway.tls.enabled | bool | `false` | Whether to create and apply a TLS-Certificate |
| gateway.tls.httpsRedirect | bool | `false` | Whether to redirect all traffic from http to https |
| gateway.tls.issuerRef | object | `{"kind":"ClusterIssuer","name":"letsencrypt-staging"}` | Certificate Resource spec.issuerRef |
| routing.additionalHttp | list | `[]` | Additional HTTPRoutes, see [istio request routing](https://istio.io/latest/docs/tasks/traffic-management/request-routing/) |
| routing.deploymentRoute | object | `{"match":[{"uri":{"prefix":"/"}}]}` | HTTPRoute config for deployment, see [istio HTTPRoute](https://istio.io/latest/docs/reference/config/networking/virtual-service/#HTTPRoute) |
| routing.enabled | bool | `false` |  |
| routing.gateways | list | `[]` | Gateways for the VirtualService. Will always include this charts' Gateway, if used. |
| routing.hosts | list | `["*"]` | Hosts, the VirtualService should listen too |