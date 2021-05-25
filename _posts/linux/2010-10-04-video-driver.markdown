---
layout: post
title:  "video-driver"
date:   2010-10-04 01:24:58 +0400
categories: linux
tags: linux
---

# video-driver
Для запуска операционной среды linux в текстовом режиме (режим командной строки) дополнительных действий не требуется.

  Внимание!
  В ряде случаев - например после некорректной установки драйверов ati с поддержкой 3D (fglrx) -
  возможен старт с "чёрным экраном".
  Для устранения данной проблемы осуществляем вход с удаленной машины по ssh и выполняем команду
     # aticonfig -inital


Драйвер vesa может быть использован, если видеокарта поддерживает стандарт VESA. (На текущий момент) 
Нам неизвестны видеокарты не поддерживающие данный стандарт. Последние версии драйвера vesa (например в debian squeeze с xorg версии 7.5) обеспечивают поддержку и 2D/3D ускорения.

Для подключения драйвера

    устанавливаем пакет xserver-xorg-video-vesa содержащий драйвер xorg-vesa 

  # apt-get install xserver-xorg-video-vesa

    добавляем в файл конфигурации X-сервера /etc/X11/xorg.conf секцию 

  Section "Device"
          Driver      "vesa"
  EndSection

    перезапускаем X-сервер / менеджер дисплея 

  Внимание!
  В некоторых случаях - например при использовании видеокарт intel и при включ


Узнать тип видеокарты
lspci | grep VGA



Система какраз таки загружается. Не работает X сервер. Комбинация клавишь Ctrl+Alt+Backspace завершит работу X сервера.
 Далее в любом текстовом редакторе (консольном конечно) открыть конфиг.
Самый простой это nano
от root:
# nano /etc/X11/xorg.conf
(или можно в mc клавишей F4)
далее правим строчку в секции 'Section "Device"':
Driver "vesa"
vesa - это общий видеодрайвер независимый от железа.
сохраняем конфиг и запускаем X сервер командой:
$ startx
только запускать от пользователя а не от рута.
Это не решит проблему с 3D просто поможет загрузиться в графический режим и продолжить поиск решения проблемы.




не может оно к перезагрузке привести. Просто возможно X сервер перезапускается. Обычно после нескольких раз он падает.
вот ещё вариант переключись в виртуальную консоль
ctrl+alt+F2 (или практически любой F кроме 7 на ней X сервер)
появиться приглашение логинься под рутом, правь конфиг, выходи (ctrl+D) переходи в консоль 
где X сервер висит (ctrl+alt+F7) и перезапускай его (ctrl+alt+backspace)



Цитата:
    далее правим строчку в секции 'Section "Device"': Driver "vesa"

и ещё, желательно Цитата:
    # sax2 -r 
это пересоберёт xorg.conf на драйвер по умолчанию.














Только сначала, в дополнение сказанному Maestro
Цитата:

    # sax2 -r


что пересоберёт xorg.conf
а потом
Цитата:

    # rpm -e $(rpm -qa | grep fglrx)


что удалит ранее установленный драйвер
















nomodeset попробовать при загрузке






000:007:00.0 Display controller: Matrox Graphics, Inc. MGA G200e [Pilot] ServerEngines (SEP1) 


05:00.0 VGA compatible controller: Matrox Electronics Systems Ltd. MGA G200e [Pilot] ServerEngines (SEP1) (rev 04)










[https://www.suse.com/releasenotes/i386/openSUSE/12.3/RELEASE-NOTES.ru.html](https://www.suse.com/releasenotes/i386/openSUSE/12.3/RELEASE-NOTES.ru.html)


В openSUSE 11.3 мы перешли на KMS (Kernel Mode Setting) для видеокарт Intel, ATI и NVIDIA, теперь это поведение по умолчанию. 
Если у вас при этом возникают проблемы с поддержкой KMS драйвером (intel, radeon, nouveau), 
отключите KMS, добавив nomodeset в строку загрузки ядра. Для постоянного применения в Grub 2, 
загрузчике по умолчанию, добавьте это в строку параметров загрузки ядра по 
умолчанию GRUB_CMDLINE_LINUX_DEFAULT в файле /etc/default/grub от имени root и запустите команду терминала

sudo /usr/sbin/grub2-mkconfig --output=/boot/grub2/grub.cfg





ну как вариант еще отключить kms в initrd
yast2 sysconfig set NO_KMS_IN_INITRD=«yes»
но устоновщик ати должен это сделать сам













[http://www.linux.org.ru/forum/desktop/6036976](http://www.linux.org.ru/forum/desktop/6036976)
[http://ru.opensuse.org/%D0%94%D1%80%D0%B0%D0%B9%D0%B2%D0%B5%D1%80%D1%8B_NVIDIA](http://ru.opensuse.org/%D0%94%D1%80%D0%B0%D0%B9%D0%B2%D0%B5%D1%80%D1%8B_NVIDIA)
[http://help.ubuntu.ru/wiki/ubuntu_12.04_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B_%D1%82%D0%B2%D0%B8%D0%BA%D0%B8](http://help.ubuntu.ru/wiki/ubuntu_12.04_%D0%BF%D1%80%D0%BE%D0%B1%D0%BB%D0%B5%D0%BC%D1%8B_%D1%82%D0%B2%D0%B8%D0%BA%D0%B8)
[http://ru.opensuse.org/SDB:%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA_%D1%81_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82%D0%B0%D0%BC%D0%B8_NVIDIA](http://ru.opensuse.org/SDB:%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA_%D1%81_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82%D0%B0%D0%BC%D0%B8_NVIDIA)
[http://ru.opensuse.org/SDB:NVIDIA_-_%D1%81%D0%BB%D0%BE%D0%B6%D0%BD%D1%8B%D0%B9_%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1](http://ru.opensuse.org/SDB:NVIDIA_-_%D1%81%D0%BB%D0%BE%D0%B6%D0%BD%D1%8B%D0%B9_%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1)
[http://ru.opensuse.org/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA_%D1%81_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82%D0%B0%D0%BC%D0%B8_NVIDIA](http://ru.opensuse.org/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA_%D1%81_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82%D0%B0%D0%BC%D0%B8_NVIDIA)

[http://tdkare.ru/sysadmin/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82_%D0%B2_linux](http://tdkare.ru/sysadmin/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82_%D0%B2_linux)



[http://tdkare.ru/sysadmin/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82_%D0%B2_linux](http://tdkare.ru/sysadmin/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B2%D0%B8%D0%B4%D0%B5%D0%BE%D0%BA%D0%B0%D1%80%D1%82_%D0%B2_linux)








[http://ru.opensuse.org/SDB:%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85_%D0%BA%D0%B0%D1%80%D1%82](http://ru.opensuse.org/SDB:%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D1%85_%D0%BA%D0%B0%D1%80%D1%82)
[http://open-suse.ru/content/seryy-ekran-posle-perezagruzki-linux-suse-122](http://open-suse.ru/content/seryy-ekran-posle-perezagruzki-linux-suse-122)
[http://forums.opensuse.org/english/get-technical-help-here/how-faq-forums/advanced-how-faq-read-only/438705-opensuse-graphic-card-practical-theory-guide-users.html](http://forums.opensuse.org/english/get-technical-help-here/how-faq-forums/advanced-how-faq-read-only/438705-opensuse-graphic-card-practical-theory-guide-users.html)
[https://forums.opensuse.org/blogs/jdmcdaniel3/how-start-opensuse-12-2-grub-2-into-run-level-3-112/](https://forums.opensuse.org/blogs/jdmcdaniel3/how-start-opensuse-12-2-grub-2-into-run-level-3-112/)
[https://www.suse.com/releasenotes/x86_64/openSUSE/12.3/#sec.114.kms](https://www.suse.com/releasenotes/x86_64/openSUSE/12.3/#sec.114.kms)