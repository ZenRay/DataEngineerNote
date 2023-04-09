# DataEngineerNote
数据工程相关笔记

## [Docker](./Docker)
使用 Docker 搭建相应的环境:

### [hadoop](./Docker/hadoop/)
使用 Dockerfile 配置基本的环境，使用 `docker compose` 解决分布式环境。在搭建过程中踩过的坑:
* Dockerfile 中 `ENV` 和 `ARG` 等语句时，多参数整合为一行会出现报错，该用每个参数一个 `ENV`/ `ARG`
* 以 Dockerfile 搭建的容器为基础，使用 `docker compose` 启动容器 Dockerfile 中最后使用了 `CDM` 出现退出情况，因此在 Dockerfile 中取消 `CDM` 语句