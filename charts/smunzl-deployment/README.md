# smunzl-deployment

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) 

A Chart for deploying services and apps inside the smunzl cluster

## Install smunzl-deployment chart

### Prerequisites

Before installing this chart you need to make sure that

- [istio](https://istio.io/) has already been installed on the k8s cluster.
- a namespace where the service shall be installed into has already been created on the K8S cluster.

## Chart Configuration Parameters

The following table lists the configurable parameters of the chart and its default values.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| deployment.configmap.enabled | bool | `true` |  |
| deployment.configmap.values | object | `{}` | Values for configmap. The values will be passed as container envs, exactly matching the key names. |
| deployment.env | list | `[]` | Additional [kubernetes container envs](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/) |
| deployment.image | string | `"ghcr.io/knallbumm/sz-app-landingpage:0.5.2"` | Docker image uri |
| deployment.imagePullSecrets | object | `{}` | Image pull secrets, useful when interacting with private registy |
| deployment.port | int | `3000` | Container-port to expose per Service |
| deployment.replicas | int | `1` | Amount of pod replicas |
| gateway.enabled | bool | `true` |  |
| gateway.hosts | list | `[]` | List of usable hosts |
| gateway.name | string | `""` | Name of Gateway Resource. Defaults to: {{ .Release.Name }}-gateway |
| gateway.tls.enabled | bool | `true` | Whether to create and apply a TLS-Certificate |
| gateway.tls.httpsRedirect | bool | `true` | Whether to redirect all traffic from http to https |
| gateway.tls.issuerRef | object | `{"kind":"ClusterIssuer","name":"letsencrypt-staging"}` | Certificate Resource spec.issuerRef |
| routing.additionalHttp | list | `[]` | Additional matchers/routes, see [istio request routing](https://istio.io/latest/docs/tasks/traffic-management/request-routing/) |
| routing.deploymentMatch | list | `[{"uri":{"prefix":"/"}}]` | Matcher helper for deployment, see [istio request routing](https://istio.io/latest/docs/tasks/traffic-management/request-routing/) |
| routing.enabled | bool | `true` |  |
| routing.gateways | list | `[]` | Gateways for the VirtualService. Will always include this charts' Gateway, if used. |
| routing.hosts | list | `["landing.int.smunzl.art"]` | Hosts, the VirtualService should listen too |