# qbittorrent

![Version: 13.0.1](https://img.shields.io/badge/Version-13.0.1-informational?style=flat-square) ![AppVersion: v4.3.7](https://img.shields.io/badge/AppVersion-v4.3.7-informational?style=flat-square)

qBittorrent is a cross-platform free and open-source BitTorrent client

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/k8s-at-home/charts/issues/new/choose)**

## Source Code

* <https://github.com/qbittorrent/qBittorrent>
* <https://github.com/k8s-at-home/container-images>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://library-charts.k8s-at-home.com | common | 4.0.1 |

## TL;DR

```console
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
helm install qbittorrent k8s-at-home/qbittorrent
```

## Installing the Chart

To install the chart with the release name `qbittorrent`

```console
helm install qbittorrent k8s-at-home/qbittorrent
```

## Uninstalling the Chart

To uninstall the `qbittorrent` deployment

```console
helm uninstall qbittorrent
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install qbittorrent \
  --set env.TZ="America/New York" \
    k8s-at-home/qbittorrent
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install qbittorrent k8s-at-home/qbittorrent -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. See [image docs](https://docs.k8s-at-home.com/our-container-images/configuration/) for more details. |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"ghcr.io/k8s-at-home/qbittorrent"` | image repository |
| image.tag | string | `"v4.3.7"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| metrics.enabled | bool | See values.yaml | Enable and configure prometheus-qbittorrent-exporter sidecar and Prometheus podMonitor. |
| metrics.exporter.env.logLevel | string | `"INFO"` | log level [DEBUG|INFO|WARNING|ERROR|CRITICAL] |
| metrics.exporter.env.password | string | `"adminadmin"` | qbittorrent password update value after configuring qbittorrent |
| metrics.exporter.env.port | int | `9022` | metrics port |
| metrics.exporter.env.user | string | `"admin"` | qbittorrent username update value after configuring qbittorrent |
| metrics.exporter.image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| metrics.exporter.image.repository | string | `"esanchezm/prometheus-qbittorrent-exporter"` | image repository |
| metrics.exporter.image.tag | string | `"v1.2.0"` | image tag |
| metrics.prometheusRule | object | See values.yaml | Enable and configure Prometheus Rules for the chart under this key. |
| metrics.prometheusRule.rules | list | See prometheusrules.yaml | Configure additionial rules for the chart under this key. |
| metrics.serviceMonitor.interval | string | `"15s"` |  |
| metrics.serviceMonitor.labels | object | `{}` |  |
| metrics.serviceMonitor.scrapeTimeout | string | `"5s"` |  |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service | object | See values.yaml | Configures service settings for the chart. |
| settings.automaticPortSetup | bool | `false` | Enables automatic port configuration at startup This sets the qbittorrent port to the value of `service.bittorrent.ports.bittorrent.port`. |

## Changelog

All notable changes to this application Helm chart will be documented in this file but does not include changes from our common library. To read those click [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common#changelog).

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### [13.0.0]

#### Changed

- **BREAKING**: Refactored Prometheus metrics section to add rules. Enabling metrics automatically enables the serviceMonitor.

### [12.2.0]

#### Changed

- Switched to serviceMonitor instead of podMonitor. This would revert scrape intervals and timeouts if changed from default.

### [12.1.0]

#### Added

- Added podMonitor and the ability to use [prometheus-qbittorrent-exporter](https://github.com/esanchezm/prometheus-qbittorrent-exporter) as a sidecar container.

### [12.0.0]

#### Changed

- Upgraded the common library dependency to version 4.0.0. This introduced (potentially) breaking changes to `initContainers` and `additionalContainers`. Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-4.0.0/charts/stable/common/) for the up-to-date values.

### [11.0.0]

#### Changed

- **BREAKING**: Upgraded the common library dependency to version 3.0.2. This introduces several breaking changes (`service`, `ingress` and `persistence` keys have been refactored).
  Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-3.0.2/charts/stable/common/) for the up-to-date values.
- Changed image tag to `v4.3.5`.
- Move automatic port management at startup to `settings.automaticPortSetup`.

### [10.0.0]

#### Changed

- **Breaking**: swap linuxserver.io images for k8s@home image

### [1.0.0]

#### Added

- Initial version

[13.0.0]: #1300
[12.2.0]: #1220
[12.1.0]: #1210
[12.0.0]: #1200
[11.0.0]: #1100
[10.0.0]: #1000
[1.0.0]: #100

## Support

- See the [Docs](https://docs.k8s-at-home.com/our-helm-charts/getting-started/)
- Open an [issue](https://github.com/k8s-at-home/charts/issues/new/choose)
- Ask a [question](https://github.com/k8s-at-home/organization/discussions)
- Join our [Discord](https://discord.gg/sTMX7Vh) community

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)
