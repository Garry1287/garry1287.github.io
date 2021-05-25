---
layout: post
title:  "python-virtualenv"
date:   2011-07-15 22:19:49 +0400
categories: python
tags: python
---

# python-virtualenv

--------------------------------------------------------------------------------------
Virtualenv
-----------------------------------------------------------------------------------------
--no-site-packages
-p /usr/bin/python2.7
  -p PYTHON_EXE, --python=PYTHON_EXE
                        The Python interpreter to use, e.g.,
                        --python=python2.5 will use the python2.5 interpreter
                        to create the new environment.  The default is the
                        interpreter that virtualenv was installed with
                        (/usr/bin/python3)




virtualenv --no-site-packages --python=python2.5 env2


 virtualenv --no-site-packages --python=python2.7 env2

[http://proft.me/2010/04/3/python-i-okruzhenie-virtualenv/](http://proft.me/2010/04/3/python-i-okruzhenie-virtualenv/)





Так вот, virtualenv — это инструмент, позволяющий создавать виртуальные окружения с пакетами. Разные «песочницы» (согласитесь, напоминает sandbox’ы в Cabal) имеют разный набор пакетов разных версий. Работая над конкретным проектом, вы просто переключаетесь на подходящую песочницу, и проблема уходит. Заметьте, что в отличие от того, как это сделано в некоторых других языках программирования, одну и ту же песочницу можно смело использовать сразу в нескольких проектах. Плюс к этому уходит проблема засорения системы ненужными пакетами, так как песочницы можно легко создавать и удалять. Как я это вижу, программируя на Python в третьем тысячелетии, вообще все нужно делать через virtualenv!

Установка virtualenv и virtualenvwrapper, предоставляющего чуть более удобный интерфейс к virtualenv:
sudo pip3 install virtualenv virtualenvwrapper

В ~/.bashrc дописываем:
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/bin/virtualenvwrapper.sh

Создаем новое окружение:
mkvirtualenv env-name

Смотрим список окружений:
workon

Меняем окружение:
workon env-name

Выходим из окружения:
deactivate

Удаляем окружение:
rmvirtualenv env-name

Находясь в одном из окружений, можно ставить пакеты через pip, как обычно:
pip3 install flask

Список зависимостей проекта, насколько я смог разобраться, принято сохранять в файл с именем requirements.txt:
pip3 freeze > requirements.txt

Этот подход позволяет одной командой установить все зависимости, необходимые проекту:
pip3 install -r requirements.txt

Заметьте, что если вы используете bpython, его тоже придется установить в песочницу. После этого его можно запустить как обычно, сказав bpython. Подозреваю, что то же справедливо и в отношении некоторых других утилит, написанных на Python. В связи с этим поддержание минимального requirements.txt становится не такой уж простой задачей.

Решение, насколько я понимаю, заключается в использовании двух песочниц на проект — одной чистой, содержащей минимальный набор зависимостей, и одной песочницы, предназначенной для разработки. Думаю, такой подход в любом случае не лишен смысла, так как вряд ли вы захотите тянуть на боевой сервер всевозможные моки и фреймворки для тестирования. Что же касается проверки корректности соответствующих файлов requirements.txt, тут на помощь приходит continuous integration. По идее, должно работать.

Ссылки по теме:

    [https://pypi.python.org/pypi/virtualenv](https://pypi.python.org/pypi/virtualenv);
    [http://virtualenvwrapper.readthedocs.io/en/latest/](http://virtualenvwrapper.readthedocs.io/en/latest/);

А используете ли вы virtualenv?Так вот, virtualenv — это инструмент, позволяющий создавать виртуальные окружения с пакетами. Разные «песочницы» (согласитесь, напоминает sandbox’ы в Cabal) имеют разный набор пакетов разных версий. Работая над конкретным проектом, вы просто переключаетесь на подходящую песочницу, и проблема уходит. Заметьте, что в отличие от того, как это сделано в некоторых других языках программирования, одну и ту же песочницу можно смело использовать сразу в нескольких проектах. Плюс к этому уходит проблема засорения системы ненужными пакетами, так как песочницы можно легко создавать и удалять. Как я это вижу, программируя на Python в третьем тысячелетии, вообще все нужно делать через virtualenv!

Установка virtualenv и virtualenvwrapper, предоставляющего чуть более удобный интерфейс к virtualenv:
sudo pip3 install virtualenv virtualenvwrapper

В ~/.bashrc дописываем:
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/bin/virtualenvwrapper.sh

Создаем новое окружение:
mkvirtualenv env-name

Смотрим список окружений:
workon

Меняем окружение:
workon env-name

Выходим из окружения:
deactivate

Удаляем окружение:
rmvirtualenv env-name

Находясь в одном из окружений, можно ставить пакеты через pip, как обычно:
pip3 install flask

Список зависимостей проекта, насколько я смог разобраться, принято сохранять в файл с именем requirements.txt:
pip3 freeze > requirements.txt

Этот подход позволяет одной командой установить все зависимости, необходимые проекту:
pip3 install -r requirements.txt

Заметьте, что если вы используете bpython, его тоже придется установить в песочницу. После этого его можно запустить как обычно, сказав bpython. Подозреваю, что то же справедливо и в отношении некоторых других утилит, написанных на Python. В связи с этим поддержание минимального requirements.txt становится не такой уж простой задачей.

Решение, насколько я понимаю, заключается в использовании двух песочниц на проект — одной чистой, содержащей минимальный набор зависимостей, и одной песочницы, предназначенной для разработки. Думаю, такой подход в любом случае не лишен смысла, так как вряд ли вы захотите тянуть на боевой сервер всевозможные моки и фреймворки для тестирования. Что же касается проверки корректности соответствующих файлов requirements.txt, тут на помощь приходит continuous integration. По идее, должно работать.

Ссылки по теме:

    [https://pypi.python.org/pypi/virtualenv](https://pypi.python.org/pypi/virtualenv);
    [http://virtualenvwrapper.readthedocs.io/en/latest/](http://virtualenvwrapper.readthedocs.io/en/latest/);

А используете ли вы virtualenv?
