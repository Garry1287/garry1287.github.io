---
layout: post
title:  "test-open-relay"
date:   2013-05-13 10:21:05 +0400
categories: mail
tags: mail
---

# test-open-relay
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
220 sapphire.sc.ru, ESMTP Server
EHLO 1
250-sapphire.sc.ru Hello 1 [127.0.0.1]
250-SIZE 25165824
250-PIPELINING
250-AUTH PLAIN LOGIN CRAM-MD5
250 HELP
MAIL FROM:<igordzu@yandex.ru>
250 OK
RCPT TO:<igordzu@yandex.ru>
250 Accepted

Если получите ответ "550 Relaying prohibited", то всё в порядке, Relay в CMS запрещён.
 При ответе "250 OK, recipient - <user@mail.ru>" Relay разрешён






Relaying test.
Attempting to connect to mail.sc.ru....

<<< 220 post.sc.ru, ESMTP Server
>>> EHLO www.test-smtp.com
<<< 250-post.sc.ru Hello www.test-smtp.com [91.194.96.35]
<<< 250-SIZE 25165824
<<< 250-PIPELINING
<<< 250-AUTH PLAIN LOGIN CRAM-MD5
<<< 250 HELP
>>> HELP
<<< 214-Commands supported:
<<< 214 AUTH HELO EHLO MAIL RCPT DATA NOOP QUIT RSET HELP
>>> AUTH LOGIN
<<< 334 VXNlcm5hbWU6
>>> AaAaAa
<<< 501 Invalid base64 data
>>> AaAaAa
<<< 500 unrecognized command
>>> VRFY postmaster
<<< 252 Administrative prohibition
>>> STARTTLS
<<< 503 STARTTLS command used when not advertised
>>> NOOP
<<< 250 OK
Test 1/28
>>> RSET
<<< 250 Reset OK
>>> MAIL FROM: <test@spam.com>
<<< 250 OK
>>> RCPT TO: <test@spam.com>
Error: host didn't reply on time
>>> NOOP
Connection lost
Attempting to connect to mail.sc.ru....
<<< 220 post.sc.ru, ESMTP Server
>>> EHLO www.test-smtp.com
<<< 250-post.sc.ru Hello www.test-smtp.com [91.194.96.35]
<<< 250-SIZE 25165824
<<< 250-PIPELINING
<<< 250-AUTH PLAIN LOGIN CRAM-MD5
<<< 250 HELP
Test 1/28
>>> RSET
<<< 250 Reset OK
>>> MAIL FROM: <test@spam.com>
<<< 250 OK
>>> RCPT TO: <test@spam.com>
Error: host didn't reply on time
>>> NOOP
Connection lost
Attempting to connect to mail.sc.ru....
<<< 220 post.sc.ru, ESMTP Server
>>> EHLO www.test-smtp.com
<<< 250-post.sc.ru Hello www.test-smtp.com [91.194.96.35]
<<< 250-SIZE 25165824
<<< 250-PIPELINING
<<< 250-AUTH PLAIN LOGIN CRAM-MD5
<<< 250 HELP
Test 1/28
>>> RSET
<<< 250 Reset OK
>>> MAIL FROM: <test@spam.com>
<<< 250 OK
>>> RCPT TO: <test@spam.com>
Error: host didn't reply on time
>>> NOOP
Connection lost
Attempting to connect to mail.sc.ru....
<<< 220 post.sc.ru, ESMTP Server
>>> EHLO www.test-smtp.com
<<< 250-post.sc.ru Hello www.test-smtp.com [91.194.96.35]
<<< 250-SIZE 25165824
<<< 250-PIPELINING
<<< 250-AUTH PLAIN LOGIN CRAM-MD5
<<< 250 HELP

Too many errors
CPU time: 0ms - LA: 0.91 - 21 SMTP requests - 3 disconnection(s)
Address: 81.20.192.9 - Reverse: emerald.sc.ru
ESMTP: yes - TLS: no - AUTH: yes - VRFY: no - MTA: Unknown
Average time : 0.09sec - Slowest : 0.15sec - Fastest : 0.07sec 







echo 'User-Name = ll0139' | radclient  -x 127.0.0.1:1645 status disconnect testing123
echo 'Message-Authenticator = 0x00' | radclient  -x 127.0.0.1:1645  status testing123
убил radutmp


       radclient  [-d  raddb_directory] [-c count] [-f file] [-i id] [-n num_requests_per_second] [-p num_requests_in_parallel] [-r num_retries] [-s] [-S
       shared_secret_file] [-t timeout] [-qvx] server {acct|auth|status|disconnect|auto} secret
radclient  [-d  raddb_directory] [-c count] [-f file] [-i id] [-n num_requests_per_second] [-p num_requests_in_parallel] [-r num_retries] [-s] [-S
       shared_secret_file] [-t timeout] [-qvx] server {acct|auth|status|disconnect|auto} secret



Failed to open a session for the virtual machine xp.

Implementation of the USB 2.0 controller not found!

Because the USB 2.0 controller state is part of the saved VM state, the VM cannot be started.
 To fix this problem, either install the 'Oracle VM VirtualBox Extension Pack' or disable USB 2.0 support in the VM settings (VERR_NOT_FOUND).

Result Code: NS_ERROR_FAILURE (0x80004005)
Component: Console
Interface: IConsole {1968b7d3-e3bf-4ceb-99e0-cb7c913317bb}




95.57.112.242.fazzt-admin

exim -bh 81.20.192.9


[http://tests.nettools.ru/](http://tests.nettools.ru/)

Имя: mailman.promsvyaz.ru
IP: 81.20.192.2


Подключение... OK
Запрос 	Ответ
	220 sapphire.sc.ru, ESMTP Server
Тест 1	
From: <spamtest@mail.nettools.ru>	250 OK
To: <relaytest@nettools.ru>	550 "It s not open relay ))"
Тест 2	
From: <spamtest>	501 : sender address must contain a domain
To: <relaytest@nettools.ru>	503 sender not yet given
Тест 3	
From: <>	250 OK
To: <relaytest@nettools.ru>	550 "It s not open relay ))"
Тест 4	
From: <spamtest@mail.nettools.ru>	250 OK
To: <relaytest@nettools.ru>	550 "It s not open relay ))"
Тест 5	
From: <spamtest@[194.87.98.220]>	501 : domain literals not allowed
To: <relaytest@nettools.ru>	503 sender not yet given
Тест 6	
From: <spamtest@mail.nettools.ru>	250 OK
To: <relaytest%nettools.ru@mail.nettools.ru>	550 "Unknown symbols in address"

Ошибка при получении данных [Connection reset by peer]
Тест 7	
From: <spamtest@mail.nettools.ru>	250 OK
To: <relaytest%nettools.ru@[194.87.98.220]>	501-: domain literals not allowed 501 Too many syntax or protocol errors

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 8	
From: <spamtest@mail.nettools.ru>	
To: <"relaytest@nettools.ru">	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 9	
From: <spamtest@mail.nettools.ru>	
To: <"relaytest%nettools.ru">	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 10	
From: <spamtest@mail.nettools.ru>	
To: <relaytest@nettools.ru@mail.nettools.ru>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 11	
From: <spamtest@mail.nettools.ru>	
To: <"relaytest@nettools.ru"@mail.nettools.ru>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 12	
From: <spamtest@mail.nettools.ru>	
To: <relaytest@nettools.ru@[194.87.98.220]>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 13	
From: <spamtest@mail.nettools.ru>	
To: <@mail.nettools.ru:relaytest@nettools.ru>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 14	
From: <spamtest@mail.nettools.ru>	
To: <@[194.87.98.220]:relaytest@nettools.ru>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 15	
From: <spamtest@mail.nettools.ru>	
To: <nettools.ru!relaytest>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 16	
From: <spamtest@mail.nettools.ru>	
To: <nettools.ru!relaytest@mail.nettools.ru>	

Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Ошибка при передачe данных [Broken pipe]
Тест 17	
From: <spamtest@mail.nettools.ru>	
To: <nettools.ru!relaytest@[194.87.98.220]>	

Все тесты пройдены успешно.
Сервер не является публичным пересыльщиком почты.






