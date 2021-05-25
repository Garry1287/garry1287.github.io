---
layout: post
title:  "python_selenium"
date:   2012-11-29 19:45:52 +0400
categories: python
tags: python
---

# python_selenium


from selenium.webdriver.firefox.firefox_binary import FirefoxBinary
from selenium import webdriver
binary = FirefoxBinary('/path/to/firefox46.0.1') # from [https://ftp.mozilla.org/pub/firefox/releases/46.0.1/](https://ftp.mozilla.org/pub/firefox/releases/46.0.1/)
d = webdriver.Firefox(firefox_binary=binary)



If you are using Firefox 48+ you need to use GeckoDriver:
[https://github.com/mozilla/geckodriver](https://github.com/mozilla/geckodriver)

driver = webdriver.Firefox(capabilities={"marionette":False})



[http://www.autotest.org.ua/first-autotest-with-selenium-webdriver-and-python/](http://www.autotest.org.ua/first-autotest-with-selenium-webdriver-and-python/)
[http://python-3.ru/page/selenium-python-examplehttp://python-3.ru/page/selenium-python-example](http://python-3.ru/page/selenium-python-examplehttp://python-3.ru/page/selenium-python-example)
[https://habrahabr.ru/post/250921/](https://habrahabr.ru/post/250921/)
[https://github.com/seleniumhq/selenium/issues/2739](https://github.com/seleniumhq/selenium/issues/2739)
[https://stackoverflow.com/questions/40073548/python-selenium-in-ubuntu-oserror-errno-20-not-a-directory/40399367#40399367](https://stackoverflow.com/questions/40073548/python-selenium-in-ubuntu-oserror-errno-20-not-a-directory/40399367#40399367)
[https://pypi.python.org/pypi/selenium](https://pypi.python.org/pypi/selenium)
[https://pypi.python.org/pypi/selenium](https://pypi.python.org/pypi/selenium)
