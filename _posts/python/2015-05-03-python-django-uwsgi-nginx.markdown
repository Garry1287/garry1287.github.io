---
layout: post
title:  "python-django-uwsgi-nginx"
date:   2015-05-03 15:36:17 +0300
categories: python
tags: python
---

# python-django-uwsgi-nginx
virtualenv -p python3 venv
source venv/bin/activate

cd /srv/med/www
django-admin.py startproject project



STATIC_URL = '/static/'


STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),
]

в setting.py

2. static директорию создать в корне   project/static
3. В шаблоне нужно делать - 
{% load staticfiles %}
<link href="{% static "css/bootstrap-responsive.css" %}" rel="stylesheet">








Fedora, CentOS:

chown -R uwsgi:nginx /srv/myapp



/etc/uwsgi.d/myapp.ini
[uwsgi]
socket = /srv/myapp/uwsgi.sock
chmod-socket = 775
chdir = /srv/myapp/appdata
master = true
binary-path = /srv/myapp/bin/uwsgi
virtualenv = /srv/myapp
module = flaskapp:app
uid = www-data
gid = www-data
processes = 1
threads = 1
plugins = python3,logfile
logger = file:/srv/myapp/uwsgi.log







nginx configuration

We need to configure our web server. Here’s a basic configuration that will get us started:

Save this file as:

    Ubuntu, Debian: /etc/nginx/sites-enabled/myapp.conf
    Fedora, CentOS: /etc/nginx/conf.d/myapp.conf
    Arch Linux: add include /etc/nginx/conf.d/*.conf; to your http directive in /etc/nginx/nginx.conf and use /etc/nginx/conf.d/myapp.conf

server {
    # for a public HTTP server:
    listen 80;
    # for a public HTTPS server:
    # listen 443 ssl;
    server_name localhost myapp.local;

    location / {
        include uwsgi_params;
        uwsgi_pass unix:/srv/myapp/uwsgi.sock;
    }

    location /static {
        alias /srv/myapp/appdata/static;
    }

    location /favicon.ico {
        alias /srv/myapp/appdata/static/favicon.ico;
    }
}




For Fedora and CentOS

Make sure you followed the extra note about editing /etc/uwsgi.ini earlier and run:

systemctl enable nginx uwsgi
systemctl start nginx uwsgi
