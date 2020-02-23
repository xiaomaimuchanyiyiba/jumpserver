# Jumpserver

[English](./README-en.md)

[Jumpserver](http://Jumpserver.org/) 是全球首款完全开源的堡垒机, 使用 GNU GPL v2.0 开源协议, 是符合 4A 的专业运维审计系统。

## 使用方法

```bash
# Testing configuration
$ helm install my-release ./jumpserver
```

## 介绍

当前Chart包含了Jumpserver所需的基本组件

## 依赖

- Kubernetes 1.12+
- Helm 2.11+ 或 Helm 3.0-beta3+
- PV provisioner 支持
- [wojiushixiaobai](https://github.com/wojiushixiaobai/docker-compose)的镜像支持

## 安装

发布名为 `my-release` 的release:

```bash
$ helm install my-release ./jumpserver
```

上条命令把默认配置的Jumpserver部署到了kubernetes集群中，[参数](#parameters)一节中列出了配置参数

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

删除 `my-release` release:

```bash
$ helm delete my-release
```

上条命令删除了所有包含在release中的组件

## 参数

下面的表格中列出了一些必要的参数，发布前请先阅读并设置

### 总览

| 参数                   | 描述               | 默认值  |
| ---------------------- | ------------------ | ------- |
| `nameOveride`          | name override      | `nil`   |
| `fullNameOveride`      | full name override | `nil`   |
| `ingress.enabled`      | 开启 ingress       | `true`  |
| `jmsCore.enabled`      | 开启 core o        | `true`  |
| `jmsGuacamole.enabled` | 开启 guacamole     | `true`  |
| `jmsKoko.enabled`      | 开启 koko          | `true`  |
| `jmsLuna.enabled`      | 开启 luna          | `true`  |
| `mariadb.enabled`      | 开启 mariadb       | `false` |
| `redis.enabled`        | 开启 redis         | `false` |

### jmsCore.config

| 参数             | 描述                                                                    | 默认值                 |
| ---------------- | ----------------------------------------------------------------------- | ---------------------- |
| `secretKey`      | 加密秘钥 生产环境中请修改为随机字符串，请勿外泄, 可使用命令生成         | `nil`                  |
| `bootstrapToken` | 预共享Token coco和guacamole用来注册服务账号，不在使用原来的注册接受机制 | `nil`                  |
| `debug`          | 开启 debug 模式                                                         | `false`                |
| `log.level`      | 日志等级                                                                | `INFO`                 |
| `log.dir`        | 日志存放路径                                                            | `/opt/jumpserver/logs` |
| `db.engine`      | 数据库引擎                                                              | `mysql`                |
| `db.host`        | 数据库IP地址                                                            | `nil`                  |
| `db.port`        | 数据库端口                                                              | `3306`                 |
| `db.username`    | 数据库用户名                                                            | `jumpserver`           |
| `db.password`    | 数据库密码                                                              | `nil`                  |
| `db.name`        | 数据库名称                                                              | `nil`                  |
| `redis.host`     | redisIP地址                                                             | `nil`                  |
| `redis.port`     | redis端口                                                               | `6379`                 |
| `redis.password` | redis密码                                                               | `nil`                  |

### jmsKoko.config

| 参数                  | 描述                                                       | 默认值 |
| --------------------- | ---------------------------------------------------------- | ------ |
| `log.level`           | 日志等级                                                   | `INFO` |
| `lang`                | koko网页显示语言                                           | `zh`   |
| `sftp.root`           | sftp根路径                                                 | `/tmp` |
| `sftp.showHiddenFile` | sftp显示隐藏文件                                           | `true` |
| `reuseConnection`     | 复用和用户后端资产已建立的连接(用户不会复用其他用户的连接) | `true` |


在`helm install`时通过 `--set key=value[,key=value]` 指定参数. 举例,

```bash
$ helm install my-release \
  --set ingress.enabled=true \
    ./jumpserver
```

上条命令开启了ingress.

也可以通过 `-f file` 的形式指定一个或多个values.yaml文件. 举例,

```bash
$ helm install my-release -f values.yaml ./jumpserver
```

> **注**: 默认使用 [values.yaml](values.yaml)

## 存在问题与改进方向

- [ ] HA支持，由于koko和guacamole注册机制导致无法实现HA，考虑通过构建自定义镜像或修改源码实现
- [ ] 自动增删Pod节点并支持指定容器，考虑通过sidecar实现

## 相关项目

- https://github.com/jumpserver/jumpserver
- https://github.com/wojiushixiaobai/docker-compose