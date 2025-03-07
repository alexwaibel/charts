# teslamate

![Version: 6.1.1](https://img.shields.io/badge/Version-6.1.1-informational?style=flat-square) ![AppVersion: v1.23.4](https://img.shields.io/badge/AppVersion-v1.23.4-informational?style=flat-square)

A self-hosted data logger for your Tesla 🚘

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/k8s-at-home/charts/issues/new/choose)**

## Source Code

* <https://github.com/adriankumpf/teslamate>

## Requirements

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | postgresql | 10.9.4 |
| https://library-charts.k8s-at-home.com | common | 4.0.1 |

## TL;DR

```console
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
helm install teslamate k8s-at-home/teslamate
```

## Installing the Chart

To install the chart with the release name `teslamate`

```console
helm install teslamate k8s-at-home/teslamate
```

## Uninstalling the Chart

To uninstall the `teslamate` deployment

```console
helm uninstall teslamate
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install teslamate \
  --set env.TZ="America/New York" \
    k8s-at-home/teslamate
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install teslamate k8s-at-home/teslamate -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. See [teslamate docs](https://docs.teslamate.org/docs/configuration/environment_variables) for more details. |
| env.DATABASE_HOST | string | `"{{ include \"common.names.fullname\" .}}-postgresql"` | Postgres database hostname |
| env.DATABASE_NAME | string | `"{{ .Values.postgresql.postgresqlDatabase }}"` | Postgres database password |
| env.DATABASE_PASS | string | `"{{ .Values.postgresql.postgresqlPassword }}"` | Postgres database password |
| env.DATABASE_USER | string | `"{{ .Values.postgresql.postgresqlUsername }}"` | Postgres database user name |
| env.DISABLE_MQTT | string | `"false"` | Disables the MQTT feature if `true` |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"teslamate/teslamate"` | image repository |
| image.tag | string | `"1.23.4"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| postgresql | object | See values.yaml | Enable and configure postgresql database subchart under this key.    For more options see [postgresql chart documentation](https://github.com/bitnami/charts/tree/master/bitnami/postgresql) |
| service | object | See values.yaml | Configures service settings for the chart. |

## Changelog

All notable changes to this application Helm chart will be documented in this file but does not include changes from our common library. To read those click [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common#changelog).

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### [6.0.0]

#### Changed

- Upgraded the common library dependency to version 4.0.0. This introduced (potentially) breaking changes to `initContainers` and `additionalContainers`. Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-4.0.0/charts/stable/common/) for the up-to-date values.

### [5.0.0]

#### Changed

- **BREAKING**: Upgraded the common library dependency to version 3.2.0. This introduces several breaking changes (`service`, `ingress` and `persistence` keys have been refactored).
  Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-3.2.0/charts/stable/common/) for the up-to-date values.
- Changed image tag to `1.23.4`.
- Provide dynamic default values for database environment vars.
- Provide sane default values for postgresql chart.

### [4.0.0]

#### Changed

- **BREAKING** Migrate to the common library, a lot of configuration has changed.

#### Removed

- test-connection

### [3.6.1]

#### Changed

- use helm-docs

[6.0.0]: #600
[5.0.0]: #500
[4.0.0]: #400
[3.6.1]: #361

## Support

- See the [Docs](https://docs.k8s-at-home.com/our-helm-charts/getting-started/)
- Open an [issue](https://github.com/k8s-at-home/charts/issues/new/choose)
- Ask a [question](https://github.com/k8s-at-home/organization/discussions)
- Join our [Discord](https://discord.gg/sTMX7Vh) community

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)
