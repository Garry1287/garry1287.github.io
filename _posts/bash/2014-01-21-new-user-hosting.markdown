---
layout: post
title:  "new-user-hosting"
date:   2014-01-21 20:27:16 +0400
categories: new-user-hosting
tags: new-user-hosting
---

# new-user-hosting
USERNAME=GROUPNAME

useradd -d /srv/www/USERNAME -p PASSWORD USERNAME
usermod -G GROUPNAME nginx

cd /srv/www/USERNAME
mkdir cgi-bin log public_html tmp
ln -s public_html www
chown -R USERNAME:USERNAME /srv/www/USERNAME

1. DNS
2. Apache+ngix
:%s/old/new/g

3. DB

mysql -u root -p

create database DBNAME;
GRANT ALL ON DBNAME.* TO dbuser@localhost IDENTIFIED BY 'somepassword';
flush privileges;

4. SSH

Match User USERNAME
    ChrootDirectory /srv/www/USERNAME
    AllowTCPForwarding no
    X11Forwarding no
    ForceCommand /usr/lib/openssh/sftp-server


# override default of no subsystems
#Subsystem      sftp    /usr/libexec/openssh/sftp-server
Subsystem sftp internal-sftp

# Example of overriding settings on a per-user basis
#Match User anoncvs
#       X11Forwarding no
#       AllowTcpForwarding no
#       ForceCommand cvs server

Match User usmmag
    ChrootDirectory /srv/www/usmmag
    AllowTCPForwarding no
    X11Forwarding no
    ForceCommand internal-sftp

Match User usm-mag 
    ChrootDirectory /srv/www/usm-mag
    AllowTCPForwarding no
    X11Forwarding no
    ForceCommand internal-sftp





 mysqldump -u root -p iptech48 > /srv/www/iptech48.sql
 mysqldump -u root -p potolok > /srv/www/potolok.sql
scp -P 2222 *.sql garry@192.168.1.141:/home/garry/seo






GRANT ALL ON usmmag.* TO usmmag@localhost IDENTIFIED BY 'Edv83Hdv';
flush privileges;
GRANT ALL ON usmmag2.* TO usmmag2@localhost IDENTIFIED BY 'Edv83Hdv';
flush privileges;
Rad35Gdv