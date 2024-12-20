# Default Backend

<p align="center">
  <img src="https://helm.wyrihaximus.net/images/charts/default-backend.png">
</p>

![Version: 1.1.0](https://img.shields.io/badge/Version-1.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: random](https://img.shields.io/badge/AppVersion-random-informational?style=flat-square)

Opinionated helm chart for [`wyrihaximusnet/default-backend`](https://github.com/wyrihaximusnet/docker-default-backend).

## Provided tags

* `random` - Each time when the images are build a random image is selected and build, plus every hour an image is retagged as `random` and pushed.
* `images/*` - For each directory inside [`images/`](https://github.com/WyriHaximusNet/docker-default-backend/tree/master/images).

## Configuration

This chart has very little configuration, it runs without any. But it is recommended to set the number of replica's
(until autoscaling support has been added), and optionally configure ingress hosts. Listed below is my personal
configuration. Both [`k8s.wyrihaximus.net`](https://k8s.wyrihaximus.net/) and
[`default-backend.k8s.wyrihaximus.net`](https://default-backend.k8s.wyrihaximus.net/) are active, refresh the pages a
few times. This configuration example also enables the cronjob that replaces the oldest pod, and forces the latest,
hourly retagged, Docker image to be used. It also has the horizontal pod autoscaler enabled.

```yaml
replicas: 3

cron:
  replaceOldestPodHourly: true

hpa:
  enable: true

ingress:
  hosts:
    - k8s.wyrihaximus.net
    - default-backend.k8s.wyrihaximus.net
```

###

## Opinionated decisions

* requires kubernetes ^1.18
* Ports are hardcoded to `6969` for the service, and `9696` for the metrics.
* TLS is assumed to be required, and is set up based on supplied hosts in `ingress.hosts`.
* It's assumed that this helm chart will be run in it's own namespace, so the naming for all resources is kept as simple as possible.
* Prometheus export annotations are added for metric scraping.
* The default tag is random to randomly cycle through the different `404` pages.
* Comes with a pod
* Replace oldest pod every hour to hook into the hourly random image retagging

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| WyriHaximus | <helm@wyrihaximus.net> | <https://wyrihaximus.net> |

## Requirements

Kubernetes: `^1.23`

| Repository | Name | Version |
|------------|------|---------|
| https://helm.wyrihaximus.net/ | commons | ^0.1 |
| https://helm.wyrihaximus.net/ | cron-jobs | ^1 |
| https://helm.wyrihaximus.net/ | horizontal-pod-autoscalers | ^1 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| cron.replaceOldestPodHourly | bool | `false` |  |
| hpa.enable | bool | `false` |  |
| hpa.maxReplicas | int | `1024` |  |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"ghcr.io/wyrihaximusnet/default-backend"` |  |
| image.tag | string | `"random"` |  |
| ingress.annotations."kubernetes.io/ingress.class" | string | `"nginx"` |  |
| ingress.annotations."kubernetes.io/tls-acme" | string | `"true"` |  |
| ingress.hosts | list | `[]` |  |
| replicas | int | `2` |  |
| resources.limits.cpu | string | `"75m"` |  |
| resources.limits.memory | string | `"64Mi"` |  |
| resources.requests.cpu | string | `"75m"` |  |
| resources.requests.memory | string | `"64Mi"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
