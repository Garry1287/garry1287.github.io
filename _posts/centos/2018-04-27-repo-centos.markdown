---
layout: post
title:  "repo-centos"
date:   2018-04-27 11:08:34 +0300
categories: repo-centos
tags: centos
---

# repo-centos
[http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/](http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/)

## RHEL/CentOS 7 64-Bit ##
# wget [http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm](http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm)
# rpm -ivh epel-release-7-2.noarch.rpm

Установка пакета из выбранного репозитория
sudo yum --enablerepo=remi install php-tcpdf

systemctl enable mariadb.service
systemctl start mariadb.service
mysql_secure_installation


[http://centos.name/?page/additionalresources/repositories](http://centos.name/?page/additionalresources/repositories)
[http://howtoit.ru/linux/centos/item/15-podklyuchenie-repozitoriev-centos-6-epel-rpmforge-remi.html](http://howtoit.ru/linux/centos/item/15-podklyuchenie-repozitoriev-centos-6-epel-rpmforge-remi.html)
[http://www.rackspace.com/knowledge_center/article/install-epel-and-additional-repositories-on-centos-and-red-hat](http://www.rackspace.com/knowledge_center/article/install-epel-and-additional-repositories-on-centos-and-red-hat)
[http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/](http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/)
[http://www.cyberciti.biz/faq/installing-rhel-epel-repo-on-centos-redhat-7-x/](http://www.cyberciti.biz/faq/installing-rhel-epel-repo-on-centos-redhat-7-x/)


YUM
[http://hrafn.me/articles/package-management-in-rhel6-yum/](http://hrafn.me/articles/package-management-in-rhel6-yum/)
[http://www.bog.pp.ru/work/yum.html](http://www.bog.pp.ru/work/yum.html)
[http://www.shellhacks.com/ru/Dobavlenie-Repozitoriya-EPEL-v-CentOS-RHEL](http://www.shellhacks.com/ru/Dobavlenie-Repozitoriya-EPEL-v-CentOS-RHEL)