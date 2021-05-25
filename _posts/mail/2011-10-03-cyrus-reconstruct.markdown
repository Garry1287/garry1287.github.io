---
layout: post
title:  "cyrus-reconstruct"
date:   2011-10-03 03:04:28 +0400
categories: mail
tags: mail
---

# cyrus-reconstruct
reconstruct

reconstruct -m


su -l cyrus -c '/usr/lib/cyrus-imapd/reconstruct -r user.sanek

/usr/lib/cyrus/bin/reconstruct -r user/ckn@sc.ru

/usr/lib/cyrus/bin/reconstruct -r user/pas@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/s.smolyaninov@sc.ru


/usr/lib/cyrus/bin/reconstruct -r user/nio@sc.ru

/usr/lib/cyrus/bin/reconstruct -r user/avd@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/pta@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/pas@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/a.ignatenko@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/t.antipova@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/tol@sc.ru
/usr/lib/cyrus/bin/reconstruct -r user/i.sapova@sc.ru


далее по su переходим на юзера cyrus и из-под него выполняем комманду reconstruct -r user.pupkin


восстановить ящик (перечитывает все письма и восстанавливает или делает новую БД)

 sudo -u cyrus /usr/lib/cyrus-imapd/reconstruct -r user.kgb

сделать индекс ящика (ускорить поиск)

sudo -u cyrus /usr/lib/cyrus-imapd/squatter -r -i user.kgb


[http://valynkin.ru/articles/41/ustanovka-nastroika-i-obsluzhivanie-cyrus-imapd-na-centos-shpargalka](http://valynkin.ru/articles/41/ustanovka-nastroika-i-obsluzhivanie-cyrus-imapd-na-centos-shpargalka)










Если журнал почты нашел это:

said: 451 4.3.0 System I/O error (in reply to RCPT TO command))

Это происходит, когда делает RM удалять сообщения в /var/spool/cyrus/mail/foo/mail/bar, чтобы исправить необходимо войти как пользователь cyrus


	
su - cyrus

Затем запустите команд
cyrus@server:~$ /usr/lib/cyrus/bin/reconstruct -r -f user.foobar


Результат будет что-то вроде этой команды:

user.foobar
user.foobar.Drafts
user.foobar.Sent
user.foobar.Custom
user.foobar.OtherCustom
user.foobar.Trash

А потом
1
	
cyrus@server:~$ 




При этом мы восстановить структуры, которые имеют пользователя в вашем почтовом ящике.















создаем директорию ящика (если повредилась и отсутствует), проверяем права доступа на группу cyrus
su cyrus
%/usr/local/cyrus/bin/reconstruct -r "user.username@domain"

и если потребуется:
/usr/local/etc/rc.d/imapd restart



от сноса служебного файлА в дирах всегда помогает reconstruct.
второе issue, которое мне регулярно встречается на сайрусе - при кончине свободного места на разделе ломаются .seen у тех мэйлбоксов,
 кто там сидел в дагнный момент, и цепляющиеся процессы начинают падать с sig11. это лечится echo -n "" > pupkin.seen.









Полезные ссылки
[http://www.tldp.org/HOWTO/Cyrus-IMAP.html#toc8](http://www.tldp.org/HOWTO/Cyrus-IMAP.html#toc8)
[http://www.kryukov.biz/wiki/Cyrus-imapd](http://www.kryukov.biz/wiki/Cyrus-imapd)
[http://www.opennet.ru/docs/RUS/Cyrus_imap/install.html](http://www.opennet.ru/docs/RUS/Cyrus_imap/install.html)
[http://plone.uconn.edu/Members/jar02014/huskymail/cyrus-imap-file-formats-and-recovery](http://plone.uconn.edu/Members/jar02014/huskymail/cyrus-imap-file-formats-and-recovery)
[http://comments.gmane.org/gmane.linux.altlinux.sysadmins/11389](http://comments.gmane.org/gmane.linux.altlinux.sysadmins/11389)


Exim
[http://www.opennet.ru/docs/RUS/Cyrus_imap/overview.html](http://www.opennet.ru/docs/RUS/Cyrus_imap/overview.html)
[http://wiki.leonchik.ru/doku.php?id=exim:exim-debug](http://wiki.leonchik.ru/doku.php?id=exim:exim-debug)
[http://www.opennet.ru/docs/RUS/exim_guide/1205.html](http://www.opennet.ru/docs/RUS/exim_guide/1205.html)







# stop cyrus
cyr_dbtool /var/lib/imap/mailboxes.db skiplist show > mailboxes.dump
cyr_dbtool -n /var/lib/mailboxes_new.db skiplist set < mailboxes.dump
mv /var/imap/mailboxes.db /var/imap/mailboxes_old.db
mv /var/lib/mailboxes_new.db /var/imap/mailboxes.db
# start cyru






I have tried running several commands to fix the problem with no success:
# sudo -u cyrusimap /usr/bin/cyrus/bin/ctl_cyrusdb -c
# sudo -u cyrusimap /usr/bin/cyrus/bin/ctl_cyrusdb -r
# /usr/bin/cyrus/bin/reconstruct -i 





точно
su -l cyrus -c '/usr/lib/cyrus-imapd/reconstruct -r user.sanek'
восстанавливает даже все три файла если их удалить

кстати по очистке ящика тоже нашел
su - cyrus -c "/usr/lib/cyrus-imapd/ipurge -f -b 0 user.sanek"
:) 





Поэтому я просто удалил этот файл (/var/lib/imap/domain/e/egida-sb.ru/user/v/viktor.seen) и 
восстановил почтовый каталог (mailbox) командой reconstruct -r -f user.viktor@egida-sb.ru. Вошел через почтовый клиент и все заработало....


В общем если reconstruct не помогает, то нужно грохать эту бд и создавать заново.
 После создавания заново нужно регулярно делать plain text dump этих баз, что бы потом можно было их вливать обратно.


ключевое слово - практически.. для нормального reconstruct в 2.1 нужно было перезапускать cyrmaster, в 2.2 уже ненужно.
 Да и производителность у 2.2 меня радует. 2.3 даже не щупал, народ в рассылках нелестен к этой ветке.

проблемы всегда будут без соблюдения жёстких условий эксплуатации и бесперебойного сервиса баз, вообще для cyrus испорченные индексы это норма,
 если есть клиенты типа thebat на медленных соединениях или последние веяния войны
 за блокировки на сервере с практически 100% результатом испорченных индексов: 2 одновременно подключённых и работающих с одним боксом imap клиента с iPod-ов













Cyrus 452 4.2.2 Over quota
[http://www.minigeek.org/?p=156](http://www.minigeek.org/?p=156)

su - cyrus -c "/bin/quota -f user/"












cyrus требует пароль
[http://www.opennet.ru/openforum/vsluhforumID1/79449.html](http://www.opennet.ru/openforum/vsluhforumID1/79449.html)


начните с testsaslauthd
когда на пользователя cyrus и его пароль будет success, удостоверьтесь в imapd.conf, что cyrus является админом чего вам нужно.
и только потом набирайте cyradm --user cyrus --server bla-b

