# Jumpserver

[中文版](./README.md)

[Jumpserver](http://Jumpserver.org/) is the world's first fully open source bastion machine. It uses the GNU GPL v2.0 open source protocol and is a 4A professional operation and maintenance audit system.

## TL;DR;

```bash
# Testing configuration
$ helm install my-release ./jumpserver
```

## Introduction

This chart bootstraps a [Jumpserver](https://github.com/kelajin/jumpserver) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.12+
- Helm 2.11+ or Helm 3.0-beta3+
- PV provisioner support in the underlying infrastructure
- docker images of [wojiushixiaobai](https://github.com/wojiushixiaobai/docker-compose)

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install my-release ./jumpserver
```

The command deploys Jumpserver on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

The following table lists the configurable parameters of the Jumpserver chart and their default values.

### overview

| Parameter              | Description                    | Default |
| ---------------------- | ------------------------------ | ------- |
| `nameOveride`          | name override                  | `nil`   |
| `fullNameOveride`      | full name override             | `nil`   |
| `ingress.enabled`      | enable ingress of jumpserver   | `true`  |
| `jmsCore.enabled`      | enable core of jumpserver      | `true`  |
| `jmsGuacamole.enabled` | enable guacamole of jumpserver | `true`  |
| `jmsKoko.enabled`      | enable koko of jumpserver      | `true`  |
| `jmsLuna.enabled`      | enable luna of jumpserver      | `true`  |
| `mariadb.enabled`      | enable mariadb of jumpserver   | `false` |
| `redis.enabled`        | enable redis of jumpserver     | `false` |

### jmsCore.config

| Parameter        | Description                   | Default                |
| ---------------- | ----------------------------- | ---------------------- |
| `secretKey`      | secrete key of jumpserver     | `nil`                  |
| `bootstrapToken` | bootstrap token of jumpserver | `nil`                  |
| `debug`          | enable debug for jumpserver   | `false`                |
| `log.level`      | log level of jumpserver       | `INFO`                 |
| `log.dir`        | log dir of jumpserver         | `/opt/jumpserver/logs` |
| `db.engine`      | engine of db of jumpserver    | `mysql`                |
| `db.host`        | host of db                    | `nil`                  |
| `db.port`        | port of host                  | `3306`                 |
| `db.username`    | username of db                | `jumpserver`           |
| `db.password`    | password of db                | `nil`                  |
| `db.name`        | database name of db           | `nil`                  |
| `redis.host`     | host of redis                 | `nil`                  |
| `redis.port`     | port of redis                 | `6379`                 |
| `redis.password` | password of redis             | `nil`                  |

### jmsKoko.config

| Parameter             | Description                      | Default |
| --------------------- | -------------------------------- | ------- |
| `log.level`           | log level of koko                | `INFO`  |
| `lang`                | lang of koko web UI              | `zh`    |
| `sftp.root`           | sftp root path                   | `/tmp`  |
| `sftp.showHiddenFile` | enable show hidden file for sftp | `true`  |
| `reuseConnection`     | reuse sftp link                  | `true`  |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install my-release \
  --set ingress.enabled=true \
    ./jumpserver
```

The above command enables the Jumpserver server ingress.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install my-release -f values.yaml ./jumpserver
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Related projects

- https://github.com/jumpserver/jumpserver
- https://github.com/wojiushixiaobai/docker-compose