---
layout: post
title:  "Установка jekyll на opensuse и github pages"
date:   2018-12-17 10:31:15 +0300
categories: jekyll posts
---


# Установка jekyll на opensuse и github pages #
* `zypper install ruby-devel`
* `zypper search gcc`
* `zypper install gcc-c++`

Gem - менеджер пакетов для ruby, как pip для python

`gem install bundle jekyll`

В suse надо добавлять версию через точку.

`jekyll.ruby2.5 -v`

`cd /home/garry/MyBlog/`

Создание 

`jekyll.ruby2.5 new iptech-blog`

Запуск сайта и встроенного веб-сервера

`bundle.ruby2.5 exec jekyll.ruby2.5 serve`

## Работа с git
Создаем новый репозиторий на github, с названием, как username. Не забываем в setting поставить галочку для github-pages.

Клонируем репозиторий к себе (один README файл), потом создаем там сайт, добавлем все файлы в него

`git init`

`git add .`

Добавляем удалённый репозиторий как источник
`git remote add origin https://github.com/Garry1287/iptech.github.io.git`

Коммитим

`git commit -m "first blog commit`

Пушим файлы в удалённых репозиторий с компьютера

`garry-w:/home/garry/MyBlog/test-blog # git push origin master`



## Что надо ещё почитать
Надо сделать дизайн страниц новый
[https://jekyllrb.com/docs/themes/#overriding-theme-defaults](https://jekyllrb.com/docs/themes/#overriding-theme-defaults)

По умолчанию стоит тема minima и файлы css и некоторые другие лежат не в осноной папке сайта, а в папке темы.
Чтобы на github все заработало их надо тоже скопировать

1. [http://www.unix-lab.org/posts/jekyll/](http://www.unix-lab.org/posts/jekyll/) 
2. [https://guides.hexlet.io/jekyll/](https://guides.hexlet.io/jekyll/)
3. [https://gosha20777.github.io/blog/github/jekyll/2017/01/28/blog-with-github/](https://gosha20777.github.io/blog/github/jekyll/2017/01/28/blog-with-github/)
4. [https://frontender.info/build-blog-jekyll-github-pages](https://frontender.info/build-blog-jekyll-github-pages/)
5. [https://annimon.com/article/2658](https://annimon.com/article/2658)

[Тема для оформления блога](http://jekyllthemes.org/themes/Less-Or-More/)

[Markdown краткое описание](https://paulradzkov.com/2014/markdown_cheatsheet/)
