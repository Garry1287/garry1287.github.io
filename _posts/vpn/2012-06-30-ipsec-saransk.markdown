---
layout: post
title:  "ipsec-saransk"
date:   2012-06-30 14:37:59 +0400
categories: vpn
tags: vpn
---

# ipsec-saransk
Phase: 7
Type: VPN
Subtype: encrypt
Result: DROP
Config:
Additional Information:
 Forward Flow based lookup yields rule:
 out id=0xac57ee18, priority=70, domain=encrypt, deny=false
        hits=0, user_data=0x0, cs_id=0xac860db8, reverse, flags=0x0, protocol=0
        src ip=172.28.0.0, mask=255.255.255.0, port=0
        dst ip=10.113.1.128, mask=255.255.255.192, port=0, dscp=0x0




192.168.64.8



config lacp_ports 1-28 mode passive
config link_aggregation algorithm mac_source
create link_aggregation group_id 1 type lacp
config link_aggregation group_id 1 master_port 25 ports 25,27 state enable



26 переключить в 27



access-list PSI-Saransk extended permit ip 172.28.0.0 255.255.255.0 10.113.1.128 255.255.255.192


Dec 19 15:49:51 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Can't find a valid tunnel group, aborting...!
Dec 19 15:49:51 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Removing peer from peer table failed, no match!
Dec 19 15:49:51 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Error: Unable to remove PeerTblEntry



tunnel-group Saransk-IP type ipsec-l2l
tunnel-group Saransk-IP ipsec-attributes
 pre-shared-key Kup3qbTehODji5opUgxk
 isakmp keepalive threshold 3600 retry 2



crypto map PSI-White_map 1 match address PSI-White_1_cryptomap
crypto map PSI-White_map 1 set peer 80.75.128.2 
crypto map PSI-White_map 1 set security-association lifetime seconds 3600
crypto map PSI-White_map 2 match address PSI-White_2_cryptomap
crypto map PSI-White_map 2 set pfs group1
crypto map PSI-White_map 2 set peer Start-IP-SEC 
crypto map PSI-White_map 3 match address CRYPTO-TEST
crypto map PSI-White_map 3 set pfs group1
crypto map PSI-White_map 3 set peer 81.20.192.58 
crypto map PSI-White_map 3 set security-association lifetime seconds 3600
crypto map PSI-White_map 4 match address IPSEC_NLMK.KVK
crypto map PSI-White_map 4 set pfs group1
crypto map PSI-White_map 4 set peer ipsec.nlmk 
crypto map PSI-White_map 4 set security-association lifetime seconds 3600
crypto map PSI-White_map 4 set nat-t-disable
crypto map PSI-White_map 5 match address PSI-Saransk
crypto map PSI-White_map 5 set pfs 
crypto map PSI-White_map 5 set peer Saransk-IP 
crypto map PSI-White_map 5 set security-association lifetime seconds 3600
crypto map PSI-White_map interface PSI-White



Dec 19 14:46:02 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Can't find a valid tunnel group, aborting...!
Dec 19 14:46:02 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Removing peer from peer table failed, no match!
Dec 19 14:46:02 [IKEv1]: Group = 31.204.98.143, IP = 31.204.98.143, Error: Unable to remove PeerTblEntry
Dec 19 14:46:12 [IKEv1]: IP = 31.204.98.143, Header invalid, missing SA payload! (next payload = 4)
















192.168.117.1
192.168.118.1
192.168.120.1
192.168.121.1
192.168.122.1
192.168.123.1
172.28.0.8

192.168.124.1
255.255.252.0


192.168.253.48/30
10.148.0.0/16
192.168.117.0/24
192.168.118.0/24
192.168.120.0/21
172.28.0.0/24


sh cry isa sa (первичный туннель)
sh cry ipsec sa (туннель для данных)
- sh cry ipsec sa det, sh vpn-sessiondb det l2l


Пункт 1.

Transform set (уже настроен)
crypto ipsec transform-set ESP-DES-SHA esp-des esp-sha-hmac 
crypto ipsec security-association lifetime seconds 3600
crypto ipsec security-association lifetime kilobytes 4608000


ESP-DES-SHA - это просто название transform-set
esp-des - это Encryption Protocol пункт 9
esp-sha-hmac - это MAC-Algorithm for Authentication пункт 10



crypto isakmp policy 10
 authentication pre-share
 encryption aes-256
 hash sha
 group 2
 lifetime 86400

31.204.98.143






crypto map PSI-White_map 5 match address PSI-Saransk 
crypto map PSI-White_map 5 set pfs group2
crypto map PSI-White_map 5 set peer Saransk-IP 
crypto map PSI-White_map 5 set security-association lifetime seconds 3600





tunnel-group Saransk-IP type ipsec-l2l
tunnel-group Saransk-IP ipsec-attributes
 pre-shared-key Kup3qbTehODji5opUgxk
 isakmp keepalive threshold 3600 retry 2


ACL - для сетей


access-list PSI-Saransk extended permit ip object-group PSI-SHPD object-group Sarank 
access-list PSI-Saransk extended permit ip object-group Sarank object-group PSI-SHPD



name 31.204.98.143 Saransk-IP


object-group network PSI_shpd
object-group network SHPD





crypto ipsec transform-set ESP-AES-256 esp-aes-256 esp-sha-hmac 



crypto isakmp policy 20
 authentication pre-share
 encryption 3des
 hash sha     
 group 2      
 lifetime 86400



no crypto map PSI-Sar_map 1 match address PSI-Saransk
no crypto map PSI-Sar_map 1 set pfs group1
no crypto map PSI-Sar_map 1 set peer Saransk-IP 
no crypto map PSI-Sar_map 1 set security-association lifetime seconds 3600

crypto map PSI-White_map 5 match address PSI-Saransk
crypto map PSI-White_map 5 set pfs group1
crypto map PSI-White_map 5 set peer Saransk-IP 
crypto map PSI-White_map 5 set security-association lifetime seconds 3600

crypto map PSI-White_map interface PSI-White











адрес 31.204.98.143
source 10.113.1.128/26


#phase1 Saransk
remote 31.204.98.143
{
        exchange_mode main,aggressive;
        doi ipsec_doi;
        situation identity_only;

        my_identifier address 81.20.192.19;
        #certificate_type x509 "my.cert.pem" "my.key.pem";

        #nonce_size 16;
        lifetime time  1440 min;
        initial_contact on;
        proposal_check obey;    # obey, strict, or claim

        proposal {
                encryption_algorithm 3des;
                hash_algorithm sha1;
                authentication_method pre_shared_key;
                dh_group 2;
        }
}

#phase2 Saransk
sainfo address 10.148.0.0/16 any address 10.113.1.128/26 any
{
       pfs_group 2;
       lifetime time 3600 sec;
       encryption_algorithm 3des;
       authentication_algorithm hmac_sha1;
       compression_algorithm deflate;
}
sainfo address 192.168.253.48/30 any address 10.113.1.128/26 any
{
       pfs_group 2;
       lifetime time 3600 sec;
       encryption_algorithm 3des;
       authentication_algorithm hmac_sha1;
       compression_algorithm deflate;
}




# Saransk
spdadd 192.168.253.48/30 10.113.1.128/26 any -P out ipsec esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 10.148.0.0/16 10.113.1.128/26 any -P out ipsec esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 192.168.253.48/30 10.113.1.128/26 any -P fwd ipsec esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 10.148.0.0/16 10.113.1.128/26 any -P fwd ipsec esp/tunnel/81.20.192.19-31.204.98.143/require;

spdadd 10.113.1.128/26 192.168.253.48/30 any -P in ipsec esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 10.148.0.0/16 any -P in ipsec esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 192.168.253.48/30 any -P fwd ipsec esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 10.148.0.0/16 any -P fwd ipsec esp/tunnel/31.204.98.143-81.20.192.19/require;




iptables -A INPUT -s 31.204.98.143/32 -p esp -j ACCEPT
iptables -A INPUT -s 31.204.98.143/32 -p ah -j ACCEPT
iptables -A allow_ports -p udp -m udp --dport 500 -j ACCEPT



31.204.98.143

10.113.1.169















На ap добавил маршруты

10.113.1.128/26

/sbin/route add -net 10.113.1.0 netmask 255.255.255.0 gw 10.148.0.8

-------- Перенаправленное сообщение --------
Тема: 	Re: IPSEC
Дата: 	Mon, 15 Dec 2014 15:38:14 +0300
От: 	Рачков Тимур <t.rachkov@sar.starttelecom.ru>
Кому: 	Игорь Дзюин <i.dzuin@promsvyaz.ru>


spdadd 10.13.0.2/32 10.113.1.0/24 any -P out ipsec 
esp/tunnel/31.204.98.37-31.204.98.143/require;
spdadd 10.113.1.0/24 10.13.0.2/32 any -P in ipsec 
esp/tunnel/31.204.98.38-31.204.98.143/require;

Здравствуйте,

В фаерволе всё разрешено



#phase1 Saransk
remote 31.204.98.143
{
         exchange_mode main,aggressive;
         doi ipsec_doi;
         situation identity_only;

         my_identifier address 81.20.192.19;
         #certificate_type x509 "my.cert.pem" "my.key.pem";

         #nonce_size 16;
         lifetime time  1440 min;
         initial_contact on;
         proposal_check obey;    # obey, strict, or claim

         proposal {
                 encryption_algorithm 3des;
                 hash_algorithm sha1;
                 authentication_method pre_shared_key;
                 dh_group 2;
         }
}

#phase2 Saransk
sainfo address 10.148.0.0/16 any address 10.113.1.128/26 any
{
        pfs_group 2;
        lifetime time 3600 sec;
        encryption_algorithm 3des;
        authentication_algorithm hmac_sha1;
        compression_algorithm deflate;
}
sainfo address 192.168.253.48/30 any address 10.113.1.128/26 any
{
        pfs_group 2;
        lifetime time 3600 sec;
        encryption_algorithm 3des;
        authentication_algorithm hmac_sha1;
        compression_algorithm deflate;
}




# Saransk
spdadd 192.168.253.48/30 10.113.1.128/26 any -P out ipsec 
esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 10.148.0.0/16 10.113.1.128/26 any -P out ipsec 
esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 192.168.253.48/30 10.113.1.128/26 any -P fwd ipsec 
esp/tunnel/81.20.192.19-31.204.98.143/require;
spdadd 10.148.0.0/16 10.113.1.128/26 any -P fwd ipsec 
esp/tunnel/81.20.192.19-31.204.98.143/require;

spdadd 10.113.1.128/26 192.168.253.48/30 any -P in ipsec 
esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 10.148.0.0/16 any -P in ipsec 
esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 192.168.253.48/30 any -P fwd ipsec 
esp/tunnel/31.204.98.143-81.20.192.19/require;
spdadd 10.113.1.128/26 10.148.0.0/16 any -P fwd ipsec 
esp/tunnel/31.204.98.143-81.20.192.19/require;















sainfo address 192.168.117.0/24 any address 10.113.1.128/26 any
{
      pfs_group 2;
       lifetime time 3600 sec;
      encryption_algorithm 3des;
      authentication_algorithm hmac_sha1;
     compression_algorithm deflate;
}


sainfo address 192.168.118.0/24 any address 10.113.1.128/26 any
{
      pfs_group 2;
       lifetime time 3600 sec;
      encryption_algorithm 3des;
      authentication_algorithm hmac_sha1;
     compression_algorithm deflate;
}


sainfo address 192.168.120.0/21 any address 10.113.1.128/26 any
{
      pfs_group 2;
       lifetime time 3600 sec;
      encryption_algorithm 3des;
      authentication_algorithm hmac_sha1;
     compression_algorithm deflate;
}



sainfo address 172.28.0.0/24 any address 10.113.1.128/26 any
{
      pfs_group 2;
       lifetime time 3600 sec;
      encryption_algorithm 3des;
      authentication_algorithm hmac_sha1;
     compression_algorithm deflate;
}





supplied indices
поставляемые идексы (указатели)




Помогает 

killall -9 racoon
/etc/init.d/racoon stop
setkey -F
setkey -FP
/etc/init.d/racoon start


Dec 23 15:03:35 sapphire racoon: DEBUG: ignore the acquire because ph2 found


Dec 23 15:06:24 sapphire racoon: ERROR: fatal NO-PROPOSAL-CHOSEN notify messsage, phase1 should be deleted.
Dec 23 15:06:24 sapphire racoon: DEBUG: notification message 14:NO-PROPOSAL-CHOSEN, doi=1 proto_id=3 spi=00f1f2ed(size=4).
Dec 23 15:06:24 sapphire racoon: ERROR: Message: '4 B: E hs E E hE A `E '.







[http://www.opennet.ru/openforum/vsluhforumID1/85478.html](http://www.opennet.ru/openforum/vsluhforumID1/85478.html)

>gsmrouter# less /usr/local/etc/racoon/ipsec.conf
>flush;
>spdflush;
>
>spdadd 10.112.223.224/27 172.16.0.0/24 any -P out ipsec esp/tunnel/yyy.yyy.yyy.yyy-xxx.xxx.xxx.xxx/require;
>spdadd 172.16.0.0/24 10.112.223.224/27 any -P in ipsec esp/tunnel/xxx.xxx.xxx.xxx-yyy.yyy.yyy.yyy/require;
>
>spdadd 10.112.223.224/27 10.111.0.0/19 any -P out ipsec esp/tunnel/yyy.yyy.yyy.yyy-xxx.xxx.xxx.xxx/require;
>spdadd 10.111.0.0/19 10.112.223.224/27 any -P in ipsec esp/tunnel/xxx.xxx.xxx.xxx-yyy.yyy.yyy.yyy/require;

Проблема решилась заменой require на unique. Всем спасибо!




Между linux и pix
[http://www.opennet.ru/base/net/ipsec_linux_pix.txt.html](http://www.opennet.ru/base/net/ipsec_linux_pix.txt.html)
[http://www.opennet.ru/base/cisco/cisco_freebsd_ipsec.txt.html](http://www.opennet.ru/base/cisco/cisco_freebsd_ipsec.txt.html)
