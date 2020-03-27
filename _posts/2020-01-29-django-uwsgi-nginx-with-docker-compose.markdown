---
layout: post
title:  "Запуск Django вместе с postgres, uwsgi, nginx в docker-compose"
date:   2020-01-29 14:02:10 +0300
categories: jekyll posts
---



#Запуск Django вместе с postgres, uwsgi, nginx в docker-compose

План действий
1. Просто запустить Django (пустой) в контейнере
2. Запустить django в контейнере через uwsgi
3. Запусить django с DB в 2 контейнерах
4. Запусить 3 контейнера с nginx

/code - папка для проекта (как volume) для django и nginx контейнеров 
/sock - папка для socket (как volume) для django и nginx контейнеров 
/var/lib/postgresql/data (как volume) для postgresql контейнера



###Структура проекта при запуске на сервере без контейнеров.
```
/srv/ 
        - nlmk-project
            - www
                - django-project-name(nlmk)
                    - manage.py
                    - [..django-project-apps..]
                    - static
            - env
                - bin
                - include
                - lib
                - share
            - logs
                - nginx_access.log
            - config
                - nginx
                - postgres
                - pip
                - uwsgi
            - dbdata
            - docker-compose.yml
            - dockerfiles
```
При запуске без контейнера не используются docker-compose, dockerfiles

При запуске в контейнерах не используюется logs, env

###Что такое docker-entrypoint-initdb.d

Позволяет инициировать DB в докер образе postgres (также работает в mysql)
COPY ./config/postgres/pg-setup.sql /docker-entrypoint-initdb.d/


Database in Docker conteiner
[https://medium.com/@wkrzywiec/database-in-a-docker-container-how-to-start-and-whats-it-about-5e3ceea77e50](https://medium.com/@wkrzywiec/database-in-a-docker-container-how-to-start-and-whats-it-about-5e3ceea77e50) 

####Пример
 Это мой Dockerfile:
```
FROM mysql
ADD script.sql /docker-entrypoint-initdb.d/script.sql
RUN chmod -R 775 /docker-entrypoint-initdb.d

ENV MYSQL_ROOT_PASSWORD mypass

Это мой script.sql:

CREATE DATABASE mydb;
CREATE DATABASE mydb2;
```
Я строю и запускаю контейнер:
```
$ docker build -t mysql .
$ docker run -v data_volume:/var/lib/mysql --name somedb -d mysql
```

Во многих статьях предлагают запускать Django обычной командой `python manage.py`

```
services:
  db:
    image: postgres
    volumes:
      - /data/postgres_data:/var/lib/postgresql/data/
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db

volumes:
  postgres_data:
```
Но мы так не будем делать, а сделаем через uwsgi.


###В процессе возникли следующие проблемы
1.  Доступ к совместому сокеру в volume sock. Проблема прав


` to unix:///sock/nlmk.sock failed (13: Permission denied) while connecting to upstream, client: 192.168.121.1, server: , request: "GET / HTTP/1.1", upstream: "uwsgi://unix:///sock/nlmk.sock:", host: "192.168.121.60:8088`
Нашёл подобные рассуждения
```
Допустим, есть директория куда пишутся логи и она монтируется в контейнер). Соответственно php-fpm по умолчанию запускается от www-data и прав писать у него в эту директорию нет. Как можно решить данную задачу? Рассмотрим 6 способов:

    можно поставить chmod -R 777 на директорию в хосте
    можно сделать владельца в хосте www-data
    можно стартануть php-fpm изменив в конфиге pool на имя пользователя = имени в хосте
    можно переопределить пользователя в dockerfile user 1000 например
    user 1000 можно задать в docker-compose.yml
    можно сделать в докер файле usermod -u 1000 www-data

```
Я сделал 777 для сокета и папки. Не совсем верно это.

2. Не верно настраивал setting.py в django. Чтобы postgres заработал нужно указать имя контейнера, которое само резолвится в ip.  Понять что происходит помог DEBUG в Django.

Была 500-а ошибка так как в настройке БД - был 127.0.0.1:5432, как поменяли на projectname_postgres:5432 в setting.py, 

3. 400 ошибка была связана с настройками ALLOWED_HOSTS = ['*']
[https://stackoverflow.com/questions/24192283/django-uwsgi-nginx-bad-request-400](https://stackoverflow.com/questions/24192283/django-uwsgi-nginx-bad-request-400) 

[https://fooobar.com/questions/15110394/getting-400-bad-request-error-frequently-when-trying-to-use-flask-socket-with-uwsgi-and-nginx](https://fooobar.com/questions/15110394/getting-400-bad-request-error-frequently-when-trying-to-use-flask-socket-with-uwsgi-and-nginx) 

[https://adminvps.ru/blog/nginx-i-open-permission-denied-while-reading-upstream-oshibka-ispmanager/](https://adminvps.ru/blog/nginx-i-open-permission-denied-while-reading-upstream-oshibka-ispmanager/) 


4. Само понимание как делать возникло при пошаговой реализации по статье
[https://medium.com/faun/tech-edition-how-to-dockerize-a-django-web-app-elegantly-924c0b83575d](https://medium.com/faun/tech-edition-how-to-dockerize-a-django-web-app-elegantly-924c0b83575d) 

Ещё полезные ссылки
[https://github.com/damsonn/django-docker-compose](https://github.com/damsonn/django-docker-compose) 
[https://cloud.croc.ru/blog/byt-v-teme/docker-upravlenie-dannymi/](https://cloud.croc.ru/blog/byt-v-teme/docker-upravlenie-dannymi/) 
[https://stackoverflow.com/questions/45774221/how-to-run-docker-exec-on-a-docker-compose-yml](https://stackoverflow.com/questions/45774221/how-to-run-docker-exec-on-a-docker-compose-yml) 
[https://zotovp.wordpress.com/2019/07/07/djangouwsginginxpostgresql-in-dockerdocker-compose-for-development-and-production-deployment-%d1%80%d0%b0%d0%b7%d0%bc%d0%b5%d1%89%d0%b5%d0%bd%d0%b8%d0%b5-djangouwsginginxpostgresql-%d0%b2/](https://zotovp.wordpress.com/2019/07/07/djangouwsginginxpostgresql-in-dockerdocker-compose-for-development-and-production-deployment-%d1%80%d0%b0%d0%b7%d0%bc%d0%b5%d1%89%d0%b5%d0%bd%d0%b8%d0%b5-djangouwsginginxpostgresql-%d0%b2/) 



[https://github.com/hendrikfrentrup/docker-django/tree/develop](https://github.com/hendrikfrentrup/docker-django/tree/develop) 
[https://github.com/hendrikfrentrup/docker-django/commit/b0e8e186ab275fb94c3c53f267ebe2853ef3d127](https://github.com/hendrikfrentrup/docker-django/commit/b0e8e186ab275fb94c3c53f267ebe2853ef3d127) 


Хорошее руководство c картинками
[https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial/blob/master/README.en.md](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial/blob/master/README.en.md) 


[https://medium.com/faun/tech-edition-django-dockerization-with-bells-and-whistles-and-a-tad-bit-of-cleverness-2b5d1b57e289](https://medium.com/faun/tech-edition-django-dockerization-with-bells-and-whistles-and-a-tad-bit-of-cleverness-2b5d1b57e289) 

[http://pawamoy.github.io/2018/02/01/docker-compose-django-postgres-nginx.html](http://pawamoy.github.io/2018/02/01/docker-compose-django-postgres-nginx.html) 









Версии compose файла зависят от версии docker
[https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/) 



Запуск с тестом (браузер для тестирования)
[https://emacsway.github.io/ru/docker/](https://emacsway.github.io/ru/docker/) 
[https://medium.com/zeitcode/a-simple-recipe-for-django-development-in-docker-bonus-testing-with-selenium-6a038ec19ba5](https://medium.com/zeitcode/a-simple-recipe-for-django-development-in-docker-bonus-testing-with-selenium-6a038ec19ba5) 



Пример с SSL
[https://hashedin.com/blog/deployment-with-docker-compose/](https://hashedin.com/blog/deployment-with-docker-compose/) 




Можно так compose запускать (web - это служба)
`docker-compose -f docker-compose.prod.yml run web python manage.py migrate`



Неплохой пример 
[https://ruddra.com/posts/docker-django-nginx-postgres/](https://ruddra.com/posts/docker-django-nginx-postgres/) 

Тут описано как залазить в запущенный контейнер, смотреть логи
```
#Nginx
docker exec -ti nginx bash

#Web
docker exec -ti web bash

#Database
docker exec -ti db bash

For logs:

#Nginx
docker-compose logs nginx
#Web
docker-compose logs web
#DB
docker-compose logs db
```
Как я делал
```
  817  docker  logs projectname_django
  818  docker  logs projectname_nginx
  819  docker  logs projectname_django
  820  docker  logs projectname_nginx
  821  docker  logs projectname_django
  822  docker exec -it projectname_django /bin/bash
  823  docker exec -it projectname_postgers /bin/bash
  824  docker exec -it projectname_postgres /bin/bash
  825  docker exec -it projectname_django /bin/bash
```

Сделал отдельную сеть, как рекомендуют
```
networks:  # <-- here
      - nginx_network


 networks:  # <-- here
      - nginx_network


networks:  # <-- and here
  nginx_network:
    driver: bridge
```


##Использование  Environment

[https://techstream.org/Web-Development/Development-Environment-for-Django-in-docker-compose](https://techstream.org/Web-Development/Development-Environment-for-Django-in-docker-compose) 


Создаём отдельный .env файл для переменных окружения
```
POSTGRES_PASSWORD=secret
POSTGRES_USER=postgres
DJANGO_SECRET_KEY=secret
```

В setting.py получаем переменную окружения
```
POSTGRES_PASSWORD = os.environ.get('POSTGRES_PASSWORD')


DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',                      
        'USER': 'postgres',
        'PASSWORD': POSTGRES_PASSWORD,
        'HOST': 'db',
        'PORT': '5432', 
    }
}
```

.env файл по умолчанию не сработал, руками прописал файл в docker-compose.yml
Может не совсем понял [https://docs.docker.com/compose/environment-variables/https://docs.docker.com/compose/environment-variables/](https://docs.docker.com/compose/environment-variables/) 

Возможно использовать проект

[https://pypi.org/project/python-decouple/](https://pypi.org/project/python-decouple/) 

Возможно тут сработает .env по умолчанию

```
Он также применил полезную и обычно используемую иерархию для получения конфигурации: во-первых, найдите переменную среды, в противном случае проверьте файл .env в корне проекта, в противном случае выберите значение по умолчанию. 
```
Или
```
   Environment variables;
    Repository: ini or .env file;
    default argument passed to config.
```

   
Хорошая статья о ENV
[https://habr.com/ru/company/otus/blog/337688/](https://habr.com/ru/company/otus/blog/337688/) 



Не пользовался, но тоже хорошая статья с примерами об Environment
[https://www.eidel.io/2017/07/10/dockerizing-django-uwsgi-postgres/](https://www.eidel.io/2017/07/10/dockerizing-django-uwsgi-postgres/) 


Возможно работает только с этим модулем 
django-environ
 `pip install django-environ`

```
import environ
env = environ.Env(
# set casting, default value
DEBUG=(bool, False)
)
# reading .env file
environ.Env.read_env()

# False if not in os.environ
DEBUG = env('DEBUG')

# Raises django's ImproperlyConfigured exception if SECRET_KEY not in os.environ
SECRET_KEY = env('SECRET_KEY')
```

```
import django-environ
env = environ.Env()
env.read_env(env.str('ENV_PATH', '/path/to/.env'))
AWS_ACCESS_KEY_ID = env('AWS_ACCESS_KEY_ID')
AWS_SECRET_ACCESS_KEY = env('AWS_SECRET_ACCESS_KEY')
AWS_STORAGE_BUCKET_NAME = env('AWS_STORAGE_BUCKET_NAME')
```



### Запуск просто Docker
```
FROM python:3.6.8-alpine
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD ./ /code/
CMD ["python", "mysite/manage.py", "runserver", "0.0.0.0:8001"]
````


`docker-compose exec web python mysite/manage.py migrate`


Лог действий
```
  899  docker build -t django-docker:0.0.1 .
  900  docker run -p 8001:8001 docker-django:0.0.1
  901  docker ps
  902  docker ps -a
  903  docker images
  904  docker run -p 8001:8001 docker-django
  905  docker ps
  906  deactivate
  907  docker run -p 8001:8001 docker-django
  908  docker images
  909  docker run -p 8001:8001 docker-django:0.0.1
  910  docker run -p 8001:8001 django-docker:0.0.1
  911  vi docker-compose.yml
  912  ls
  913  docker-compose up. 
  914  docker-compose up
  915  docker ps
  916  docker images
  917  vi docker-compose.yml
  918  docker-compose up
  919  vi docker-compose.yml
  920  docker-compose up
  921  ls
  922  cp Dockerfile Dockerfile-via-docker
  923  vi Dockerfile
  924  docker-compose up
  925  docker-compose exec web python mysite/manage.py migrate
  926  docker-compose exec testdjango_web_1 python mysite/manage.py migrate
  927  docker ps
  928  docker ps -a
  929  docker-compose exec testdjango_web python mysite/manage.py migrate
  930  cat docker-compose.yml 
  931  docker-compose exec testdjango_web_1 python mysite/manage.py migrate
  932  docker-compose exec testdjango_web python mysite/manage.py migrate
  933  docker-compose exec web python mysite/manage.py migrate
  934  ls
  935  cat docker-compose.yml 
  936  docker-compose ps
  937  docker-compose exec testdjango_web_1 python mysite/manage.py migrate
  938  docker-compose ps
  939  docker-compose ps -a
  940  ls
  941  cat Dockerfile
```
В следующий раз сразу в git пихать и коммитить.
































