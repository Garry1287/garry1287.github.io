---
layout: post
title:  "python + mysql"
date:   2009-01-19 06:42:45 +0300
categories: python
tags: python
---

# python + mysql
python + mysql
[http://toly-blog.ru/programming/python-recepty-druzhim-python-i-mysql/](http://toly-blog.ru/programming/python-recepty-druzhim-python-i-mysql/)
[http://webonrails.ru/post/71270402097156262/](http://webonrails.ru/post/71270402097156262/)
[http://rtfm.co.ua/python-rabota-s-mysql-s-ispolzovaniem-mysqldb/](http://rtfm.co.ua/python-rabota-s-mysql-s-ispolzovaniem-mysqldb/)
[http://wikipython.ru/modules/mysql-python](http://wikipython.ru/modules/mysql-python)
[http://www.internet-technologies.ru/articles/article_2190.html](http://www.internet-technologies.ru/articles/article_2190.html)

Установка
[http://rtfm.co.ua/centos-pip-install-mysql-python-installationerror/](http://rtfm.co.ua/centos-pip-install-mysql-python-installationerror/)
Установить возможно потребуется следующие пакеты
yum -y install python-devel mysql-devel


mysqlclient  -  это новый модуль для python3, работающий как MySQLdb
[https://pypi.python.org/pypi/mysqlclient](https://pypi.python.org/pypi/mysqlclient)
[https://github.com/PyMySQL/mysqlclient-python](https://github.com/PyMySQL/mysqlclient-python)
[https://mysqlclient.readthedocs.org/en/latest/user_guide.html#mysql](https://mysqlclient.readthedocs.org/en/latest/user_guide.html#mysql) 

Установка mysqlclient
pip install mysqlclient

для второй версии надо обычный MySQLdb


Работа со строками
[http://pythonworld.ru/tipy-dannyx-v-python/stroki-funkcii-i-metody-strok.html](http://pythonworld.ru/tipy-dannyx-v-python/stroki-funkcii-i-metody-strok.html)
[http://pythonworld.ru/osnovy/formatirovanie-strok-metod-format.html](http://pythonworld.ru/osnovy/formatirovanie-strok-metod-format.html)
[http://www.ibm.com/developerworks/ru/library/l-python_part_2/index.html](http://www.ibm.com/developerworks/ru/library/l-python_part_2/index.html)
[http://pythonworld.ru/osnovy/formatirovanie-strok-operator.html](http://pythonworld.ru/osnovy/formatirovanie-strok-operator.html)
[http://pythonworld.ru/osnovy/formatirovanie-strok-metod-format.html](http://pythonworld.ru/osnovy/formatirovanie-strok-metod-format.html)
[https://docs.python.org/2.4/lib/typesseq-strings.html](https://docs.python.org/2.4/lib/typesseq-strings.html)
[http://habrahabr.ru/post/236633/](http://habrahabr.ru/post/236633/)

Циклы
[http://www.python-course.eu/python3_for_loop.php](http://www.python-course.eu/python3_for_loop.php)
[http://radio-hobby.org/modules/instruction/python/43-funktsii-range-i-xrange](http://radio-hobby.org/modules/instruction/python/43-funktsii-range-i-xrange)


Paramstyle у модулей работы с БД - вопрос с экранированием
[http://stackoverflow.com/questions/25236777/change-paramstyle-on-python-mysqldb-module](http://stackoverflow.com/questions/25236777/change-paramstyle-on-python-mysqldb-module)
[http://stackoverflow.com/questions/2969044/python-string-escape-vs-unicode-escape](http://stackoverflow.com/questions/2969044/python-string-escape-vs-unicode-escape)
[http://bobby-tables.com/python](http://bobby-tables.com/python)

Python

Using the Python DB API, don't do this:

# Do NOT do it this way.
cmd = "update people set name='%s' where id='%s'" % (name, id)
curs.execute(cmd)

Instead, do this:

cmd = "update people set name=%s where id=%s"
curs.execute(cmd, (name, id))

Note that the placeholder syntax depends on the database you are using.

'qmark'         Question mark style,
                e.g. '...WHERE name=?'
'numeric'       Numeric, positional style,
                e.g. '...WHERE name=:1'
'named'         Named style,
                e.g. '...WHERE name=:name'
'format'        ANSI C printf format codes,
                e.g. '...WHERE name=%s'
'pyformat'      Python extended format codes,
                e.g. '...WHERE name=%(name)s'

The values for the most common databases are:

>>> import MySQLdb; print MySQLdb.paramstyle
format
>>> import psycopg2; print psycopg2.paramstyle
pyformat
>>> import sqlite3; print sqlite3.paramstyle
qmark

So if you are using MySQL or PostgreSQL, use %s (even for numbers and other non-string values!) and if you are using SQLite use ?
To do

    Add some narrative.


    
    
    [http://blog.nagaychenko.com/2011/03/11/%D0%BE%D1%81%D0%BE%D0%B1%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-last_insert_id-%D0%B8-auto_increment-%D0%B2-mysql/](http://blog.nagaychenko.com/2011/03/11/%D0%BE%D1%81%D0%BE%D0%B1%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-last_insert_id-%D0%B8-auto_increment-%D0%B2-mysql/)
    [https://github.com/PyMySQL/mysqlclient-python](https://github.com/PyMySQL/mysqlclient-python)
    
    Хорошие примеры
    [https://github.com/PyMySQL/mysqlclient-python](https://github.com/PyMySQL/mysqlclient-python)


Создание модулей и пакетов
[http://python-lab.blogspot.ru/2012/07/python-201.html](http://python-lab.blogspot.ru/2012/07/python-201.html)



Устанавливаем mysqlclient через pip ([https://github.com/PyMySQL/mysqlclient-python)](https://github.com/PyMySQL/mysqlclient-python))
Во втором python работает
import MySQLdb

В третьем не работает
Требовалось поставить gcc, python-devel
