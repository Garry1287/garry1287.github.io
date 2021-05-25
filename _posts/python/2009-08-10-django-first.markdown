---
layout: post
title:  "django-first"
date:   2009-08-10 01:43:06 +0400
categories: python
tags: python
---

# django-first


[https://github.com/dyve/django-bootstrap3](https://github.com/dyve/django-bootstrap3)
[http://django-bootstrap3.readthedocs.io/en/latest/templatetags.html#bootstrap-jquery-url](http://django-bootstrap3.readthedocs.io/en/latest/templatetags.html#bootstrap-jquery-url)


Работа с шаблонами
[http://knigun.com/post/architecture-for-django-templates/](http://knigun.com/post/architecture-for-django-templates/)
[http://www.vr-online.ru/blog/django-chast-7-sovershenstvuem-shablony-9191](http://www.vr-online.ru/blog/django-chast-7-sovershenstvuem-shablony-9191)


Разработка интернет магазина
[https://www.youtube.com/watch?v=2epT35eA0dE](https://www.youtube.com/watch?v=2epT35eA0dE)

Танго и django
[http://tango.pythoff.com/](http://tango.pythoff.com/)
[https://leanpub.com/tangowithdjango19](https://leanpub.com/tangowithdjango19)


[http://www.intuit.ru/studies/courses/3586/828/lecture/28997](http://www.intuit.ru/studies/courses/3586/828/lecture/28997)
[http://djbook.ru/rel1.9/](http://djbook.ru/rel1.9/)
[https://habrahabr.ru/post/234307/](https://habrahabr.ru/post/234307/)
[https://blog.udemy.com/django-tutorial-getting-started-with-django/#looking_better](https://blog.udemy.com/django-tutorial-getting-started-with-django/#looking_better)
[http://agiliq.com/books/djenofdjango/](http://agiliq.com/books/djenofdjango/)

Всякая фигня
[https://www.youtube.com/channel/UClSYlwlCbXiw_BmmsKi4HFw](https://www.youtube.com/channel/UClSYlwlCbXiw_BmmsKi4HFw)


Код сайта
[https://github.com/djbook-ru/djbookru](https://github.com/djbook-ru/djbookru)

Учебник
[http://www.djangobook.com/en/2.0/](http://www.djangobook.com/en/2.0/)
[http://www.effectivedjango.com/tutorial/](http://www.effectivedjango.com/tutorial/)



    “Чем дальше в лес, тем больше дров”

На написание данного поста подтолкнула статья 10 Django Trouble Spots for Beginners. Это вольный перевод этого материала с множеством “отсебятины” показавшейся мне важной при изучении django. Естественно проблем при изучении джанго всплывает гораздо больше чем 10 :-). Описанные проблемы в основном возникают на самых ранних этапах обучения и, особенно при переходе c PHP.

1. Django это не CMS. Он не умеет из коробки делать то, что делають Wordpress, ModX и другие CMS, но на django можно сделать куда более сложные приложения за кратчайшие сроки. У Django очень функциональная админка, но настройка и разработка на джанго это не совсем так просто как пишут все гораздо сложнее, чем в CMS, потому что это НЕ CMS.

2. У начинающих возникает много проблем с первоначальной настройкой среды разработки на локальном компьютере. Какую IDE выбрать, какие модули python ставить и как это делается, а если учесть что большинство разработчиков мигрируют c PHP и никогда не программировали на python, то это вызывает немало трудностей. И тут не поможет NIMP и Денвер :-). Попробуйте для разработки использовать PyCharm, это великолепная IDE сэкономит вам кучу времени и нервов.

3. Если вы новичок в Django, то наверняка вас ставили в тупик терминология “проекты” и “приложения”, куда что “совать” и зачем так все запутывать. Конечно же, в итоге все становится на свои места и вы понимаете что проект - это только просто набор (обёртка) для приложений, которых он может содержать великое множество. Думаю, будет корректно сравнить термин “приложение” с гораздо более понятным для большинства термином “плагин/модуль” как в обычных CMS. В отличие от модулей обычных движков в большинстве случаев джанго приложения выполняют только 1-2 функции и могут быть с лёгкостью портированы в другие ваши проекты на django. Например, вы строите клон YouTube для этого необходимо создать проект, “MyTube”, который будет содержать приложения, такие как “видео”, “комментарии”, “рейтинги”, “блог”, и т.д.

4.Наследование шаблонов. Наследование шаблонов одна из приятных плюшек в django, но у вас уйдет немало времени, что бы понять это. Если сравнивать с движками(CMS), то мне показалось что идея django шаблонов в некоторых моментах наиболее близка к системе шаблонизации в ModX(чанки, фильтры, простейшая логика на phx очень напомнили base.html, {% block %}, фильтры, {% if %}, {% else %} и т.д. в джанго) думаю, кто знаком с ModX и Django меня поддержат. Для тех же, кто работал с другими движками, возможно, возникнет небольшая трудность с пониманием джанго шаблонов.
Для начала создаётся основной шаблон base.html, их может быть несколько для разного функционала сайта, в нем делает блоки header, content, footer …..
<div>
{% block content %}
<p>Если в дочерних шаблонах это блок будет использоваться, то текст здесь перезапишиться</p>
{% endblock %}
<p>Этот же текст будет виден на всех станицах сайта без разницы, какие блоки используются</p>
</div>

В дочернем шаблоне подключаем основной шаблон, и блок content.
{% extends base.html %}

{% block content %}
Этим текстом мы перезапишем текст в блоке content основного шаблона!
{% endblock %}

5. Разделение кода от медиа файлов (фото, js, css ….), это необходимость. Django сам по себе не предназначен для отдачи статики, на продакшен серверах этим занимаются вэб серверы nginx, apache и поэтому важно, что бы вся статика хранилась в одном месте (обычно это папка media в корне проекта). Вот самая обычная структура джанго проекта:
MyProject
- app
- app2
- media
- javascript
- stylesheets
- images
- ……….
….
для разработки можно использовать исключительно django, а отдачу статики можно организовать, написав в urls.py

from django.conf import settings
if settings.DEBUG:
urlpatterns += patterns(”,
(r’^robots.txt$’, ‘django.views.static.serve’, {’document_root’: settings.MEDIA_ROOT, ‘path’: “robots.txt”}),
(r’^favicon.ico$’, ‘django.views.static.serve’, {’document_root’: settings.MEDIA_ROOT, ‘path’: “favicon.ico”}),
(r’^media/(?P<path>.*)$’, ‘django.views.static.serve’, {’document_root’: settings.MEDIA_ROOT}),
)

в шаблоне к статическим файлам обращаемся, например так
<img src=”/media/{{ images }}” width=”200″ height=”300″ alt=”">

6. Работа с БД. Так как встроенная в django команда syncdb умеет только вносить информацию из моделей в базу данных. Возникает вопрос, как добавлять или удалять полей в уже существующие модели. Тут на помощь придёт South. Умеет:
– отслеживание изменений в модели и создание миграций
– независимость от движков БД (заявлена поддержка 5 разных типов БД)
– создание миграций только для выбранного приложения (application)
– сообщение о возможных конфликтах при комите миграций от других разработчиков

7. Несколько блоков на странице. Поначалу очень сложно понять как же вывести разную информацию на одной странице(допустим верхнее меню, sidebar с облаком тегов и в footer последние комментарии). По логике кажется, что для каждого блока надо делать свою функцию/представление во views.py, но в urls.py нельзя добавить больше одного представления, что же делать?? Эта мысль будоражит мозги начинающих джангистов. Оказывается надо дочитать документацию до конца и там чёрным по белому написано, что для вывода дополнительных блоков надо использовать Template Tags. Вот прекрасный пример кода

8. Аутентификации пользователей. Для аутентификации пользователей лучше всего использовать сторонние библиотеки, например django-registration.

9. Установка приложений сторонних разработчиков. Часто при установке “чужих” приложений в консоль валится куча ошибок, в большинстве случаев они указывают на отсутствие нужных модулей python для данного приложения. Единственный способ корректно установить приложение это прочитать его документацию и обратить внимание на требуемые модули питона. Установка модулей происходит через pip или устаревший easy_install.

10. И самая популярная проблема это
- Аааааааааааааааааааааааа, я них……на не понял в этом django, вернусь обратно к PHP, Wordpress.
Уважаемые начинающие джангисты, читайте внимательно документацию спрашивайте на форумах, django комюнити очень лояльное к новичкам.

Удачной вам разработки.



1. cat urls.py  - шаблон url
urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
    url(r'^blog/', include('blog.urls')),
]


2. /djsite/mysite/blog> cat urls.py
app_name = 'blog'                                                                                                                                                                       
                                                                                                                                                                                        
urlpatterns = [                                                                                                                                                                         
    url(r'^$', PostsListView.as_view(), name='list'), # то есть по URL http://имя_сайта/blog/ 
                                               # будет выводиться список постов
    url(r'^(?P<pk>\d+)/$', PostDetailView.as_view()), # а по URL http://имя_сайта/blog/число/ 
                                              # будет выводиться пост с определенным номером
]


3. view
garry@garry:~/djsite/mysite/blog> cat views.py 
from django.shortcuts import render

# Create your views here.
from blog.models import Post 
from django.views.generic import ListView, DetailView

class PostsListView(ListView): # представление в виде списка
    model = Post                   # модель для представления 

class PostDetailView(DetailView): # детализированное представление модели
    model = Post

Мы используем здесь два общих представления: ListView и DetailView. Эти два типа представлений отображают две концепции: “отображение списка объектов” и “отображение подробностей о конкретном объекте”.


4.
cat models.py 
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=255) # заголовок поста
    datetime = models.DateTimeField(u'Дата публикации') # дата публикации
    content = models.TextField(max_length=10000) # текст поста

    def __unicode__(self):
        return self.title

    def get_absolute_url(self):
        return "/blog/%i/" % self.id

        
В шаблонах переменная выводится с помощью {{ posts }}
{% endfor %} - это встроенный язык шабонов


Ты заметила, что мы использовали немного другую запись в этот раз {{ post.title }} или {{ post.text }}? Мы обращаемся к различным полям нашей модели Post. Также |linebreaksbr прогоняет текст через фильтр, для преобразования переносов строк в параграфы.
    


Как с помощью tag выводит информацию в django




