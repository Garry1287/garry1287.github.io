---
layout: post
title:  "openvpn-howto"
date:   2014-06-01 05:27:41 +0400
categories: vpn
tags: vpn
---

# openvpn-howto
О tls
[https://mnorin.com/tls-ssl-neobhodimy-j-minimum-znanij.html](https://mnorin.com/tls-ssl-neobhodimy-j-minimum-znanij.html)
[https://habrahabr.ru/post/188042/](https://habrahabr.ru/post/188042/)
[https://habrahabr.ru/post/258285/](https://habrahabr.ru/post/258285/)

Подробно о tls
[https://tls.dxdt.ru/tls.html](https://tls.dxdt.ru/tls.html)


ca.crt - сертификат ключа центра сертификации
ca.key  - секретный ключ CA - центра сертификации
crl.pem - список отозванных сертификатов

dh1024.pem - Файл Диффи-Хелмана для защиты трафика от расшифровки
ta.key -  	Ключ HMAC для дополнительной защиты от DoS-атак и флуда

ipp.txt - файл со списком ip адресов выдаваемых клиентам
openvpn-srv.conf  - конфиг сервера
easy-rsa/  - каталог программы easy-rsa для управления pki
ccd/ - каталог, в котором будут хранится индивидуальные настройки клиентов:

server.crt -  	Сертификат сервера OpenVPN
server.csr -   запрос на сертификат сервера OpenVPN
server.key  -  секретный ключ сервера OpenVPN







Bash команды
[http://white55.ru/export.html](http://white55.ru/export.html)
[http://rus-linux.net/MyLDP/consol/export.html](http://rus-linux.net/MyLDP/consol/export.html)
Команда export - команда командной оболочки UNIX, добавляющая переменную в среду окружения.
. В целом команда export отмечает переменную окружения для экспорта с любым новым дочерним процессом, и это позволяет дочернему процессу наследовать все отмеченные переменные. В данной статье этот процесс будет описан более подробно.

export работает так    РОДИТЕЛЬСКИЙ Процесс передаёт ДОЧЕРНЕМУ отмеченные им переменные


Но обратный процесс не работает, чтобы ДОЧЕРНИЙ мог передать с помощью export РОДИТЕЛЬСКОМУ используют source или точку.
[http://my-it-notes.com/2011/10/how-to-execute-bash-script-in-current-console-environment-using-source-command/](http://my-it-notes.com/2011/10/how-to-execute-bash-script-in-current-console-environment-using-source-command/)

Разница между  source, ./  и .
-----------------------------------------------------------------------------------------------------------------------------------------
Для того чтобы команды скрипта выполнялись в контексте текущего экземпляра интерпретатора необходимо
использовать команду “source” или его аналог команду “.” – да, команда точка.
1) . ./test_export.sh или source ./test_export.sh
2) echo $MYVAR
Таким образом мы указываем интерпретатору не запускать дополнительный экземпляр для обработки комманд скрипта,а заняться им самому.

This is the syntax of the . built-in, which does do the same thing as source:
source  .vars
. .vars
- Это одно и тоже

./vars 
отличается

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Команда source – как выполнить bash-скрипт не запуская второй процесс bash
	

В линукс-системах, в консоли, каждый скрипт запускается следующим образом:

1) определяется необходимый интерпретатор для его выполнения (на основе указания-подсказки внутри самого файла, по расширению, и т.п.)
2) запускается новый процесс командного интерпретатора, в рамках которого и выполняются инструкции из скрипта
3) процесс-родитель, из которого была запущена новая копия интерпретатора приостанавливает свою работу
4) по выполнении всех инструкций дочерний процесс интерпретатора завершает свою работу
5) процесс-родитель возобновляет свою работу

Почему это имеет значение? Представьте что у вас есть некоторая иерархическая система скриптов использующих одну переменную, значение которой определяется динамически, на основе нескольких параметров. Почему после запуска скрипта должным образом инициализированная и экспортированная переменная не доступна из консоли, из которой производился запуск и не может быть использована другими скприптами?

У каждого процесса есть своя собственная среда окружения (в это понятие, кроме всего прочего, входят и переменные окружения). Когда мы в контексте дочернего процесса экспортировали переменную, она успешно сохранялась в переменных окружения дочернего процесса и существовала все время пока существовал сам дочерний процесс. По завершению дочернего процесса – когда были выполнены все команды из файла-скрипта, дочерний процесс завершился, вместе с чем его рабочее пространство со всеми экспортируемыми переменными также перестало существовать.

В результате, если у вас есть скрипт test_export.sh следующего содержания
#!/bin/sh
export MYVAR=”some value”;
то результатом следующей последовательности команд:

1)  ./test_export.sh
2)  echo $MYVAR

будет пустая строка – текущему экземпляру интерпретатора ничего не известно о только что завершившемся процессе интерпретатора, выполнявшего какие-то экспорты в свою среду окружения.

Для того чтобы команды скрипта выполнялись в контексте текущего экземпляра интерпретатора необходимо
использовать команду “source” или его аналог команду “.” – да, команда точка.

1) . ./test_export.sh или source ./test_export.sh
2) echo $MYVAR

Таким образом мы указываем интерпретатору не запускать дополнительный экземпляр для обработки комманд скрипта,а заняться им самому.

А вообще, по-хорошему, переменные окружения должны устанавливаться специальными startup или pre-load-скриптами, выполняющимися при загрузке самой системы, x-window или нового экземпляра консоли – в зависимост от наших конкретных задач. Есть специальные утилиты для управления скриптами, выполняемыми при загрузке системы – update-rc.d, file-rc. Но, при острой необходимости управлять скриптами можно и голыми руками: гуглить “.bashrc”, “.bash_profile”, “.profile”, /etc/rc?.d/rc.N ).

[http://askubuntu.com/questions/182012/is-there-a-difference-between-and-source-in-bash-after-all](http://askubuntu.com/questions/182012/is-there-a-difference-between-and-source-in-bash-after-all)











Устанавливаем openvpn, easy-rsa (программу для управления pki)

/usr/share/docs - там нормальный мануал по программе и ещё [https://github.com/OpenVPN/easy-rsa/blob/master/doc/EasyRSA-Readme.md](https://github.com/OpenVPN/easy-rsa/blob/master/doc/EasyRSA-Readme.md)
[https://openvpn.net/index.php/open-source/documentation/miscellaneous/77-rsa-key-](https://openvpn.net/index.php/open-source/documentation/miscellaneous/77-rsa-key-)

Первый шаг
------------------------------------------------------------------------------------------------------------------
Копируем easy-rsa папку в /etc/openvpn

Никаких переименование в vars openssl я не делал,

В папке в easy-rsa есть файл vars
В vars прописываем наши параметры, используются для генерации сертификата
export KEY_COUNTRY="RU"
export KEY_PROVINCE="LPK"
export KEY_CITY="LIPETSK"
export KEY_ORG="iptech-io"
export KEY_EMAIL="hd@iptech-io.ru"


[root@iptech 2.0]# vi vars 
[root@iptech 2.0]# source ./vars
NOTE: If you run ./clean-all, I will be doing a rm -rf on /etc/openvpn/easy-rsa/2.0/keys


(Все эти команды на самом деле алиасы с разными параметрами на pkitool, а pkitool - это скрипт который вызывает openssl с определёнными параметрами)
Очищаем существующие
./clean-all

Генерим новый CA ключ и сертификат
./build-ca



Генерируем сертификат и ключ для сервера (vpnserver): Генерить сразу ключ, сертификат и запрос на сертификат. Можно сначала сгенерить запрос на сертификат, а потом подписать его
./build-key-server vpnserver 

Теперь генерируем файл параметров по алгоритму Diffie-Hellman:
./build-dh 

Генерируем сертификат и ключ для клиента velowup (такое вот имя у клиентского сертификата):
./build-key velowup


И последним создаем общий ключ для клиентов и сервера. Это TLS-ключ:
openvpn --genkey --secret ta.key 





СОЗДАНИЕ запроса на подпись, а затем подпись его и создание сертификата
[root@iptech 2.0]# ./pkitool --csr iptech-gcrs
Generating a 2048 bit RSA private key
......................................+++
.+++
writing new private key to 'iptech-gcrs.key'
-----
[root@iptech 2.0]# ls
build-ca  build-inter  build-key-pass    build-key-server  build-req-pass  inherit-inter  list-crl           openssl-0.9.8.cnf  pkitool      sign-req  whichopensslcnf
build-dh  build-key    build-key-pkcs12  build-req         clean-all       keys           openssl-0.9.6.cnf  openssl-1.0.0.cnf  revoke-full  vars
[root@iptech 2.0]# cd keys/
[root@iptech keys]# l
-bash: l: команда не найдена
[root@iptech keys]# ls
01.pem  03.pem  ca.key      index.txt       index.txt.attr.old  iptech-false.crt  iptech-false.key  iptech-garry.csr  iptech-gcrs.csr  serial      vpnserver.crt  vpnserver.key
02.pem  ca.crt  dh2048.pem  index.txt.attr  index.txt.old       iptech-false.csr  iptech-garry.crt  iptech-garry.key  iptech-gcrs.key  serial.old  vpnserver.csr
[root@iptech keys]# ./pkitool --sign iptech-gcrs
-bash: ./pkitool: Нет такого файла или каталога
[root@iptech keys]# cd ..
[root@iptech 2.0]# ./pkitool --sign iptech-gcrs
Using configuration from /etc/openvpn/easy-rsa/2.0/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
countryName           :PRINTABLE:'RU'
stateOrProvinceName   :PRINTABLE:'LPK'
localityName          :PRINTABLE:'LIPETSK'
organizationName      :PRINTABLE:'iptech-io'
commonName            :PRINTABLE:'iptech-gcrs'
name                  :PRINTABLE:'EasyRSA'
emailAddress          :IA5STRING:'hd@iptech-io.ru'
Certificate is to be certified until Mar 12 13:04:30 2027 GMT (3650 days)

Write out database with 1 new entries
Data Base Updated
[root@iptech 2.0]# ls



























Запуск клиента
garry:/etc/openvpn # ls
ca.crt  iptech-garry.conf  iptech-garry.crt  iptech-garry.key  ta.key
garry:/etc/openvpn # ls -al
total 40
drwxr-xr-x   2 root root  4096 Mar 14 17:22 .
drwxr-xr-x 145 root root 12288 Mar 14 10:38 ..
-rw-r--r--   1 root root  1639 Mar 14 16:41 ca.crt
-rw-r--r--   1 root root   473 Mar 14 16:42 iptech-garry.conf
-rw-r--r--   1 root root  5238 Mar 14 16:41 iptech-garry.crt
-rw-------   1 root root  1704 Mar 14 16:41 iptech-garry.key
-rw-------   1 root root   636 Mar 14 16:41 ta.key
garry:/etc/openvpn # systemctl start openvpn@iptech-garry




-------------------------------------------------------------------------------------------------------------------------------------------
Отзыв сертификата
в easy-rsa
/revoke-full iptech-false
 
 После этого появился файл crl.pem, который я скопировал в конфиг openvpn

 Можно его получить и  пустым, при первоначальной настройке
 [http://mdex-nn.ru/blokirovka-sertifikat-openvpn.html](http://mdex-nn.ru/blokirovka-sertifikat-openvpn.html)
 
 
 IPTABLES никак не настраивал кроме 1 пункта, но необходимо 
1) Разрешить 1194 порту по UDP (или какой другой) на обычном eth интерфейсе
2)разрешить ходить траффик через tun (tap) интерфейс - INPUT правила, OUTPUT правила. Если соединяем локальные сети по OPENVPN, то ещё и FORWARD
    конечно можно резать на этих интерфейсах траффик также, как на обычных eth
 
 Теперь можно переходить к настройкам файервола.
В iptables перед строчками, запрещающими все INPUT и FORWARD

-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited


пишем:

-A INPUT -i tun0 -j ACCEPT
-A FORWARD -i tun0 -j ACCEPT


Также добавляем строки «натизации»:
Это чтобы у клиентов, которые подключились к openvpn из сети 10.10.20.0/24  был доступ в инет

*nat 
:PREROUTING ACCEPT [4:614] 
:POSTROUTING ACCEPT [18:936] 
:OUTPUT ACCEPT [18:936] 
-A POSTROUTING -s 10.10.20.0/24 -o eth0 -j MASQUERADE


 -----------------------------------------------------------------------------------------------------------------------------------------------------------------
Из под какого user запускать?
По умолчанюи все файлы на сервере принадлежат root и  запускаю из под nobody -
Вроде все ок
ps acux | grep open
nobody   23098  0.0  0.1  45032  3692 ?        Ss   Mar14   0:02 openvpn

На клиенте тоже гуд
garry:/etc/openvpn # ps aucx | grep openvp
nobody    4291  0.5  0.1  45212  5156 ?        Ss   11:14   0:00 openvpn

Но по умолчанию при установке в Centos появляется пользователь openvpn
Я так понимаю, если сделать владельцем всех файлов в папке пользвователем openvpn, то можно запускать и из-под него

Генерить сертификаты и ключи кошерно на отдельном сервере, особенно СА сертификат и лучше всего это делать под отдельным пользователем, например userca
На клиентах и vpnserver генерить ключ и запрос на подпись (csr) 
 
 
 
 
 Сам мануал
 [https://openvpn.net/index.php/open-source/documentation/howto.html](https://openvpn.net/index.php/open-source/documentation/howto.html)
 
 Тоже 
 [http://lithium.opennet.ru/articles/openvpn/openvpn-howto.html](http://lithium.opennet.ru/articles/openvpn/openvpn-howto.html)
 
 Хорошие мануалы
 [https://habrahabr.ru/post/233971/](https://habrahabr.ru/post/233971/)
[https://habrahabr.ru/post/100932/](https://habrahabr.ru/post/100932/)


На centos6
[http://dedicatesupport.com/content/nastroika-openvpn-na-centos-6x](http://dedicatesupport.com/content/nastroika-openvpn-na-centos-6x)
[http://demi4.com/ustanovka-openvpn-centos-6/](http://demi4.com/ustanovka-openvpn-centos-6/)

Достаточно свежий мануал
[https://www.digitalocean.com/community/tutorials/openvpn-ubuntu-16-04-ru](https://www.digitalocean.com/community/tutorials/openvpn-ubuntu-16-04-ru)

Тоже не плохой
[http://linux-bash.ru/mseti/51-openvpn.html](http://linux-bash.ru/mseti/51-openvpn.html)





Перегенерация crl
openssl ca -keyfile private/ca.key.pem -cert certs/ca.cert.pem -gencrl -out crl/crl.pem
