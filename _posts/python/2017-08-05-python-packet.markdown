---
layout: post
title:  "python-packet"
date:   2017-08-05 02:23:21 +0300
categories: python
tags: python
---

# python-packet
Системные пакеты (т.е. те, которые устанавливаются при помощи APT или другого менеджера пакетов) помещаются в /usr/lib/python2.4/site-packages. 
Если вы сами ставите пакет при помощи python setup.py install, то он по умолчанию помещается в вышеуказанный каталог, куда доступ на запись - только у root. 
    Стандартным для системы способом (пакет для Linux, инсталлятор для Windows)
    Из исходных текстов (python setup.py install) - это distutils
   
   Python eggs (предлагают ставить в отдельную папку (домашнюю), чтобы отделять пакеты установленные разным способом друг от дргуа
[http://pyobject.ru/blog/2006/12/21/cooking-python-eggs/](http://pyobject.ru/blog/2006/12/21/cooking-python-eggs/)






            Создание пакетов и установка с помощью distutils
            
 и какие возможности в нем отсутствуют.
Когда пакет создается с помощью distutils, обычно установка такого
пакета выполняется командой:
python setup.py install
           
            
Теперь достаточно сделать
python setup.py sdist
и просто магическим образом появляется директория dist с файлом pyfoo-1.2.3.tar.gz.
Теперь любому пользователю достаточно распаковать этот архив и сказать python setup.py install. Все файлы модуля окажутся там где им положено быть (например, в /usr/lib/python2.5/site-packages/pyfoo).
([http://blog-ru.greenmice.info/2008/08/python-distutils.html)](http://blog-ru.greenmice.info/2008/08/python-distutils.html))

При такой установке пакет будет установлен в вашу основную версию Python, чтобы этого избежать необходимо исопльзовать virtualenv или подобную вещь

        Setuptools 
Setuptools библиотека, расширяющая возможности distutils, который являлся основным средством создания установочных пакетов с модулями, написанными на python. 

Создание пакетов «eggs» – это
особенность библиотеки setuptools, которая работает с easy_install.

Согласно официальной документации «Easy Install – это модуль на
языке Python (easy_install), связанный с библиотекой setuptools, ко
торая позволяет автоматически загружать, собирать, устанавливать
и управлять пакетами языка Python».  Пакеты носят название «eggs» и имеют расширение .egg. Как правило, эти пакеты распространяются в формате архива ZIP.


easy_install  - это программа (модуль написанный на python)  связанный с библиотекой setuptools для установки пакетов, загрузки, создания, управления. Это часть setuptools, те  easy_install только часть глыбы под названием setuptools

А правильный способ - это указать setuptools ставить eggs в отдельный каталог. И я бы советовал не использовать для этого дела /usr/local/lib/python2.4/site-packages по простой причине - держать яйца в разных корзинах.
Я предлагаю такой подход: в конфиге указываем опции для eggs и ставим их просто easy_install NeededPackage, а для установки "руками" используем опцию --prefix. 
[http://pyobject.ru/blog/2006/12/21/cooking-python-eggs/](http://pyobject.ru/blog/2006/12/21/cooking-python-eggs/)

PyPI - это репозиторий пакетов для питона с расширение .egg




pip это замена для easy_install
Pip это альтернатива easy_install
PIP не использует eggs, но можно ставить проги из git
Вот тут pip выступает как противоположность, говоря - я сборкой пакетов не занимаюсь, а только их ставлю.




        Buildout 
Buildout — средство автоматизации сборки для программного обеспечения с открытым исходным кодом, написанное на Python. 
    С его помощью можно собирать пакеты написанные не только на python, а также устанавливать их.

Этот вопрос сложнее. Я к примеру использую python buildout

А я вот, в последнее время, съехал с pip на buildout. По крайней мере, когда нужно что-то более сложное, нежели просто установка одного-двух пакетиков для "поиграться".

Кроме того, buildout позволяет наследовать конфиги, что оказывается очень удобно: есть базовый конфиг, где описано общее окружение, и есть, скажем, конфиги для тестинга и разработки, которые что-то переопределяют. Например докидывают пакетиков типа ipython или django-debug-toolbar.

Все три своих сайта сейчас именно так раскладываю в продакшн.






            Virtualenv
virtualenv –это инструмент создания изолированной среды Python». Основная задача, которую решает virtualenv, состоит в устранении конфликтов
между пакетами. Часто один инструмент требует одну версию некоторого пакета, а другой инструмент – другую версию того же пакета.

virtualenv - генератор вирутальных сред для python
      создаём свою среду, помещаем нужные модули, разрабатываем свои, если надо,то можем разместить в другое место и т д
virtualenv {наствание папки}


Следует заметить, что оба инструмента, Buildout и virtualenv,
очень широко используют библиотеку setuptools, сопровождением ко
торой в настоящее время занимается Филлип Дж. Эби (Phillip J. Eby).



distutils
    |                      
 setuptools         
    I
easy_install





 Distribute был создан как замена Setuptools
 Проект Distribute, который развивался как форк setuptools, официально больше не поддерживается, его код слит обратно с setuptools. Теперь остались только setuptools и pip. Distutils2 тоже загнулся.
 Получается надо использовать Distribute (средство создание пакетов с модулями)  и Pip - программа для установки пакетов
 
 
 
 Разработчики Python отдают предпочтение PIP
 [https://www.python.org/dev/peps/pep-0453/](https://www.python.org/dev/peps/pep-0453/)
 
 
 virtualenv + pip это **не** система дистрибуции софта. Это способ разработки. На выходе все равно должен получиться .tar.gz с кучей *.wheel-ов или нечто другое инсталлябельное.

А если так, то разрабатываться можно так как удобно — никто тут ничего не навязывает. Тот же кто использует virtualenv+pip для обновления продакшна — дурак и всё. 
 
 
 zypper install python-virtualenv
 
 
 
 
 
 [http://python-lab.blogspot.com.tr/2012/07/python-201-distutils.html](http://python-lab.blogspot.com.tr/2012/07/python-201-distutils.html)
 [http://habrahabr.ru/post/112332/](http://habrahabr.ru/post/112332/)
 [http://www.stableit.ru/2011/12/pip-easyinstall.html](http://www.stableit.ru/2011/12/pip-easyinstall.html)
 [http://webnewage.org/2009/06/23/what-is-pip/](http://webnewage.org/2009/06/23/what-is-pip/)
 [http://pythonworld.ru/osnovy/pip.html](http://pythonworld.ru/osnovy/pip.html)
 
 virtualenv
 [http://proft.me/2010/04/3/python-i-okruzhenie-virtualenv/](http://proft.me/2010/04/3/python-i-okruzhenie-virtualenv/)
 [https://virtualenv.pypa.io/en/latest/installation.html](https://virtualenv.pypa.io/en/latest/installation.html)
 [http://adw0rd.com/2012/6/19/python-virtualenv/](http://adw0rd.com/2012/6/19/python-virtualenv/)
 [http://www.unix-lab.org/posts/virtualenv/](http://www.unix-lab.org/posts/virtualenv/)
 [https://virtualenv.pypa.io/en/latest/](https://virtualenv.pypa.io/en/latest/)


 virtualenv + python
 [http://stackoverflow.com/questions/23842713/using-python-3-in-virtualenv3](http://stackoverflow.com/questions/23842713/using-python-3-in-virtualenv3)
 
 PEP8
[http://pep8.ru/doc/pep8/](http://pep8.ru/doc/pep8/)



 Установка pip
 yum install python-pip

 python-virtualenv тоже нужно установить из пакета
 
$ source ~/venv/<venv_name>/bin/activate
Для окончания работы с окружением (например для переключение на системный python) следует выполнить в командной строке:
$ deactivate

Для 3 версии python
 virtualenv -p python3 env3
 source /home/garry/env3/bin/activate

virtualenv -p /usr/bin/python2.7 --no-site-packages ~/.virtualenvs/env2.7
 source .virtualenvs/env2.7/bin/activate
 pip install django==1.4
 python

>>> Python 2.7.3
>>> import django
>>> django.VERSION
>>> (1, 4, 0, 'final', 0)

pip uninstall django==1.4

Чтобы выйти из виртуального окружения введите команду $ deactivate.




--no-site-packages

    Запретить использование системного site-packages (для полной изоляции вашего окружения от системы). Например у вас в системе установлена "Django 1.3", если вы будете использовать эту опцию, то в созданном окружении эта "Django" не будет доступна.
    В текущих версиях virtualenv эта опция используется по умолчанию, можете её не указывать.

--system-site-packages

    Эта опция противоположна предыдущей, то есть заставляет окружение использовать установленные в системе пакеты, если не нашлись онные в окружении.

О virtualenvwrapper

В иных руководствах рекомендуется использовать вдовесок virtualenvwrapper, призванный упростить работу с самим virtualenv. Думается, он не особенно нужен, ибо единственной вещью, которую делать лениво представляется переключение между виртуальными окружениями: слишком длинную команду приходится вводить для такого простого действия. Но это можно легко поправить, добавив в ваш .bashrc или .zshrc несколько псевдонимов для окружений, например так:

alias env3='source ~/.virtualenvs/env3.2/bin/activate'
alias env2='source ~/.virtualenvs/env2.7/bin/activate'
alias blog='source ~/.virtualenvs/blog/bin/activate'

Теперь смена окружения будет выглядеть немного иначе:

    $ evn2 – вошли в окружение, работаем работу
    $ deactivate – деактивируем окружение
    $ env3 – входим в другое окружение

При использовании virtualenvwrapper:

    $ mkvirtualenv myapp – создаст новое окружение myapp
    $ workon myapp – переключиться на myapp
    $ deactivate – деактивировать
    $ rmvirtualenv myapp – удалить
    
    
    
    
[http://3bep.blogspot.ru/2010/11/virtualevn-virtualenvwrapper-and-pip.html](http://3bep.blogspot.ru/2010/11/virtualevn-virtualenvwrapper-and-pip.html)

Для еще большего комфорта при работе с virtualenv Doug Hellmann написал расширение virtualenvwrapper, которое делает все манипуляции с окружениям еще проще.
Ставим virtualenvwrapper
sudo easy_install virtualenvwrapper
Создаем папку, где будут лежать все окружения
mkdir ~/.virtualenvs
Добавляем в файл ~/.bashrc следующие содержание

export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh

Приминяем изменения:
source ~/.bashrc
Создаем новое окружение:
mkvirtualenv blog
Активируем:
workon blog
Деактивируем
deactivate
Удаляем
rmvirtualenv blog

    
    
Список зависимостей проекта, насколько я смог разобраться, принято сохранять в файл с именем requirements.txt:
pip3 freeze > requirements.txt

Этот подход позволяет одной командой установить все зависимости, необходимые проекту:
pip3 install -r requirements.txt
    
    
    
    
    
    
    
    django-admin startproject djangolocalhost
    создаст в текущей папке проект djangolocalhost
    
    
    
    
    djangogirls
├───manage.py
└───mysite
        settings.py
        urls.py
        wsgi.py
        __init__.py

    
    
    
    
    
    /home/web/*YOUR_PROJECT*/
├── env
├── files
│   ├── media
│   └── static
├── logs
├── manage.py
└── src
    ├── YOUR_APPS
    ├── local_settings.py
    ├── settings.py
    ├── static
    ├── templates
    └── urls.py

  /data                     # Общий каталог для проектов на сервере
-------- mysite           # Каталог для сайта mysite
-------- -------- conf    # Конфигурационные файлы для веб-сервера
-------- -------- project # Код проекта
-------- -------- venv    # Каталог для виртуального окружен  
    
    
    
    [https://habrahabr.ru/post/165081/](https://habrahabr.ru/post/165081/)
[http://djbook.ru/forum/topic/525/](http://djbook.ru/forum/topic/525/)
[http://pyobject.ru/blog/2006/09/11/django-code-layout/](http://pyobject.ru/blog/2006/09/11/django-code-layout/)
[https://it4it.ru/2014/12/03/django-recommended-layout/](https://it4it.ru/2014/12/03/django-recommended-layout/)

[https://habrahabr.ru/post/206024/](https://habrahabr.ru/post/206024/)
[http://pyobject.ru/blog/2006/09/11/django-code-layout/](http://pyobject.ru/blog/2006/09/11/django-code-layout/)
[http://djbook.ru/forum/topic/629/](http://djbook.ru/forum/topic/629/)
[http://djbook.ru/forum/topic/3797/](http://djbook.ru/forum/topic/3797/)
[https://bevice.ru/posts/1080.html](https://bevice.ru/posts/1080.html)

Здесь описано
[https://docs.djangoproject.com/en/1.8/intro/tutorial01/](https://docs.djangoproject.com/en/1.8/intro/tutorial01/)
    
    
    /home/ufadormash.ru/djcode/project - здесь сам проект
/home/ufadormash.ru/djcode/logs - здесь логи nginx, uwsgi, etc
/home/ufadormash.ru/djcode/etc - здесь конфиги
/home/ufadormash.ru/djcode/var - здесь pidы и, например, кеш сфинкса

2) В виртуальное окружение можно ставить пакеты, относящиеся непосредственно к проекту (Django, батарейки и тд), на системном уровне - к серверу.

3) Есть смысл создавать виртуальное окружение под каждый проект, тогда вы легко сможете держать целый зоопарк пакетов на одном сервере.

4) С правами в целом все тривиально, nginx-у нужны доступы только к статике - это папки media и static, uWSGI должен запускаться от того же пользователя, кто владеет проектом посмотрите здесь пост достаточно старый, но смысл не изменился. Supervisor нужен для того, чтобы удобно было управлять процессами uWSGI





























Внутри requirements.txt так же можно инклудить другие файлы: -r file.txt

•
Ответить
•
Поделиться ›

Аватар
Eugene Agafonov • 3 months ago

Ещё полезно знать про pip freeze: команда выкидывает cписок установленных в песочнице пакетов с указанием точных версий конкретными версиями.

Если сохранить выхлоп в requirements-файл и закоммитить в SCM, то очень легко получается повторяемость сборок на машинах разработчиков, СI/CD и боевых серверах.

Грубо последовательность действий получается такакя

На этапе разаработки:

# Ставим "сырые" зависимости
pip install -r requirements-dev.txt

# Hack/debug/test/profit

# сохраняем зависимости
pip freeze > requirements-freezed.txt
git add requirements-freezed.txt && git commit -m "Update freezed deps"

# На СI/боевом сервере
pip install -r requirements-freezed.txt

Всё это автоматизируется за пару часов с перерывами на кофе. Важно периодически обновлять requirements-freezed.txt в SCM и прогонять тесты. В идеале - два прогона тестов в CI - c зависимостями из requirements-freezed.txt и после pip install -U -r requirements-dev.txt

1
•
Ответить
•
Поделиться ›

    Аватар
    semen4ik20 Eugene Agafonov • 2 months ago

    freeze получается жеско фиксирует версию зависимости?
    •
    Ответить
    •
    Поделиться ›

    Аватар
    Eugene Agafonov semen4ik20 • 2 months ago

    да, выхлоп полностью совместим с форматом файла requirements.txt

    Собственно, под версионным контролем лежит два файла:

    - requirements-dev.txt - зависимости без указания версий
    - requirements.txt - зависимости c версиями, на которых
    гарантированно проходят тесты и которые готовы к разворачиканию на боевые сервера.

    По-умолчанию, на боевые сервера разворачивается requirements.txt с указанием версий, что гарантирует повторяемость установки. В CI есть задача которая самые последние версии из requirements-dev.txt и запускает тесты. Если обновление зависимостей на последние версии ломают тесты, то воют сирены и машутся флаги.

    Буквально вчера эта схема съэкономила много нервов, когда выснилось, что pysft- 0.2.9 "сломали" ([https://bitbucket.org/dundeemt...](https://bitbucket.org/dundeemt...), а в зависимостях для продакшена была неполоманая 0.2.8


    
    
    Установка pip3 на centos7
     wget [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)
--2016-09-27 16:26:31--  [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)
Распознаётся bootstrap.pypa.io (bootstrap.pypa.io)... 151.101.84.175
Подключение к bootstrap.pypa.io (bootstrap.pypa.io)|151.101.84.175|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа... 200 OK
Длина: 1524722 (1,5M) [text/x-python]
Сохранение в: «get-pip.py»

100%[==============================================================================================================================================>] 1 524 722   5,54MB/s   за 0,3s   

2016-09-27 16:26:31 (5,54 MB/s) - «get-pip.py» сохранён [1524722/1524722]

[root@centos7py garry]# ls
get-pip.py  ifcfg-ens3.11
[root@centos7py garry]# python3.4 get-pip.py 
Collecting pip
  Using cached pip-8.1.2-py2.py3-none-any.whl
Collecting wheel
  Downloading wheel-0.29.0-py2.py3-none-any.whl (66kB)
    100% |████████████████████████████████| 71kB 998kB/s 
Installing collected packages: pip, wheel
Successfully installed pip-8.1.2 wheel-0.29.0
[root@centos7py garry]# pip3
