# WyriHaximus.net Helm charts

Opinionated helm chats for my personal projects, and OSS Projects that either don't have public helm charts, and don't meet my requirements for them.

## Charts in this repository

* [`docker-hub-exporter`](https://hub.helm.sh/charts/wyrihaximusnet/docker-hub-exporter)
* [`redirect`](https://hub.helm.sh/charts/wyrihaximusnet/redirect)


## Opinionated decisions shared by all charts

* All have pod anti-affinity to be not be on the same node
