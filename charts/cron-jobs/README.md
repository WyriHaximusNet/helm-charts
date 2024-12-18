# Cron Jobs

<p align="center">
  <img src="https://helm.wyrihaximus.net/images/charts/cron-jobs.png">
</p>

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: library](https://img.shields.io/badge/Type-library-informational?style=flat-square)

Opinionated helm library chart for easy creation of cron jobs.

# Example

Very basic example without any customization:

```gotemplate
{{- range $job := .Values.jobs }}
{{- include "cron-jobs.cronjob" $job -}}
{{- end }}
```

The following values will run a cronjob that sleeps for 1 second any minute

```yaml
jobs:
  - name: sleep
    schedule: "* * * * *"
    labels:
      cronjob:
        key: value
      jobTemplate:
        key: value
    container:
      command: ["sleep"]
      args: ["1"]
      resources:
        limits:
          cpu: 1m
          memory: 12Mi
        requests:
          cpu: 1m
          memory: 12Mi
    image:
      repository: alpine
      tag: 3.12
      pullPolicy: IfNotPresent
```

## Opinionated decisions

* A history of `3` failed and `3` successful jobs are kept around for log checking.
* No restarts
* No concurrently
* A single container per cron job
* `cron` and `name` labels are set on each cron job with the name you give it

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| WyriHaximus | <helm@wyrihaximus.net> | <https://wyrihaximus.net> |

## Requirements

Kubernetes: `>= 1.21`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| jobs | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)
