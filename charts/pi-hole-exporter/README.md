# Pi-Hole Exporter

<p align="center">
  <img src="https://helm.wyrihaximus.net/images/charts/pi-hole-exporter.png">
</p>

Opinionated helm chart for [`eko/pihole-exporter`](https://github.com/eko/pihole-exporter). There is an alternative 
available at [`SiM22/pihole-exporter-helm-chart`](https://github.com/SiM22/pihole-exporter-helm-chart) but that didn't 
meet my requirements.

## Configuration

By default, this chart will look for a secret name `pi-hole` in the same namespace for additional env vars to add to the 
container. It is required that it contains the location of your [`PiHole`](https://pi-hole.net/) and a away to authenticate against it. Those 
can be find [here](https://github.com/eko/pihole-exporter#using-docker). You can find an example secret file in 
[`library-ci/secret.yaml`](https://github.com/WyriHaximusNet/helm-charts/blob/master/charts/pi-hole-exporter/library-ci/secret.yaml).

## Opinionated decisions

* Port is hardcoded to `9617` for the metrics.
* Metrics collection from Pi-Hole happens every 30 seconds.
* Requires you to configure a secret in the same namespace as you deploy this chart to container additional env vars.
