---
layout: post
title:  "django-static"
date:   2013-01-13 15:38:39 +0400
categories: python
tags: python
---

# django-static

Статика в одном месте

Перед запуском nginx поместим всю статику в папку static. Для этого добавляем в файл mysite/settings.py следующую строку:

STATIC_ROOT = os.path.join(BASE_DIR, "static/")


И выполняем команду:

python manage.py collectstatic

Получаем папку static в корне

Static django python

# Static files (CSS, JavaScript, Images)
# [https://docs.djangoproject.com/en/1.10/howto/static-files/](https://docs.djangoproject.com/en/1.10/howto/static-files/)

STATIC_URL = '/static/'

STATIC_ROOT = os.path.join(BASE_DIR, "static/")

#STATICFILES_DIRS = [
#    os.path.join(BASE_DIR, "static"),
#]
