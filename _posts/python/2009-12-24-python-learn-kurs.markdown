---
layout: post
title:  "python-learn-kurs"
date:   2009-12-24 00:39:30 +0300
categories: python
tags: python
---

# python-learn-kurs

Первый блок. Занятия 1-7.
Занятие 1: Введение

Результат занятия: настроенная среда, библиотека с основами синтаксиса и типов данных, на которые можно опереться в дальнейшем.

    Общее знакомство с `Python`, его историей и перспективами
    Общее знакомство с версиями `Python` 2.7 и 3
    Настройка и установка `Python` 2.7 и 3 на локальные машины
    Установка `SublimeText`(Text Editor)
    Настройка и установка `git`, регистрация на github
    `print 'Hello Pythonic world!'`, первый commit и push на github
    Детальный разбор, что же произошло в пункте выше
    Знакомство с базовым синтаксисом, базовые типы данных
    Что такое переменная? Как ее объявить, и где ее видно?
    Знакомство со структурами языка: ветвления, циклы, условия
    Stackoverflow-driven development, секция о том, как самому найти ответы на свои вопросы

Занятие 2:

Результат занятия: приложение-игра, "крестики-нолики" в консоли.

    Знакомство с командной строкой
    Управление зависимостями, `pip`, установка первых внешних пакетов
    Знакомство с `virtualenv`, создание среды
    Установка `PyCharm`(IDE)
    Продолжение знакомства с типами данных в `Python`, принцип "присваивание никогда не копирует данные": массивы, словари, кортежи
    Что такое Функция? Введение в функциональное программирование
    Обработка исплючений
    Дебаг приложения
    Написание игры "крестики-нолики" в функциональном стиле

Занятие 3: ООП

Результат занятия: приложение "список дел и покупок".

    Что такое Объект? Знакомство с ООП
    Принципы ООП: абстракция, наследование, инкапсуляция, полиморфизм
    Волшебные методы и константы: `__init__()`, `__str__()` и `__dict__`
    `Python`'s `super()`, `mro()`, новые и старые классы
    `@staticmethod` и `@classmethod`, переменные класса
    Принципы проектирования: наследование, агрегация и композиция
    Продолжение знакомства с языком `Python`: декораторы, свойства, генераторы, `lambda`, `list-comprehension`
    Zen of Python
    Написание приложения "список дел и покупок" в объектном стиле

Занятие 4: Версии Python, межверсионный код

Результат занятия: ?

    В чем основные отличия `Python` 2 и 3?
    `str` и `unicode`
    Другие важные изменения
    Какую версию интерпретатора выбрать для нового проекта?
    Как писать код под обе версии `Python`? Знакомство с `six`, `2to3`, `3to2`
    Наступившее будущее: что нового в `Python` 3.5?
    Могу ли я улучшить `Python`? Или что такое `PEP`
    Написать ?

Занятие 5: Усложнение программ

Результат занятия: приложение-игра "морской бой" с ИИ.

    Принципы разработки ПО: DRY, KISS, YAGNI, SOLID
    Частые ошибки при написании кода
    Работа с файлами
    Текстовые форматы обмена данными: `.json`, `.csv`, и как с ними работать
    Какие есть способы завершить приложение?
    Написания игры "морской бой" с ИИ с сохранением игры, в объектном стиле

Занятие 6: Создание веб-паука

Результат занятия: приложение, которое бы заходило на страницу соц.сети и забирало оттуда все статусы и/или фотографии.

    Как устроен интернет? Знакомство с `TCP/IP`, `DNS` и клиент-серверной архитектурой
    Зачем нам `http` перед адресом? Знакомство с протоколом `HTTP` с модулем `urllib`
    Что такое регулярное выражение? Модуль `re`
    Что такое веб-страница? Основы `HTML` разметки, знакомство с `HTML5` тегами
    Написание веб-паука на основе `Scrapy`, который будет получать статусы со страницы соц.сети и сохранять результаты в файле

Занятие 7: Первый web-проект, backend

Результат занятия: приложение-блог без базы данных, без стилей и скриптов

    Что такое backend и frontend?
    Как работает сервер на примере `Flask`?
    Какой путь проходит запрос, и какие бывают запросы?
    Введение в `MVC` и `MTV`
    Как происходит роутинг?
    Что такое шаблон? И как работать с `Jinja2`?
    Зачем нужны формы, и как с ними работать?
    Написание первого web-приложения




Второй блок. Занятия 8-14.
Занятие 8: Основы баз данных

Результат занятия: приложение блог с базой данных и кешем, постраничным выводом статей, без стилей и скриптов.

    Какие бывают базы данных? Знакомство с `MySQL`, `PostgresSQL`, `SQLite` и `Redis`
    Основы РСУБД: таблицы и связи между ними (OneToOne, OneToMany, ManyToMany)
    Введение в `SQL`
    Проектирование баз данных, нормальные формы
    Транзакции, индексы
    Введение в `NoSQL`: `key-value` хранилище, установка `Redis`
    Введение в `ORM` на примере `SQLAlchemy` (для `SQLite`) и `redis-py`
    Написание моделей для блога, создание кеша в `Redis`, добавление постраничного вида

Занятие 9: Первый web-проект, frontend: CSS

Результат занятия: приложение блог, с css стилями

    Что такое `CSS`? Как работают селекторы?
    Классы, id, теги
    Зачем веб-страницам нужна сетка?
    Что такое адапативный дизайн? Знакомство с `media-query`
    Что такое `fallback`?
    Подходы к написанию `CSS`: mobile-first и наоборот
    Прогрессивное улучшение
    Методологии написания `CSS`: `bem` и другие
    Что такое компонент? И что такое `styleguide`?
    Установка `node.js`, `npm` и `bower`
    Почему так часто используют `Twitter Bootstrap`? Знакомство с библиотекой
    Написание стилей для своего блога

Занятие 10: Введение в JS

Результат занятия: небольшой проект на JS

    В чем схожести и отличия `javascript` от `Python`?
    Какой бывает `javascript`?
    Типы данных
    Структуры языка
    Область видимости переменных
    Функции, и что такое `this`?
    Объекты `window` и `document`
    Что такое `polyfill`?
    Как дебажить `js` приложение?
    Написание своего небольшого frontend-проекта

Занятие 11: Первый web-проект, frontend: jQuery

Результат занятия: предварительный frontend для своего приложения

    Что такое библиотека `jQuery`?
    Когда она нужна, когда без нее можно обойтись, а когда она нежелательна?
    Методологии огранизации кода или "Как варить лапшу"
    Событийная модель браузера
    Знакомство с `$.ajax()` и `CORS`
    Манипуляции с `DOM`
    Улучшение производительности кода
    Написание frontend для своего проекта

Занятие 12: Автоматизация рутинных задач с Grunt

Результаты занятий: готовый frontend для своего приложения

    Зачем нужна автоматизация задач?
    В чем разница между ``
    Улучшение `CSS` с `autoprefixer`
    Знакомство с `PostCSS` и два слова о препроцессорах
    Уменьшение размера текстовых файлов и картинок
    Модульная система для `js` на примере `browserify`
    Моментальное изменение страницы с `liveserver`
    Зачем нужна система версий для статических файлов?
    Создание `Gruntfile.js`, первый build frontend'а

Занятие 13: Django

Результат занятия: написан скелет будущего приложения Django

    Что такое `Django`? И как работает данный фреймворк?
    Какой путь проходит запрос в жизненном цикле приложения?
    Знакомство с Middleware
    url-routing, `include()` и `reverse()`
    `Django`'s MVT, знакомство с `Django-Templates`
    `views` и `class-based views`
    Простые формы, валидация форм
    Статические файлы
    Организация настроек приложения
    Написание скелета будущего проекта

Занятие 14: Django ORM

Результат занятия: написание моделей к приложению

    Знакомство с моделями
    Установка и настройка `PostgreSQL`
    Отношения моделей между собой: `OneToOne`, `ManyToMany` и `ForeingKey`
    Как написать запрос?
    Как написать сложный запрос? `annotate()`, `aggregate()`
    Сигналы
    Миграции, обзор исторического `South` и текущего `Django-Migrations`
    Написание моделей к приложению


Занятие 15: Работа с моделями в Django

Результат занятия: доработка моделей, оптимизация и отладка

    Как сделать сложный запрос проще? `select_related()`, `values()`
    Следим за запросами с помощью `django-debug-toolbar`
    Создание и валидация `ModelForm`
    Работа в `FileField` и `ImageField`, сохранение пользовательских медиа файлов
    Наследование моделей, абстрактные модели и миксины
    Менеджеры
    `raw queries`: плюсы и минусы
    Доработка своего приложения

Занятие 16: Администрирование Django приложения

Результат занятия: написанная админская часть приложения

    Как устроена админская панель?
    Как администрировать приложение?
    Авторизация пользователей, группы и права доступа
    Создание собственных `admin-view`
    Знакомство с `django-admin-tools`
    `Django Management Commands`, создание своих комманд
    Как правильно вести логи?

Занятие 17: Тестирование Python приложения

Результат занятия: законченное приложение блог с базой данных, дизайном и с тестами.

    Что такое тест, и зачем тестировать приложение?
    Какие бывают тесты? В чем разница между unit-тестыми и интеграционными тестами?
    Модуль `unittest` в `Python`
    Что такое "изоляция"? Знакомство с модулем `mock`
    Тесты для нескольких версий `Python` с `tox`
    Интеграционные тесты с `selenium`
    Сколько кода покрыто тестами? Введение в `coverage`
    Написание тестов к своему проекту, достижение покрытия в 70-80%

Занятие 18: Тестирование Javascript приложения

Результат занятия: напиание тестов для своего приложения

    Почему у `js` так много фреймфорков для тестирования?
    Тестировани при помощи `mocha`, `Chai` и `Sinon`
    Изоляция: моки, шпионы и удары в спину
    Тестирование картинками, или как работает `gemini`
    Как запустить все тесты сразу? Знакомство с `polytester`
    Автотесты локально на примере `Grunt` и удаленно на примере Travis CI

Занятие 19: Введение в TDD и BDD

Результат занятия: написание модуля в TDD стиле, создание BDD тестов

    Что такое `Test Driven Development`?
    Плюсы и минусы такого похода
    Тестирование `Django` приложения при помощи `LiveServerTestCase` и `StaticLiveServerTestCase`
    Почему TDD и BDD часто сравнивают?
    Как описать поведение приложения? Введение в псевдо-язык `gherkin`
    Сравнение BDD фреймворков для `Python`
    Запуск BDD тестов
    Когда такие подходы нужны, применимы и потивопоказаны? И когда писать какие тесты?

Занятие 20: Celery

Результат занятия: написание асинхронных задач для своего проекта

    Настройка и установка `Celery with Redis`
    Знакомство с асинхронными задачами
    Периодичные задания с `Celery Beat`
    Конроль выполнения задач с `Celerycam`
    Мониторинг `Redis`
    Как дебажить `Celery`?
    Написание асинхронных задач

Занятие 21: Полезности для Django разработчика

Результат занятия:

    Краткое знакомство с популярными библиотеками
    `python-social-auth`
    `django-rest-framework`
    `django-cms`
    `Elasticsearch`
    `Sentry` и `Raven` (+ `raven.js`)


Занятие 22: Безопасность

Результат занятия: скрипты для XSS атаки, добавление дополнительных настроек безопасности в проект

    Какие бывают атаки?
    Какие средства предлагает `Django`, чтобы избежать потенциальных атак?
    Content Security Policy
    Пишем свой XSS
    Протокол HTTPS
    Аудит сайта на безопасность

Занятие 23: Документация

Результат занятия: Документирование своих приложений, генерация документации

    Как документировать `Python` приложение?
    Умные `doc-string`, знакомство со `Sphinx`
    Тесты в документации
    Как документировать `CSS` и зачем? Знакомство с `KSS`
    Создаем свой `styleguide` в два клика
    Документривание `js`
    Генерация документации по проектам

Занятие 24: Математика в Python

Результат занятия:

    Что такое `anaconda`?
    Фреймворк `Pandas`
    Знакомство с `numpy`
    `iPython Notebook`
    `matplotlib`

Занятие 25: Деплой на UNIX сервер

Результат занятия: деплой своего приложения на сервер, создание шаблонов конфигураций

    Отличия боевого сервера от сервера разработки
    Создание окружения
    `gunicorn` vs `uwsgi`
    Создание сервисов в `supervisor`
    Установка и конфигурация `nginx`
    Установка дополнительных сервисов
    Установка `pydevd` и удаленный дебаг

Занятие 26: Приложение в реальной жизни

Результат занятия:

    Что делать, когда все пойдет не так
    Как поддерживать свое приложение?
    Как поддерживать чужое приложение?
    Метрики (CTR, конверсия), AB-тестирование
    Куда расти и что делать?
