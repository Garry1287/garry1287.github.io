---
layout: post
title:  "centos-hosting"
date:   2012-01-19 05:27:10 +0400
categories: centos-hosting
tags: centos
---

# centos-hosting
1. Установка и обновление пакетов yum
  yum install mc
  
  команда

# yum update php-eaccelerator


обновит лишь пакет php-eaccelerator.


Удаление пакетов

Удаление пакетов осуществляется с помощью команды remove. Например, команда

# yum remove php-eaccelerator


  
2. Обновление системы

  yum clean all
  yum -y update
  cat /etc/redhat-release
  reboot

[http://www.centos.org/docs/5/html/yum/sn-updating-your-system.html](http://www.centos.org/docs/5/html/yum/sn-updating-your-system.html)

4. Учётные записи и безопасность системы
    useradd garry -m

[http://lostop.ru/page/42/](http://lostop.ru/page/42/)
[http://slyweb.ru/linux-vps/centos-root-sudo/](http://slyweb.ru/linux-vps/centos-root-sudo/)
[root@host ~]# usermod -a -G wheel smithy
[root@host ~]# vi /etc/pam.d/su
auth            required        pam_wheel.so use_uid





5. Руками посмотреть на LVM
  [http://www.altlinux.org/LVM](http://www.altlinux.org/LVM)
  [http://youngblog.hoster-ok.com/hello-world/](http://youngblog.hoster-ok.com/hello-world/)

6. Панель для хостинга

      2 недельный тест
      [http://ispsystem.com/ru/software/ispmanager](http://ispsystem.com/ru/software/ispmanager)
      [http://moonback.ru/page/free-hosting-panel](http://moonback.ru/page/free-hosting-panel)
      
7. Работа с репозиториями

[http://gnu.su/gnu-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8-%D1%86%D0%B5%D0%BD%D1%82%D0%BE%D1%81-6.html](http://gnu.su/gnu-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8-%D1%86%D0%B5%D0%BD%D1%82%D0%BE%D1%81-6.html)
[http://centos.alt.ru/?p=18](http://centos.alt.ru/?p=18)

[http://howtoconfig.net/linux/add-repository-epel-remi-rpmforge-centos6/](http://howtoconfig.net/linux/add-repository-epel-remi-rpmforge-centos6/)
[http://wiki.dieg.info/yum](http://wiki.dieg.info/yum)
[http://hrafn.me/articles/package-management-in-rhel6-yum/](http://hrafn.me/articles/package-management-in-rhel6-yum/)
[http://www.bog.pp.ru/work/yum.html](http://www.bog.pp.ru/work/yum.html)
[http://www.opennet.ru/man.shtml?topic=yum&category=8&russian=0](http://www.opennet.ru/man.shtml?topic=yum&category=8&russian=0)
[http://rus-linux.net/kos.php?name=papers/fedora8/yum_howto.html](http://rus-linux.net/kos.php?name=papers/fedora8/yum_howto.html)
[http://wiki.russianfedora.ru/index.php/%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0_%D1%81_Yum](http://wiki.russianfedora.ru/index.php/%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0_%D1%81_Yum)
[http://centos.alt.ru/?p=208](http://centos.alt.ru/?p=208)
[http://www.msav.ru/blog/206-configuring-nginx-as-a-frontend-for-the-apache-web-server](http://www.msav.ru/blog/206-configuring-nginx-as-a-frontend-for-the-apache-web-server)

Drupal
[http://drupal-admin.ru/blog/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-drupal-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-nginx-front-end-%D0%BA-apache](http://drupal-admin.ru/blog/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-drupal-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-nginx-front-end-%D0%BA-apache)

Nginx + apache
[http://libnix.com/nginx-centos-original-repo.html](http://libnix.com/nginx-centos-original-repo.html)

  1. Конфиг nginx для виртуальных хостов
  2. Нужен ли конфиг для апаче? Да
  3. Безопасность.
  4. iptech48.sc.int конфиг
  5. пользователь iptech48:iptech48 без bash. 
      Получается nginx будет запускаться под nginx, а apache под user, например iptech48. Чтобы был доступ к статике, надо 
      чтобы nginx имел доступ к домашней папке iptech48. Поэтому мы добовляем пользователя nginx в группу iptech48
  6. Права на папки


Настройка системы
    1. Сетевые настройки
    2. Обезопасить root
    3. Удалить ненужные программы
    4. Iptables






А еще симлинк /var/log/apache/site.com можно сделать в папку юзера, и тогда да, удалит симлинк — его проблемы, логи не увидит. 

Если же нужно защитить только одну папку (например, logs), можно поступить следующим образом:

touch /home/hostuser/vhosts/sitename.ru/logs/.keep
chattr +i /home/hostuser/vhosts/sitename.ru/logs/.keep






Установка nginx
[http://ru.ispdoc.com/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_Nginx_%D0%B2_CentOS_Linux](http://ru.ispdoc.com/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_Nginx_%D0%B2_CentOS_Linux)

Оптимизация nginx
[http://habrahabr.ru/post/198982/](http://habrahabr.ru/post/198982/)


Ipsmanager
[http://support.adelinahost.com/ustanovka-ispmanager-na-centos/](http://support.adelinahost.com/ustanovka-ispmanager-na-centos/)
[http://hostingbloger.com/2011/09/15/ustanovka-paneli-ispmanager-na-linux-centos-debian.html](http://hostingbloger.com/2011/09/15/ustanovka-paneli-ispmanager-na-linux-centos-debian.html)
[http://ru.ispdoc.com/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_ISPmanager_%28ISPmanager%29](http://ru.ispdoc.com/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_ISPmanager_%28ISPmanager%29)
[http://exweb.info/ystanovka-ispmanager-litepro-na-linux.html](http://exweb.info/ystanovka-ispmanager-litepro-na-linux.html)
[http://svirchoff.ru/linux/%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-apache-mpm-itk-%D0%BD%D0%B0-%D1%81entos-6-c-ispmanager/](http://svirchoff.ru/linux/%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D0%B8-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-apache-mpm-itk-%D0%BD%D0%B0-%D1%81entos-6-c-ispmanager/)
[http://svirchoff.ru/linux/%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-nginx-%D0%BD%D0%B0-ispmanager-centos-6/](http://svirchoff.ru/linux/%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-nginx-%D0%BD%D0%B0-ispmanager-centos-6/)
[http://info.9-33.com/viewtopic.php?f=13&t=13](http://info.9-33.com/viewtopic.php?f=13&t=13)




MPM-ITK 
[http://gleb.fdfh.ru/2010/12/14/apache-mpm-itk-na-centos-ispmanager/](http://gleb.fdfh.ru/2010/12/14/apache-mpm-itk-na-centos-ispmanager/)
[http://centos-server.ru/httpd-2216/](http://centos-server.ru/httpd-2216/)
[http://www.amiseo.ru/unix/ustanovka-apache-mpm-itk-na-centos](http://www.amiseo.ru/unix/ustanovka-apache-mpm-itk-na-centos)
[http://kaba.org.ua/articles/directadmin-sborka-apache-s-mpm-itk/](http://kaba.org.ua/articles/directadmin-sborka-apache-s-mpm-itk/)
[http://nixblog.info/linux-administration/%D0%BA%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-mpm_itk-%D0%BD%D0%B0-centos-5-ispmanager/](http://nixblog.info/linux-administration/%D0%BA%D0%B0%D0%BA-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C-mpm_itk-%D0%BD%D0%B0-centos-5-ispmanager/)


    от рута это родительские. 
Дочерние - от юзеров, отрабатывают за долю секунды и завершаются, их фиг поймаешь(в топе например).


[http://adw0rd.com/2009/3/27/nginx-and-apache-install/#.UluzZFSexkG](http://adw0rd.com/2009/3/27/nginx-and-apache-install/#.UluzZFSexkG)

2G памяти
nginx
    128
proxy buffer (16 8k) x 1024 connect
apache
    384
php
    640
mysql
    384

остальное 512 


Мы сами определяем max размер запроса к серверу



1Г выделяет на nginx    (4096x256k)        
	Рассчитываем на 4096 соединений
	256k - это 32 x 8 server buffer
3Г выделяется на apache
	150 соединений
5G выделаятеся на php
	150 соединений
3G на mysql
1G на остальное


Настройка системы
    1. Сетевые настройки
    2. Обезопасить root
    3. Удалить ненужные программы
    4. Iptables





Мониторинг
    процессор
    память
    диск
    своп

Включить mod status для nginx и apache
2. Поставить munin+плагины mysql, nginx, apache и стандартные
3. Включить slow log mysql
4. Найти сайт который создает нагрузку




Бэкап базы
mysqldump -u root -p -f name_database > C:\mydb_backup_name_database.txt
mysql -u root -p -f name_database < C:\mydb_backup_name_database.txt
[http://info-linux.ru/article/78](http://info-linux.ru/article/78)

Erlan Esnazarov, так если вы хотите дамп на другой сервак залить, а не создать вам нужна другая команда:

mysql -h db.host.kz -uroot -ppassword BD < BD.sql






mod_rpaf

Подводные камни в пхп-скриптах видел такие:

    При использовании $_SERVER['SERVER_NAME'], $_SERVER['HTTP_HOST'], $_SERVER['SERVER_PORT'] будут отображаться данные apache-бэкэнда, т.е. может вылезти ерунда, если эти переменные используются в выводе
    При использовании $_SERVER['REMOTE_HOST'] и $_SERVER['REMOTE_ADDR'] будут выдаваться данные nginx-фронтжнда


[http://lib.clodo.ru/web-server/webserver-lna.html](http://lib.clodo.ru/web-server/webserver-lna.html)
[http://help-host.ru/servers/apache-nginx/22-ustanovka-mod_rpaf-debian-nginxapache.html](http://help-host.ru/servers/apache-nginx/22-ustanovka-mod_rpaf-debian-nginxapache.html)
[http://dimetrius.net/blog/linux/13-ustanovka-nginx-na-server-fedora-14-pod-upravleniem-ispconfig-3.html](http://dimetrius.net/blog/linux/13-ustanovka-nginx-na-server-fedora-14-pod-upravleniem-ispconfig-3.html)
http://сеоша.рф/%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD%D1%8B-%D0%B8-%D1%85%D0%BE%D1%81%D1%82%D0%B8%D0%BD%D0%B3/%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80/62-%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-mod_rpaf-%D0%BD%D0%B0-apache-2-x-nginxapache
[http://i-notes.org/centos-nginx-apache-mod_rpaf/](http://i-notes.org/centos-nginx-apache-mod_rpaf/)









Заглушка для default хоста
# default virtual host
server {
listen 80 default;
server_name localhost;
deny all;
}





Bad buffering/timeout configuration.



find . -type f | wc -l


find . -type d -exec

find . -type f -exec

find /path -type d | xargs chmod 0755

Однако, директории с именами, содержащими пробелы, методом перенаправления через xargs обработаны не будут, поэтому следует использовать первый вариант, дополненный:

find /path -type d -exec chmod 0755 "{}" \;

Указанную выше команду find можно заменить следующим образом:

find options | xargs [commands_to_execute_on_found_files]

Команда xargs создает из стандартного входного потока командные строки и их выполняет. 
Преимущество в том, что командная строка заолняется до тех пор, пока не будет достигнут предел, определенный системой.
 Только после этого команда будет вызвана на исполнение; в приведенном выше примере это команда rm. 
Если еще есть аргументы, будет взята новая строка, которая будет заполняться до тех пор, 
пока это будет возможно или пока не закончатся аргументы. То же самое можно сделать с помощью вызова find -exec;
 но в этом случае команда будет выполняться для найденных файлов каждый раз, когда будет найден очередной файл.
 Следовательно, команда xargs значительно увеличит скорость работы вашего скрипта и повысит производительность вашей машины.













php-eaccelerator.x86_64       - настройка








Тест сайта
[http://tsung.erlang-projects.org/](http://tsung.erlang-projects.org/)
[http://jokerov.com/testirovanie/nagruzochnoe-testirovanie-sajta-apache-benchmark/](http://jokerov.com/testirovanie/nagruzochnoe-testirovanie-sajta-apache-benchmark/)
[http://debian-help.ru/web-servers/ab-apache-benchmark-test-proizvoditelnosti-servera/](http://debian-help.ru/web-servers/ab-apache-benchmark-test-proizvoditelnosti-servera/)





Полезности
[http://it-notepad.ru/](http://it-notepad.ru/)
[http://it-notepad.ru/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D1%81%D1%82%D0%B5%D0%BA%D0%B0-%D0%BE%D1%81.html](http://it-notepad.ru/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D1%81%D1%82%D0%B5%D0%BA%D0%B0-%D0%BE%D1%81.html)
[http://habrahabr.ru/post/206488/](http://habrahabr.ru/post/206488/)
[http://wiki.linuxformat.ru/wiki/%D0%97%D0%B0%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%B0%D1%8F_%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0](http://wiki.linuxformat.ru/wiki/%D0%97%D0%B0%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D0%B0%D1%8F_%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0)
[http://centos.name/?page/tipsandtricks/YumAndRpm](http://centos.name/?page/tipsandtricks/YumAndRpm)
[http://it-talk.ru/?p=85](http://it-talk.ru/?p=85)
[http://centos.name/?page/tipsandtricks/UncompressMultipleFiles](http://centos.name/?page/tipsandtricks/UncompressMultipleFiles)
[http://centos.name/?page/tipsandtricks/SelinuxBooleans](http://centos.name/?page/tipsandtricks/SelinuxBooleans)
[http://centos.name/?page/tipsandtricks/becomingroot](http://centos.name/?page/tipsandtricks/becomingroot)
[http://svirchoff.ru/linux/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D1%8B%D1%85-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B9-%D0%B8%D0%BB%D0%B8-%D1%81%D0%BD/](http://svirchoff.ru/linux/%D0%BE%D0%BF%D1%82%D0%B8%D0%BC%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D1%8B%D1%85-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B9-%D0%B8%D0%BB%D0%B8-%D1%81%D0%BD/)
[http://svirchoff.ru/%D1%80%D0%B0%D0%B7%D0%BD%D0%BE%D0%B5/%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D1%8F%D0%B5%D0%BC-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%B4%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%B8-%D1%81%D0%BA%D0%BE/](http://svirchoff.ru/%D1%80%D0%B0%D0%B7%D0%BD%D0%BE%D0%B5/%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D1%8F%D0%B5%D0%BC-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%B4%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C-%D0%B8-%D1%81%D0%BA%D0%BE/)
[http://centos.alt.ru/?p=188](http://centos.alt.ru/?p=188)
[http://habrahabr.ru/post/159203/](http://habrahabr.ru/post/159203/)
[https://docs.google.com/drawings/d/1cLsGEwEnuEEs8wW0gv2NCWQopY1cnDsRsZFfz1X_MZ8/edit?pli=1](https://docs.google.com/drawings/d/1cLsGEwEnuEEs8wW0gv2NCWQopY1cnDsRsZFfz1X_MZ8/edit?pli=1)
[http://habrahabr.ru/post/160189/](http://habrahabr.ru/post/160189/)
[http://habrahabr.ru/post/93274/](http://habrahabr.ru/post/93274/)
[http://education.aspu.ru/view.php?olif=gl5](http://education.aspu.ru/view.php?olif=gl5)
[http://habrahabr.ru/sandbox/21382/](http://habrahabr.ru/sandbox/21382/)
[http://www.ibm.com/developerworks/ru/library/l-lpic1-v3-103-4/](http://www.ibm.com/developerworks/ru/library/l-lpic1-v3-103-4/)
[http://habrahabr.ru/post/153589/](http://habrahabr.ru/post/153589/)
[http://habrahabr.ru/sandbox/62683/](http://habrahabr.ru/sandbox/62683/)
[http://habrahabr.ru/post/198982/](http://habrahabr.ru/post/198982/)
[http://habrahabr.ru/post/201814/](http://habrahabr.ru/post/201814/)


SSH
[http://linux.yaroslavl.ru/docs/conf/security/sec_book/ch11_2.html](http://linux.yaroslavl.ru/docs/conf/security/sec_book/ch11_2.html)
[http://ubuntovod.ru/instructions/21-sposob-zashity-openssh.html](http://ubuntovod.ru/instructions/21-sposob-zashity-openssh.html)

Tcpwrappers
[http://www.centos.org/docs/5/html/Deployment_Guide-en-US/ch-tcpwrappers.html](http://www.centos.org/docs/5/html/Deployment_Guide-en-US/ch-tcpwrappers.html)
[http://www.cyberciti.biz/faq/tcp-wrappers-hosts-allow-deny-tutorial/](http://www.cyberciti.biz/faq/tcp-wrappers-hosts-allow-deny-tutorial/)
[http://rus-linux.net/lib.php?name=/MyLDP/sec/tcpwrappers.html](http://rus-linux.net/lib.php?name=/MyLDP/sec/tcpwrappers.html)

Настольная книга
[http://www.gentoo.org/doc/ru/security/security-handbook.xml?full=1](http://www.gentoo.org/doc/ru/security/security-handbook.xml?full=1)
[http://ru.wikibooks.org/wiki/%D0%9D%D0%B0%D1%81%D1%82%D0%BE%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BD%D0%B8%D0%B3%D0%B0_%D0%BF%D0%BE_Linux](http://ru.wikibooks.org/wiki/%D0%9D%D0%B0%D1%81%D1%82%D0%BE%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BD%D0%B8%D0%B3%D0%B0_%D0%BF%D0%BE_Linux)



OpenVz и другие контейнеры
[http://habrahabr.ru/post/210460/](http://habrahabr.ru/post/210460/)
[http://habrahabr.ru/company/FastVPS/blog/209072/](http://habrahabr.ru/company/FastVPS/blog/209072/)

Selinux
[http://habrahabr.ru/company/kingservers/blog/209970/](http://habrahabr.ru/company/kingservers/blog/209970/)



Повышение безопасности linux
[https://habrahabr.ru/company/ruvds/blog/343892/](https://habrahabr.ru/company/ruvds/blog/343892/)
