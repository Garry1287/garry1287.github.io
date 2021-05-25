---
layout: post
title:  "python-django-wsgi"
date:   2018-09-19 02:34:57 +0300
categories: python
tags: python
---

# python-django-wsgi
[http://djbook.ru/rel1.7/topics/install.html](http://djbook.ru/rel1.7/topics/install.html)
[https://docs.djangoproject.com/en/1.8/howto/deployment/wsgi/](https://docs.djangoproject.com/en/1.8/howto/deployment/wsgi/)
[https://tyvik.ru/blog/147](https://tyvik.ru/blog/147)
[https://habrahabr.ru/post/226419/](https://habrahabr.ru/post/226419/)
[http://www.djangobook.com/en/2.0/chapter12.html](http://www.djangobook.com/en/2.0/chapter12.html)
[http://itman.in/django-webserver-nginx-uwsgi/](http://itman.in/django-webserver-nginx-uwsgi/)
[http://djbook.ru/ch20s04.html](http://djbook.ru/ch20s04.html)
[https://docs.djangoproject.com/en/1.9/howto/deployment/wsgi/modwsgi/](https://docs.djangoproject.com/en/1.9/howto/deployment/wsgi/modwsgi/)
[http://pytalk.ru/forum/django/17741/](http://pytalk.ru/forum/django/17741/)
[https://www.digitalocean.com/community/tutorials/how-to-run-django-with-mod_wsgi-and-apache-with-a-virtualenv-python-environment-on-a-debian-vps](https://www.digitalocean.com/community/tutorials/how-to-run-django-with-mod_wsgi-and-apache-with-a-virtualenv-python-environment-on-a-debian-vps)
[http://le087.ru/37/](http://le087.ru/37/)
[http://djbook.ru/rel1.5/howto/deployment/wsgi/modwsgi.html](http://djbook.ru/rel1.5/howto/deployment/wsgi/modwsgi.html)
[http://wiki.dieg.info/wsgidaemonprocess](http://wiki.dieg.info/wsgidaemonprocess)
[http://djbook.ru/examples/43/](http://djbook.ru/examples/43/)
[http://alxpy.com/blog/django-uwsgi-nginx/](http://alxpy.com/blog/django-uwsgi-nginx/)
[http://cultofdigits.com/articles/other/nastrojka-djangouwsginginx/](http://cultofdigits.com/articles/other/nastrojka-djangouwsginginx/)

Django на production. uWSGI + nginx
[https://habrahabr.ru/post/226419/](https://habrahabr.ru/post/226419/)


Мульти-хостинг django приложений с помощью nginx + uwsgi + virtualenv из песочницы
[https://habrahabr.ru/post/179831/](https://habrahabr.ru/post/179831/)

Парсер на python
[https://www.youtube.com/watch?v=BBDwd32Vwtg](https://www.youtube.com/watch?v=BBDwd32Vwtg)



Кто будет пытаться примеры запустить, учтите, что bookmarks соберётся только на МасOS - используется МacOS-only библиотека MacFSEvents.
Я, ламер, дочерта времени убил. Очень некрасиво со стороны автора.



Варианты  развёртывания django
[http://djbook.ru/rel1.9/howto/deployment/index.html](http://djbook.ru/rel1.9/howto/deployment/index.html)
[http://www.8host.com/blog/sravnenie-veb-serverov-prilozhenij-na-osnove-python/](http://www.8host.com/blog/sravnenie-veb-serverov-prilozhenij-na-osnove-python/)
[http://proft.me/2011/08/16/nastrojka-gunicorn-i-uwsgi-sravnenie-proizvoditeln/](http://proft.me/2011/08/16/nastrojka-gunicorn-i-uwsgi-sravnenie-proizvoditeln/)


1) Модули автономных сервреров (mod_wsgi) и тут 2 варианта (хотя есть и другие веб серверы и возможно у них есть свои модули)
        1.apache c модулем mod_wsgi  (статику можно отдавать с помощью nginx)       [http://djbook.ru/rel1.9/howto/deployment/wsgi/modwsgi.html](http://djbook.ru/rel1.9/howto/deployment/wsgi/modwsgi.html) (был ещё вариант mod_python с адаптером WSGI (Apache))
        2.nginx  c модулем mod_wsgi  (у nginx есть свой модуль для wsgi, статику также отдаем с помощью nginx)   [https://habrahabr.ru/post/62545/](https://habrahabr.ru/post/62545/)
2).uWSGI (нужен веб-сервер для проксирования запросов к uWSGI), до конца не понял может ли работать без стороннего веб сервера - да может, но это не кошерно - [https://habrahabr.ru/post/226419/](https://habrahabr.ru/post/226419/)
                    [http://djbook.ru/rel1.6/howto/deployment/wsgi/uwsgi.html](http://djbook.ru/rel1.6/howto/deployment/wsgi/uwsgi.html)
                    uWSGI основывается на клиент-серверной модели. Ваш веб-сервер (nginx, Apache...) обращается к рабочему процессу django-uwsgi для получения динамического контента. Подробнее описано в background documentation.
   
                        uWSGI является амбициозным проектом. Его набор инструментов позволяет выполнять гораздо более сложные задания, чем просто хостинг веб-приложений. Зарекомендовав себя как надежный и многофункциональный проект, на протяжении многих лет uWSGI остается незаменимым инструментом развертывания приложений для многих системных администраторов и разработчиков.

                            Начиная с версии 0.8.40, Nginx поддерживает протокол uwsgi (собственный протокол uWSGI). Это позволяет приложениям WSGI, запущенным на uWSGI, лучше взаимодействовать с Nginx. Благодаря этому развертывание приложений становится очень простым в настройке, чрезвычайно гибким, функциональным, а также может пользоваться преимуществами поставляемых оптимизаций. Все это делает сочетание uWSGI+Nginx великолепным вариантом для многих сценариев развертывания.
        
        
        1.uWSGI + nginx
            . Nginx нам нужен для отдачи статики и проксирования запросов к uWSGI. А uWSGI делает запросы питоновскому приложению и получает от него ответы. Взаимодействие между питоном и веб-сервером происходит по протоколу WSGI.

        Полный стек компонентов будет выглядеть следующим образом:
                    Пользователь <-> Веб-сервер <-> Сокет <-> uwsgi <-> Django
                         [http://itman.in/uwsgi-python-hosting/](http://itman.in/uwsgi-python-hosting/)
                         
        2.uWSGI + apache ( так сделать как я полагаю можно, но никто не делает, так как схема с nginx лучше, плюс nginx-ом можно отдававть статику, что является плюсом)
        
3).gunicorn (специальный web сервер Python WSGI HTTP Server for UNIX) + можно добавить nginx для отдачи статики как в классической схеме с apache
            [http://djbook.ru/rel1.9/howto/deployment/wsgi/gunicorn.html](http://djbook.ru/rel1.9/howto/deployment/wsgi/gunicorn.html)
4) flup
5).fastcgi - поддержка отключена
и др из статьи

Using flup or gunicorn or uWSGI behind nginx is much better,



Мнение одного дядьки ([http://stackoverflow.com/questions/2591715/deploying-django-fastcgi-apache-mod-wsgi-uwsgi-gunicorn)](http://stackoverflow.com/questions/2591715/deploying-django-fastcgi-apache-mod-wsgi-uwsgi-gunicorn))
Deploying Django (fastcgi, apache mod_wsgi, uwsgi, gunicorn)
Can someone explain the difference between apache mod_wsgi in daemon mode and django fastcgi in threaded mode. They both use threads for concurrency I think. Supposing that I'm using nginx as front end to apache mod_wsgi.

UPDATE:

I'm comparing django built in fastcgi(./manage.py method=threaded maxchildren=15) and mod_wsgi in 'daemon' mode(WSGIDaemonProcess example threads=15). They both use threads and acquire GIL, am I right?

UPDATAE 2:

So if they both are similar, is there any benefits of apache mod_wsgi against fastcgi. I see such pros of fastcgi:

    we don't need apache
    we consume less RAM
    I noticed that fastcgi has lesser overhead

UPDATAE 3:

I'm now happy with nginx + uwsgi.

UPDATAE 4:

I'm now happy with nginx + gunicorn :)







Рабочая схема
MySQL является узким местом до того, как будет реализовано нормальное кэширование. После этого, узкими местами становятся другие вещи, вообще это конечно весьма проекто-специфично.

1. CentOS
2. nginx(стратика + proxy_pass)
3. apache(mod_wsgi, workers=количество ядер CPU)
4. django
5. MySQL
6. RabbitMQ

Собствено ничего особенного, едиснтсвенное что, все «удалённые» операции которые не могут быть выполнены на уровне django+mysql (например http запросы к facebook и тд), делаются асинхронно в background-е. Таски при этом передаются через RabbitMQ 





Вот неплохие руководства

[http://openite.com/system/nastrojka-gunicorn-i-uwsgi-sravnenie-proizvoditeln.html](http://openite.com/system/nastrojka-gunicorn-i-uwsgi-sravnenie-proizvoditeln.html)
[https://habrahabr.ru/post/226419/](https://habrahabr.ru/post/226419/)
[https://uwsgi.readthedocs.io/en/latest/tutorials/Django_and_nginx.html#emperor-mode](https://uwsgi.readthedocs.io/en/latest/tutorials/Django_and_nginx.html#emperor-mode)
[http://monicalent.com/blog/2013/12/06/set-up-nginx-and-uwsgi/](http://monicalent.com/blog/2013/12/06/set-up-nginx-and-uwsgi/)
[https://chriswarrick.com/blog/2016/02/10/deploying-python-web-apps-with-nginx-and-uwsgi-emperor/](https://chriswarrick.com/blog/2016/02/10/deploying-python-web-apps-with-nginx-and-uwsgi-emperor/)
[http://djbook.ru/rel1.9/howto/deployment/wsgi/uwsgi.html](http://djbook.ru/rel1.9/howto/deployment/wsgi/uwsgi.html)
[http://code-maven.com/deploying-python-flask-using-uwsgi-on-ubuntu-14-04](http://code-maven.com/deploying-python-flask-using-uwsgi-on-ubuntu-14-04)
[http://perlmaven.com/deploying-pyton-with-uwsgi-on-ubuntu-13-10](http://perlmaven.com/deploying-pyton-with-uwsgi-on-ubuntu-13-10)
[https://habrahabr.ru/post/179831/](https://habrahabr.ru/post/179831/)
[https://habrahabr.ru/post/266473/](https://habrahabr.ru/post/266473/)


/srv/
        med
                www
                        conf (nginx и wsgi конфиги)
                        log
                        project(www)
                            ...(django project dirs and files)
                        venv (окружение для данного сайта)
                
Всё нужно делать под отдельным пользователем






В папке проекта необходимо запускать
(envmed) [root@centos7py project]# uwsgi --socket med.sock --module project.wsgi --chmod-socket=666


Название -module project.wsgi должно соответствовать названию проекта django, в противном случае будет ошибка
ImportError: No module named project.wsgi

Пока работает только под envmed



(envmed) [root@centos7py med]# cd project/
(envmed) [root@centos7py project]# ls
manage.py  med.sock  project  static  test.py
(envmed) [root@centos7py project]# uwsgi --socket med.sock --module project.wsgi --chmod-socket=666

Заработало

Для режима uwsgi emperor не запускалось, вообще не работал uwsgi, который находился не в virtualenv
Замучила ошибка  uwsgi upstream prematurely closed connection while reading response header from upstream,upstream prematurely closed connection while reading response header from upstream,

[http://djbook.ru/forum/topic/3286/](http://djbook.ru/forum/topic/3286/)

Помогла в конфиге 
etc/uwsgi.d/med-uwsgi.ini
прописать
[uwsgi]
plugins = python3

Ну и соответственно сам плагин я тоже поставил
uwsgi-plugin-python3.x86_64 : uWSGI - Plugin for Python 3 support


sudo ln /srv/med/conf/med-uwsgi.ini /etc/uwsgi.d/


Создал пользователя med:med и настроить его под uwsgi, чтобы у Nginx был доступ, надо nginx включить в группу med


Настройка переменных в конфиге [http://ivansimeyko.com/article/4/](http://ivansimeyko.com/article/4/)



