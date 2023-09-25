<!--
title:   Apple Silicon(M1, M2) MacBookAirでDocker上にMySQLサーバを立てる
tags:    Docker,M1,Mac,MySQL
id:      79d07be0bbf65f27351a
private: false
-->
自分用のメモになりますので、早速結論を書く。
何か誤りがありましたら、編集リクエストかコメント下さい。

# Dockerfileの場合

```Dockerfile
FROM --platform=linux/arm64/v8 mysql/mysql-server:latest

# 追加で実行する処理(参考)
ENV TZ=Asia/Tokyo
ENV MYSQL_ROOT_PASSWORD=password
COPY ./docker/mysql/my.cnf /etc/mysql/conf.d/my.cnf
COPY ./docker/mysql/initdb.d /docker-entrypoint-initdb.d
```

# docker-composeの場合

```docker-compose.yml
version: '3'
services:
  mysql:
    image: mysql/mysql-server:latest
    platform: linux/arm64/v8
    environment:
      MYSQL_ROOT_PASSWORD: password
    ports:
      - 127.0.0.1:3306:3306
```