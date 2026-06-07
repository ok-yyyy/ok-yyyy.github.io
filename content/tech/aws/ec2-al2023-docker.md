---
title: Amazon Linux 2023にDockerをインストール
tags:
  - AWS / EC2
  - Docker
---

## 概要

Amazon Linux 2023にDockerをインストールする手順をまとめます。

インスタンスタイプはt4g (linux/arm64) を想定。

## 手順

### 0. 前準備

パッケージの更新

```shell
sudo dnf update
```

### 1. Dockerインストール

```shell
sudo dnf install docker
sudo systemctl enable --now docker

docker --version
```

`docker`グループにユーザを追加 (ここでは`ec2-user`)

```shell
sudo usermod -aG docker ec2-user
```

### 2. Docker Composeインストール

最新バージョンは [リリースページ](https://github.com/docker/compose/releases) を参照

```shell
sudo mkdir -p /usr/local/lib/docker/cli-plugins

sudo curl -SL https://github.com/docker/compose/releases/download/v5.1.4/docker-compose-linux-aarch64 -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose

docker compose version
```

### 3. Docker Buildxインストール

Buildxを更新する

最新バージョンは [リリースページ](https://github.com/docker/buildx/releases) を参照

```shell
sudo curl -SL https://github.com/docker/buildx/releases/download/v0.34.1/buildx-v0.34.1.linux-arm64 -o /usr/local/lib/docker/cli-plugins/docker-buildx
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-buildx

docker buildx version
```
