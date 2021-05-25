---
layout: post
title:  "asterisk-openwrt"
date:   2011-09-07 21:50:52 +0400
categories: voip
tags: voip
---

# asterisk-openwrt
opkg update
opkg install asterisk18 asterisk18-codec-alaw asterisk18-chan-iax2 asterisk-gui
/etc/init.d/asterisk enable
редактируем /etc/asterisk/manager.conf, меняем пароль для admin-а на панель и
стартуем астериск
/etc/init.d/asterisk start




Mikrotik RB2011UAS:
CPU: 600Mhz
RAM: 128Mb
RouterOS: 6.2
NAT, Firewall, connection tracking
Metarouter: Linux metarouter 2.6.31.10, Asterisk 1.8.11.1
Параметры приложения sipp:
./sipp 172.25.26.40 -s 100 -i 172.25.26.16 -d 30s -l 4 -aa -mi 172.25.26.16 -
rtp_echo -nd -r 1
Генератор сетевого трафика Bandwidth test – 10Mbps full duplex



[sipp]
type=friend
context=in
defaultuser=sipp
host=xxx.xxx.xxx.xxx
dtmfmode=rfc2833
disallow=all
allow=ulaw
insecure=port,invite
qualify=yes
Терминация в Playback
[in]
exten=100,1,Answer
exten=100,n,Playback(moh1)
exten=100,n,Hangup



Asterisk взламывают каждый день из-за кривых рук админов
Закрыть файрволлом
Использовать приватную адресацию
Отключить анонимные звонки
Ограничить регистрацию extenstions со доверенных IP
Ограничить кол-во одновременных звонков на extension
Убрать на openwrt default gateway



VoIP трафику нужно дать приоритет
Создать queue simple/tree по критерию IP-адресов, номеров портов,
DSCP
Дать высший приоритет Priority и минимально гарантированную
скорость CIR


VoIP в виртуальной среде Mikrotik работает стабильно для количества
одновременных звонков до 10 (RB951, RB2011) и более (для x86)
Общее кол-во extenstions в сети может быть до 40-50!!!
Реализовать можно только базовые функции: звонки,
перенаправление, запись
Продвинутые функции: call center, работа с БД – не потянет
Есть проблемы со стабильностью MetaROUTER – редкие зависания,
самопроизвольные перезагрузки рутера RB2011
Не хватает встроенных портов FXS на RouterBOARD – нужно
использовать ATA, IP-телефоны, софтфоны



[https://www.linux.com/news/asterisk-openwrt/](https://www.linux.com/news/asterisk-openwrt/)
[https://openwrt.org/docs/guide-user/services/voip/asterisk](https://openwrt.org/docs/guide-user/services/voip/asterisk)



как соединиться - friend peer?
Простая ATC на ast
[https://serveradmin.ru/nastroyka-servera-telefonii-asterisk-s-nulya/](https://serveradmin.ru/nastroyka-servera-telefonii-asterisk-s-nulya/)
[https://habr.com/ru/post/113707/](https://habr.com/ru/post/113707/)

[https://new-tel.net/support/asterisk-ats-instruktsiya-po-nastroyke/](https://new-tel.net/support/asterisk-ats-instruktsiya-po-nastroyke/)
[https://wiki.merionet.ru/ip-telephoniya/72/asterisk-nastrojka-s-nulya/](https://wiki.merionet.ru/ip-telephoniya/72/asterisk-nastrojka-s-nulya/)

[https://jakondo.ru/bazovaya-nastrojka-sip-ats-asterisk-dlya-nebolshogo-ofisa/](https://jakondo.ru/bazovaya-nastrojka-sip-ats-asterisk-dlya-nebolshogo-ofisa/)





asterisk16 - 16.3.0-7 - Asterisk is a complete PBX in software. It provides all of the features you would expect from a PBX and more. Asterisk does voice over IP in three protocols, and can interoperate with almost all standards-based telephony equipment using relatively inexpensive hardware.
asterisk16-app-adsiprog - 16.3.0-7 - Asterisk ADSI programming application.
asterisk16-app-agent-pool - 16.3.0-7 - Call center agent pool applications.
asterisk16-app-alarmreceiver - 16.3.0-7 - Alarm receiver for Asterisk.
asterisk16-app-amd - 16.3.0-7 - Answering Machine Detection application.
asterisk16-app-authenticate - 16.3.0-7 - Authentication application.
asterisk16-app-bridgeaddchan - 16.3.0-7 - Bridge-add-channel application.
asterisk16-app-bridgewait - 16.3.0-7 - Application to place a channel into a holding bridge.
asterisk16-app-celgenuserevent - 16.3.0-7 - Generate a user defined CEL event.
asterisk16-app-chanisavail - 16.3.0-7 - Check channel availability.
asterisk16-app-channelredirect - 16.3.0-7 - Redirects a given channel to a dialplan target.
asterisk16-app-chanspy - 16.3.0-7 - Listen to the audio of an active channel.
asterisk16-app-confbridge - 16.3.0-7 - Conference bridge application.
asterisk16-app-controlplayback - 16.3.0-7 - Control playback application.
asterisk16-app-dahdiras - 16.3.0-7 - DAHDI ISDN Remote Access Server.
asterisk16-app-dictate - 16.3.0-7 - Virtual dictation machine.
asterisk16-app-directed-pickup - 16.3.0-7 - Directed call pickup application.
asterisk16-app-directory - 16.3.0-7 - Extension directory.
asterisk16-app-disa - 16.3.0-7 - Direct Inward System Access application.
asterisk16-app-dumpchan - 16.3.0-7 - Dump info about the calling channel.
asterisk16-app-exec - 16.3.0-7 - Executes dialplan applications.
asterisk16-app-externalivr - 16.3.0-7 - External IVR interface application.
asterisk16-app-festival - 16.3.0-7 - Simple Festival interface.
asterisk16-app-flash - 16.3.0-7 - Flash channel application.
asterisk16-app-followme - 16.3.0-7 - Find-Me/Follow-Me application.
asterisk16-app-getcpeid - 16.3.0-7 - Get ADSI CPE ID.
asterisk16-app-ices - 16.3.0-7 - Encode and stream via Icecast and IceS.
asterisk16-app-image - 16.3.0-7 - Image transmission application.
asterisk16-app-ivrdemo - 16.3.0-7 - IVR demo application.
asterisk16-app-milliwatt - 16.3.0-7 - Digital milliwatt test application.
asterisk16-app-minivm - 16.3.0-7 - A minimal voicemail e-mail system.
asterisk16-app-mixmonitor - 16.3.0-7 - Mixed audio monitoring application.
asterisk16-app-morsecode - 16.3.0-7 - Morse code.
asterisk16-app-mp3 - 16.3.0-7 - Silly MP3 application.
asterisk16-app-originate - 16.3.0-7 - Originate call.
asterisk16-app-page - 16.3.0-7 - Page multiple phones.
asterisk16-app-playtones - 16.3.0-7 - Playtones application.
asterisk16-app-privacy - 16.3.0-7 - Require phone number to be entered if no Caller ID sent.
asterisk16-app-queue - 16.3.0-7 - True call queueing.
asterisk16-app-read - 16.3.0-7 - Read variable application.
asterisk16-app-readexten - 16.3.0-7 - Read and evaluate extension validity.
asterisk16-app-record - 16.3.0-7 - Trivial record application.
asterisk16-app-saycounted - 16.3.0-7 - Decline words according to channel language.
asterisk16-app-sayunixtime - 16.3.0-7 - Say time.
asterisk16-app-senddtmf - 16.3.0-7 - Send DTMF digits application.
asterisk16-app-sendtext - 16.3.0-7 - Send text applications.
asterisk16-app-skel - 16.3.0-7 - Skeleton application.
asterisk16-app-sms - 16.3.0-7 - SMS/PSTN handler.
asterisk16-app-softhangup - 16.3.0-7 - Hangs up the requested channel.
asterisk16-app-speech - 16.3.0-7 - Dialplan speech applications.
asterisk16-app-stack - 16.3.0-7 - Dialplan subroutines.
asterisk16-app-stasis - 16.3.0-7 - Stasis dialplan application.
asterisk16-app-statsd - 16.3.0-7 - StatsD dialplan application.
asterisk16-app-stream-echo - 16.3.0-7 - Stream echo application.
asterisk16-app-system - 16.3.0-7 - Generic system application.
asterisk16-app-talkdetect - 16.3.0-7 - Playback with talk detection.
asterisk16-app-test - 16.3.0-7 - Interface test application.
asterisk16-app-transfer - 16.3.0-7 - Transfers a caller to another extension.
asterisk16-app-url - 16.3.0-7 - Send URL applications.
asterisk16-app-userevent - 16.3.0-7 - Custom user event application.
asterisk16-app-verbose - 16.3.0-7 - Send verbose output.
asterisk16-app-waitforring - 16.3.0-7 - Waits until first ring after time.
asterisk16-app-waitforsilence - 16.3.0-7 - Wait for silence/noise.
asterisk16-app-waituntil - 16.3.0-7 - Wait until specified time.
asterisk16-app-while - 16.3.0-7 - While loops and conditional execution.
asterisk16-app-zapateller - 16.3.0-7 - Block telemarketers with special information tone.
asterisk16-bridge-builtin-features - 16.3.0-7 - Built in bridging features.
asterisk16-bridge-builtin-interval-features - 16.3.0-7 - Built in bridging interval features.
asterisk16-bridge-holding - 16.3.0-7 - Holding bridge module.
asterisk16-bridge-native-rtp - 16.3.0-7 - Native RTP bridging module.
asterisk16-bridge-simple - 16.3.0-7 - Simple two channel bridging module.
asterisk16-bridge-softmix - 16.3.0-7 - Multi-party software based channel mixing.
asterisk16-cdr - 16.3.0-7 - Call Detail Records.
asterisk16-cdr-csv - 16.3.0-7 - Comma Separated Values CDR backend.
asterisk16-cdr-sqlite3 - 16.3.0-7 - SQLite3 CDR backend.
asterisk16-cel-custom - 16.3.0-7 - Customizable Comma Separated Values CEL backend.
asterisk16-cel-manager - 16.3.0-7 - Asterisk Manager Interface CEL backend.
asterisk16-cel-sqlite3-custom - 16.3.0-7 - SQLite3 custom CEL module.
asterisk16-chan-alsa - 16.3.0-7 - ALSA console channel driver.
asterisk16-chan-bridge-media - 16.3.0-7 - Bridge media channel driver.
asterisk16-chan-console - 16.3.0-7 - Console channel driver.
asterisk16-chan-dahdi - 16.3.0-7 - DAHDI telephony.
asterisk16-chan-dongle - 1.1-20180619-1 - Asterisk channel driver for Huawei UMTS 3G dongle.
asterisk16-chan-iax2 - 16.3.0-7 - Inter Asterisk eXchange.
asterisk16-chan-mgcp - 16.3.0-7 - Media Gateway Control Protocol.
asterisk16-chan-mobile - 16.3.0-7 - Bluetooth mobile device channel driver.
asterisk16-chan-motif - 16.3.0-7 - Motif Jingle channel driver.
asterisk16-chan-ooh323 - 16.3.0-7 - Objective Systems H.323 channel.
asterisk16-chan-oss - 16.3.0-7 - OSS console channel driver.
asterisk16-chan-phone - 16.3.0-7 - Linux telephony API support.
asterisk16-chan-rtp - 16.3.0-7 - RTP media channel.
asterisk16-chan-sccp - v4.3.2-20190411-2 - Replacement for the SCCP channel driver (chan_skinny) in Asterisk. Extended features include shared lines, presence / BLF, customizable feature buttons and custom device state.
asterisk16-chan-sip - 16.3.0-7 - Session Initiation Protocol.
asterisk16-chan-skinny - 16.3.0-7 - Skinny Client Control Protocol.
asterisk16-chan-unistim - 16.3.0-7 - UNISTIM protocol.
asterisk16-codec-a-mu - 16.3.0-7 - Alaw and ulaw direct coder/decoder.
asterisk16-codec-adpcm - 16.3.0-7 - Adaptive Differential PCM coder/decoder.
asterisk16-codec-alaw - 16.3.0-7 - Alaw coder/decoder.
asterisk16-codec-dahdi - 16.3.0-7 - Generic DAHDI transcoder codec translator.
asterisk16-codec-g722 - 16.3.0-7 - ITU G.722-64kbps G722 transcoder.
asterisk16-codec-g726 - 16.3.0-7 - ITU G.726-32kbps G726 transcoder.
asterisk16-codec-g729 - 1.4.3-1 - Asterisk G.729 codec based on bcg729 implementation.
asterisk16-codec-gsm - 16.3.0-7 - GSM coder/decoder.
asterisk16-codec-ilbc - 16.3.0-7 - iLBC coder/decoder.
asterisk16-codec-lpc10 - 16.3.0-7 - LPC10 2.4kbps coder/decoder.
asterisk16-codec-opus - 20171009-1 - Opus is the default audio codec in WebRTC. WebRTC is available in Asterisk via SIP over WebSockets (WSS). Nevertheless, Opus can be used for other transports (UDP, TCP, TLS) as well. Opus supersedes previous codecs like CELT and SiLK. Furthermore, in favor of Opus, other open-source audio codecs are no longer developed, like Speex, iSAC, iLBC, and Siren. If you use your Asterisk as a back-to-back user agent (B2BUA) and you transcode between various audio codecs, one should enable Opus for future compatibility.  Opus is not only supported for pass-through but can be transcoded as well.
asterisk16-codec-resample - 16.3.0-7 - SLIN resampling codec.
asterisk16-codec-ulaw - 16.3.0-7 - Ulaw coder/decoder.
asterisk16-curl - 16.3.0-7 - cURL support
asterisk16-format-g719 - 16.3.0-7 - ITU G.719.
asterisk16-format-g723 - 16.3.0-7 - G.723.1 simple timestamp file format.
asterisk16-format-g726 - 16.3.0-7 - Raw G.726 data.
asterisk16-format-g729 - 16.3.0-7 - Raw G.729 data.
asterisk16-format-gsm - 16.3.0-7 - Raw GSM data.
asterisk16-format-h263 - 16.3.0-7 - Raw H.263 data.
asterisk16-format-h264 - 16.3.0-7 - Raw H.264 data.
asterisk16-format-ilbc - 16.3.0-7 - Raw iLBC data.
asterisk16-format-ogg-vorbis - 16.3.0-7 - OGG/Vorbis audio.
asterisk16-format-pcm - 16.3.0-7 - Raw/Sun ulaw/alaw 8KHz and G.722 16Khz.
asterisk16-format-siren14 - 16.3.0-7 - ITU G.722.1 Annex C.
asterisk16-format-siren7 - 16.3.0-7 - ITU G.722.1.
asterisk16-format-sln - 16.3.0-7 - Raw signed linear audio support 8khz-192khz.
asterisk16-format-vox - 16.3.0-7 - Dialogic VOX file format.
asterisk16-format-wav - 16.3.0-7 - Microsoft WAV/WAV16 format.
asterisk16-format-wav-gsm - 16.3.0-7 - Microsoft WAV format.
asterisk16-func-aes - 16.3.0-7 - AES dialplan functions.
asterisk16-func-base64 - 16.3.0-7 - Base64 encode/decode dialplan functions.
asterisk16-func-blacklist - 16.3.0-7 - Look up Caller ID name/number from blacklist database.
asterisk16-func-callcompletion - 16.3.0-7 - Call control configuration function.
asterisk16-func-channel - 16.3.0-7 - Channel information dialplan functions.
asterisk16-func-config - 16.3.0-7 - Asterisk configuration file variable access.
asterisk16-func-cut - 16.3.0-7 - Cut out information from a string.
asterisk16-func-db - 16.3.0-7 - Database related dialplan functions.
asterisk16-func-devstate - 16.3.0-7 - Gets or sets a device state in the dialplan.
asterisk16-func-dialgroup - 16.3.0-7 - Dialgroup dialplan function.
asterisk16-func-dialplan - 16.3.0-7 - Dialplan context/extension/priority checking functions.
asterisk16-func-enum - 16.3.0-7 - ENUM related dialplan functions.
asterisk16-func-env - 16.3.0-7 - Environment/filesystem dialplan functions.
asterisk16-func-extstate - 16.3.0-7 - Gets the state of an extension in the dialplan.
asterisk16-func-frame-trace - 16.3.0-7 - Frame trace for internal ast_frame debugging.
asterisk16-func-global - 16.3.0-7 - Variable dialplan functions.
asterisk16-func-groupcount - 16.3.0-7 - Channel group dialplan functions.
asterisk16-func-hangupcause - 16.3.0-7 - Hangup cause related functions and applications.
asterisk16-func-holdintercept - 16.3.0-7 - Hold interception dialplan function.
asterisk16-func-iconv - 16.3.0-7 - Charset conversions.
asterisk16-func-jitterbuffer - 16.3.0-7 - Jitter buffer for read side of channel.
asterisk16-func-lock - 16.3.0-7 - Dialplan mutexes.
asterisk16-func-math - 16.3.0-7 - Mathematical dialplan function.
asterisk16-func-md5 - 16.3.0-7 - MD5 digest dialplan functions.
asterisk16-func-module - 16.3.0-7 - Checks if Asterisk module is loaded in memory.
asterisk16-func-periodic-hook - 16.3.0-7 - Periodic dialplan hooks.
asterisk16-func-pitchshift - 16.3.0-7 - Audio effects dialplan functions.
asterisk16-func-presencestate - 16.3.0-7 - Gets or sets a presence state in the dialplan.
asterisk16-func-rand - 16.3.0-7 - Random number dialplan function.
asterisk16-func-realtime - 16.3.0-7 - Read/write/store/destroy values from a realtime repository.
asterisk16-func-sha1 - 16.3.0-7 - SHA-1 computation dialplan function.
asterisk16-func-shell - 16.3.0-7 - Collects the output generated by a command executed by the system shell.
asterisk16-func-sorcery - 16.3.0-7 - Get a field from a sorcery object.
asterisk16-func-sprintf - 16.3.0-7 - SPRINTF dialplan function.
asterisk16-func-srv - 16.3.0-7 - SRV related dialplan functions.
asterisk16-func-sysinfo - 16.3.0-7 - System information related functions.
asterisk16-func-talkdetect - 16.3.0-7 - Talk detection dialplan function.
asterisk16-func-uri - 16.3.0-7 - URI encode/decode dialplan functions.
asterisk16-func-version - 16.3.0-7 - Get Asterisk version/build info.
asterisk16-func-vmcount - 16.3.0-7 - Indicator for whether a voice mailbox has messages in a given folder.
asterisk16-func-volume - 16.3.0-7 - Technology independent volume control.
asterisk16-odbc - 16.3.0-7 - ODBC support.
asterisk16-pbx-ael - 16.3.0-7 - Asterisk Extension Language compiler.
asterisk16-pbx-dundi - 16.3.0-7 - Distributed Universal Number Discovery.
asterisk16-pbx-loopback - 16.3.0-7 - Loopback switch.
asterisk16-pbx-lua - 16.3.0-7 - Lua PBX switch.
asterisk16-pbx-realtime - 16.3.0-7 - Realtime switch.
asterisk16-pbx-spool - 16.3.0-7 - Outgoing spool support.
asterisk16-pgsql - 16.3.0-7 - PostgreSQL support.
asterisk16-pjsip - 16.3.0-7 - PJSIP SIP stack.
asterisk16-res-adsi - 16.3.0-7 - ADSI resource.
asterisk16-res-ael-share - 16.3.0-7 - Shareable code for AEL.
asterisk16-res-agi - 16.3.0-7 - Asterisk Gateway Interface.
asterisk16-res-ari - 16.3.0-7 - Asterisk RESTful Interface.
asterisk16-res-ari-applications - 16.3.0-7 - RESTful API module - Stasis application resources.
asterisk16-res-ari-asterisk - 16.3.0-7 - RESTful API module - Asterisk resources.
asterisk16-res-ari-bridges - 16.3.0-7 - RESTful API module - bridge resources.
asterisk16-res-ari-channels - 16.3.0-7 - RESTful API module - channel resources.
asterisk16-res-ari-device-states - 16.3.0-7 - RESTful API module - device state resources.
asterisk16-res-ari-endpoints - 16.3.0-7 - RESTful API module - endpoint resources.
asterisk16-res-ari-events - 16.3.0-7 - RESTful API module - WebSocket resource.
asterisk16-res-ari-mailboxes - 16.3.0-7 - RESTful API module - mailboxes resources.
asterisk16-res-ari-model - 16.3.0-7 - ARI model validators.
asterisk16-res-ari-playbacks - 16.3.0-7 - RESTful API module - playback control resources.
asterisk16-res-ari-recordings - 16.3.0-7 - RESTful API module - recording resources.
asterisk16-res-ari-sounds - 16.3.0-7 - RESTful API module - sound resources.
asterisk16-res-calendar - 16.3.0-7 - Asterisk calendar integration.
asterisk16-res-calendar-caldav - 16.3.0-7 - Asterisk CalDAV calendar integration.
asterisk16-res-calendar-ews - 16.3.0-7 - Asterisk MS Exchange Web Service calendar integration.
asterisk16-res-calendar-exchange - 16.3.0-7 - Asterisk MS Exchange calendar integration.
asterisk16-res-calendar-icalendar - 16.3.0-7 - Asterisk iCalendar .ics file integration.
asterisk16-res-chan-stats - 16.3.0-7 - Example of how to use Stasis.
asterisk16-res-clialiases - 16.3.0-7 - CLI aliases.
asterisk16-res-clioriginate - 16.3.0-7 - Call origination and redirection from the CLI.
asterisk16-res-config-ldap - 16.3.0-7 - LDAP realtime interface.
asterisk16-res-config-mysql - 16.3.0-7 - MySQL realtime configuration driver.
asterisk16-res-config-sqlite3 - 16.3.0-7 - SQLite3 realtime config engine.
asterisk16-res-convert - 16.3.0-7 - File format conversion CLI command.
asterisk16-res-endpoint-stats - 16.3.0-7 - Endpoint statistics.
asterisk16-res-fax - 16.3.0-7 - Generic FAX applications.
asterisk16-res-fax-spandsp - 16.3.0-7 - Spandsp G.711 and T.38 FAX technologies.
asterisk16-res-format-attr-celt - 16.3.0-7 - CELT format attribute module.
asterisk16-res-format-attr-g729 - 16.3.0-7 - G.729 format attribute module.
asterisk16-res-format-attr-h263 - 16.3.0-7 - H.263 format attribute module.
asterisk16-res-format-attr-h264 - 16.3.0-7 - H.264 format attribute module.
asterisk16-res-format-attr-ilbc - 16.3.0-7 - iLBC format attribute module.
asterisk16-res-format-attr-opus - 16.3.0-7 - Opus format attribute module.
asterisk16-res-format-attr-silk - 16.3.0-7 - SILK format attribute module.
asterisk16-res-format-attr-siren14 - 16.3.0-7 - Siren14 format attribute module.
asterisk16-res-format-attr-siren7 - 16.3.0-7 - Siren7 format attribute module.
asterisk16-res-format-attr-vp8 - 16.3.0-7 - VP8 format attribute module.
asterisk16-res-hep - 16.3.0-7 - HEPv3 API.
asterisk16-res-hep-pjsip - 16.3.0-7 - PJSIP HEPv3 logger.
asterisk16-res-hep-rtcp - 16.3.0-7 - RTCP HEPv3 logger.
asterisk16-res-http-media-cache - 16.3.0-7 - HTTP media cache backend.
asterisk16-res-http-websocket - 16.3.0-7 - HTTP WebSocket support.
asterisk16-res-limit - 16.3.0-7 - Resource limits.
asterisk16-res-manager-devicestate - 16.3.0-7 - Manager device state topic forwarder.
asterisk16-res-manager-presencestate - 16.3.0-7 - Manager presence state topic forwarder.
asterisk16-res-monitor - 16.3.0-7 - Call monitoring resource.
asterisk16-res-musiconhold - 16.3.0-7 - Music On Hold resource.
asterisk16-res-mutestream - 16.3.0-7 - Mute audio stream resources.
asterisk16-res-mwi-devstate - 16.3.0-7 - This module allows presence subscriptions to voicemail boxes. This allows common BLF keys to act as voicemail waiting indicators.
asterisk16-res-mwi-external - 16.3.0-7 - Core external MWI resource.
asterisk16-res-mwi-external-ami - 16.3.0-7 - AMI support for external MWI.
asterisk16-res-parking - 16.3.0-7 - Call parking resource.
asterisk16-res-phoneprov - 16.3.0-7 - HTTP phone provisioning.
asterisk16-res-pjproject - 16.3.0-7 - PJProject log and utility support.
asterisk16-res-pjsip-phoneprov - 16.3.0-7 - PJSIP phone provisioning.
asterisk16-res-pktccops - 16.3.0-7 - PktcCOPS manager for MGCP.
asterisk16-res-realtime - 16.3.0-7 - Realtime data lookup/rewrite.
asterisk16-res-remb-modifier - 16.3.0-7 - REMB modifier module.
asterisk16-res-resolver-unbound - 16.3.0-7 - Unbound DNS resolver support.
asterisk16-res-rtp-asterisk - 16.3.0-7 - Asterisk RTP stack.
asterisk16-res-rtp-multicast - 16.3.0-7 - Multicast RTP engine.
asterisk16-res-security-log - 16.3.0-7 - Security event logging.
asterisk16-res-smdi - 16.3.0-7 - Simplified Message Desk Interface resource.
asterisk16-res-snmp - 16.3.0-7 - SNMP agent for Asterisk.
asterisk16-res-sorcery - 16.3.0-7 - Sorcery backend modules for data access intended for using realtime as backend.
asterisk16-res-sorcery-memory-cache - 16.3.0-7 - Sorcery memory cache object wizard.
asterisk16-res-speech - 16.3.0-7 - Generic speech recognition API.
asterisk16-res-srtp - 16.3.0-7 - Secure RTP.
asterisk16-res-stasis - 16.3.0-7 - Stasis application support.
asterisk16-res-stasis-answer - 16.3.0-7 - Stasis application answer support.
asterisk16-res-stasis-device-state - 16.3.0-7 - Stasis application device state support.
asterisk16-res-stasis-mailbox - 16.3.0-7 - Stasis application mailbox support.
asterisk16-res-stasis-playback - 16.3.0-7 - Stasis application playback support.
asterisk16-res-stasis-recording - 16.3.0-7 - Stasis application recording support.
asterisk16-res-stasis-snoop - 16.3.0-7 - Stasis application snoop support.
asterisk16-res-statsd - 16.3.0-7 - Statsd client support.
asterisk16-res-stun-monitor - 16.3.0-7 - STUN network monitor.
asterisk16-res-timing-dahdi - 16.3.0-7 - DAHDI timing interface.
asterisk16-res-timing-pthread - 16.3.0-7 - pthread timing interface.
asterisk16-res-timing-timerfd - 16.3.0-7 - Timerfd timing interface.
asterisk16-res-xmpp - 16.3.0-7 - Asterisk XMPP interface.
asterisk16-sounds - 16.3.0-7 - This package provides the sound-files for Asterisk 16.
asterisk16-util-aelparse - 16.3.0-7 - Check extensions.ael file.
asterisk16-util-astcanary - 16.3.0-7 - Assures Asterisk no threads have gone missing.
asterisk16-util-astdb2bdb - 16.3.0-7 - Convert astdb back to Berkeley DB 1.86.
asterisk16-util-astdb2sqlite3 - 16.3.0-7 - Convert astdb to SQLite 3.
asterisk16-util-check-expr - 16.3.0-7 - Expression checker [older version].
asterisk16-util-check-expr2 - 16.3.0-7 - Expression checker [newer version].
asterisk16-util-conf2ael - 16.3.0-7 - Convert .conf to .ael.
asterisk16-util-muted - 16.3.0-7 - Listens for AMI events. Mutes soundcard during call.
asterisk16-util-smsq - 16.3.0-7 - Send messages from command line.
asterisk16-util-stereorize - 16.3.0-7 - Merge two mono WAV-files to one stereo WAV-file.
asterisk16-util-streamplayer - 16.3.0-7 - A utility for reading from a raw TCP stream [MOH source].
asterisk16-voicemail - 16.3.0-7 - Voicemail modules.
