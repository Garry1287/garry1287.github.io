---
layout: post
title:  "openssl-ca"
date:   2015-02-19 02:06:30 +0300
categories: vpn
tags: vpn
---

# openssl-ca

CA.key - корневой ключ

Корневой сертификат
openssl req -x509 -new -key rootCA.key -days 10000 -out rootCA.crt

ca.crt

Создаем сертификат подписаный нашим СА

Генерируем ключ.

openssl genrsa -out server101.mycloud.key 2048


Создаем запрос на сертификат.

openssl req -new -key server101.mycloud.key -out server101.mycloud.csr


Тут важно указать имя сервера: домен или IP (например домен server101.mycloud)

Common Name (eg, YOUR name) []: server101.mycloud


и подписать запрос на сертификат нашим корневым сертификатом.

openssl x509 -req -in server101.mycloud.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out server101.mycloud.crt -days 5000




 ca.pem 
 ca-key.pem
CA.crt — можно давать друзьям, устанавливать, копировать не сервера, выкладывать в публичный доступ
CA.key — следует держать в тайне
