---
layout: post
title:  "docker-first"
date:   2015-05-23 00:11:27 +0300
categories: docker-first
tags: devops
---

# docker-first
Zabbix web-interface based on Nginx web server with PostgreSQL database support


docker run --name some-zabbix-web-nginx-pgsql -e DB_SERVER_HOST="some-postgres-server" -e POSTGRES_USER="some-user" -e POSTGRES_PASSWORD="some-password" -e ZBX_SERVER_HOST="some-zabbix-server" -e PHP_TZ="some-timezone" -d zabbix/zabbix-web-nginx-pgsql:tag


sudo docker run --name rabbitmq -p 8080:80 -d --network mynetwork rabbitmq


docker network create, указав опцию --driver bridge. 



docker network create --driver bridge --subnet 192.168.100.0/24 --ip-range 192.168.100.0/24 my-bridge-networ



docker run -it --name=test_brifge04_2 --net brifge04 --ip=10.1.4.100 centos:centos7 /bin/bash

