# mgate-cloud 安装与部署

`mgate-cloud-install` 提供 mgate-cloud 的公开部署文件与发布资产，不包含应用源码。

## Docker Compose 部署

请先安装 Docker 与 Docker Compose，然后执行：

```bash
mkdir mgate-cloud && cd mgate-cloud
curl -fsSLO https://raw.githubusercontent.com/akiiya/mgate-cloud-install/main/docker-compose.yml
curl -fsSLO https://raw.githubusercontent.com/akiiya/mgate-cloud-install/main/.env.example
cp .env.example .env
# 编辑 .env，替换 MYSQL_PASSWORD、MYSQL_ROOT_PASSWORD 与 MGATE_APP_SECRET。
docker compose up -d
```

打开 [http://127.0.0.1:22880/#/setup](http://127.0.0.1:22880/#/setup) 完成管理员初始化。

## Linux 一键安装

以下命令会下载最新 Release 的对应架构二进制、校验 SHA256，并安装为 systemd 服务：

```bash
curl -fsSL https://raw.githubusercontent.com/akiiya/mgate-cloud-install/main/install.sh | sudo bash
```

重复执行同一命令即可升级，原有配置与数据会保留。

## 数据与升级

- Docker 配置：`./data/config/config.yaml`
- Docker MySQL 数据：`./data/mysql/`
- 应用默认仅监听：`127.0.0.1:22880`
- Docker 升级：`docker compose pull && docker compose up -d`

请勿将 `.env` 或 `data/` 提交到版本控制；升级前建议完成备份。

## 发布资产

每个 Release 均提供 Linux/Windows 二进制压缩包、`SHA256SUMS`、Docker Compose 文件及安装/卸载脚本。

## 镜像版本

Docker Compose 默认使用 `latest` 镜像。如需固定版本，请在 `.env` 中设置 `MGATE_IMAGE_TAG`，例如 `0.2.3`。
