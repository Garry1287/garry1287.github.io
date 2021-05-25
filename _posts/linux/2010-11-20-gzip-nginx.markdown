---
layout: post
title:  "gzip-nginx"
date:   2010-11-20 07:11:58 +0300
categories: linux
tags: linux
---

# gzip-nginx
Gzip сжатие статических файлов
Настраивается как в апаче, так и в nginx
В нашем случае в nginx, так как он обрабатывает статику

Отличный мануал
[http://n-wp.ru/13969](http://n-wp.ru/13969)


<ifmodule mod_deflate="" c="">
  SetOutputFilter DEFLATE
  Header append Vary User-Agent
</ifmodule>

Подробнее тут: [http://zmoe.ru/kak-vklyuchit-gzip-szhatie/#ixzz3W2K6UUyr](http://zmoe.ru/kak-vklyuchit-gzip-szhatie/#ixzz3W2K6UUyr)



# сжатие text, html, javascript, css, xml:
<ifModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml application/xml application/xhtml+xml text/css text/javascript application/javascript application/x-javascript
</ifModule>



http {

    ...

    # Включение модуля
    gzip             on;

    # Минимальная длина ответа, при которой модуль будет жать, в байтах
    gzip_min_length  1000;

    # Разрешить сжатие для всех проксированных запросов 
    gzip_proxied     any;

    # MIME-типы которые необходимо жать
    #gzip_types text/plain text/html text/xml application/xml application/x-javascript text/javascript text/css text/json;
    # Если у вас появляются варнинги, типа "duplicate MIME type text/html", то вам стоит исключить text/html
    #gzip_types text/plain text/xml application/xml application/x-javascript text/javascript text/css text/json;

    # Запрещает сжатие ответа методом gzip для IE6
    gzip_disable     "msie6";

    # Уровень gzip-компрессии
    gzip_comp_level  8;

    ...

}



gzip on;
gzip_disable "msie6";
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_buffers 16 8k;
gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

Подробнее тут: [http://zmoe.ru/kak-vklyuchit-gzip-szhatie/#ixzz3W2NwEdgb](http://zmoe.ru/kak-vklyuchit-gzip-szhatie/#ixzz3W2NwEdgb)


[http://ruhighload.com/index.php/2009/04/24/%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-nginx/](http://ruhighload.com/index.php/2009/04/24/%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-nginx/)
[http://yapro.ru/web-master/apache/nastroyka-gzip-v-nginx.html](http://yapro.ru/web-master/apache/nastroyka-gzip-v-nginx.html)












Кеширование в браузере статической информации
[http://ruhighload.com/post/%D0%9A%D0%B0%D0%BA+%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C+%D0%BA%D0%B5%D1%88%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5+Cache-control+%D0%B2+Nginx%3F](http://ruhighload.com/post/%D0%9A%D0%B0%D0%BA+%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C+%D0%BA%D0%B5%D1%88%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5+Cache-control+%D0%B2+Nginx%3F)

[http://seo-mayak.com/sozdanie-bloga/skorost-zagruzki/kak-vklyuchit-kesh-brauzera-na-storone-polzovatelya.html](http://seo-mayak.com/sozdanie-bloga/skorost-zagruzki/kak-vklyuchit-kesh-brauzera-na-storone-polzovatelya.html)


<IfModule mod_expires.c>

Header append Cache-Control "public"

FileETag MTime Size

ExpiresActive On

ExpiresDefault "access plus 0 minutes"

ExpiresByType image/ico "access plus 1 years"

ExpiresByType text/css "access plus 1 years"

ExpiresByType text/javascript "access plus 1 years"

ExpiresByType image/gif "access plus 1 years"

ExpiresByType image/jpg "access plus 1 years"

ExpiresByType image/jpeg "access plus 1 years"

ExpiresByType image/bmp "access plus 1 years"

ExpiresByType image/png "access plus 1 years"

</IfModule>


