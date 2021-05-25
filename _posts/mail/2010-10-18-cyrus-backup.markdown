---
layout: post
title:  "cyrus-backup"
date:   2010-10-18 01:35:10 +0400
categories: mail
tags: mail
---

# cyrus-backup
Cyrus backup

[http://www.gtkdb.de/index_33_1622.html](http://www.gtkdb.de/index_33_1622.html)
www.komaii.com/linux/cyrus-imapd-backup/


SPOOLDIR=/var/spool/imap
ACCOUNTINGDIR=/var/lib/imap/user
su - cyrus -c "/usr/lib/cyrus-imapd/ctl_mboxlist -d" > /var/tmp/mailboxlist.txt


10 5 * * * /usr/lib/cyrus/bin/ctl_mboxlist -d > /usr/local/backup/mail_backup/backup-mboxlist
10 6 * * * /bin/tar -Pcjf /usr/local/backup/mail_backup/mail-data-backup.tar.bz2 /var/spool/imap
10 7 * * * /bin/tar -Pcjf /usr/local/backup/mail_backup/sieve-backup.tar.bz2 /var/lib/sieve
10 8 * * * /bin/tar -Pcjf /usr/local/backup/mail_backup/imap-backup.tar.bz2 /var/lib/imap/user



rsync -va --delete --delete-after /var/lib/cyrus/ user@failoverserver:/var/lib/cyrus/
rsync -va --delete --delete-after /var/spool/cyrus/ user@failoverserver:/var/spool/cyrus/


 Backup of mailboxes.db

When creating the backup, the file mailboxes.db should be saved separately. This file's content can be recreated by Cyrus,
 but all information on read mails or marked mails would be lost. If this file is damaged, its content is irrevocably lost. 
The following command converts the file into a plaintext file:

su - cyrus -c "/usr/sbin/ctl_mboxlist -d" > /var/lib/cyrus/mailboxlist.txt

Reloading this file is only needed, when there is a difference in the Cyrus version between the primary mailserver and the restored server. 
The file is saved in /var/lib/cyrus and will be saved automatically during the second rsync-call.
To restore the file mailboxes.txt (if needed) at a later time, e.g. after restoring the backup, the following command is used:

su - cyrus -c "/usr/sbin/ctl_mboxlist -u < /var/lib/cyrus/mailboxlist.txt"


/var/spool/imap
/var/lib/imap
/var/lib/sieve
и DB mboxlist


[https://docs.kolab.org/administrator-guide/backup-and-restore.html](https://docs.kolab.org/administrator-guide/backup-and-restore.html)  (о mysql тоже есть с lvm)
[http://lists.andrew.cmu.edu/pipermail/info-cyrus/2005-September/019624.html](http://lists.andrew.cmu.edu/pipermail/info-cyrus/2005-September/019624.html)
[http://www.lissyara.su/articles/freebsd/mail/imapsync/](http://www.lissyara.su/articles/freebsd/mail/imapsync/)


Очень хорошая статья
[http://wiki.univention.de/index.php?title=Cool_Solution_-_Backup_Cyrus_mailserver](http://wiki.univention.de/index.php?title=Cool_Solution_-_Backup_Cyrus_mailserver)


Общий план backup cyrus

1. Копируем (rsync)
/var/spool/imap
/var/lib/imap
/var/lib/sieve

2.  Backup of mailboxes.db
3. Останавливаем cyrus, и опять копируем (rsync)
/var/spool/imap
/var/lib/imap
/var/lib/sieve
4.Запускаем cyrus

