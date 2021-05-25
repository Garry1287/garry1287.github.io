---
layout: post
title:  "ksmserver"
date:   2011-05-11 01:31:50 +0400
categories: linux
tags: linux
---

# ksmserver
Господин Epoxyde на ваш вопрос ответил на форуме kde.org в теме "Could not start ksmserver".
Недавно я производил на своем нетбуке обновление с openSUSE 11.4 на openSUSE 12.1 и получил такое же сообщение.
Совет господина Epoxyde реально помог, за что премного ему благодарен.
Возможно, пригодится кому-нибудь еще, поэтому решил опубликовать ссылку на этот совет на российском форуме по KDE.
Надеюсь, господин Epoxyde не будет против. Дополнительно (на всякий случай ;)) приведу цитату без купюр:
Цитировать

    in runlevel 3 (init 3) or IceWN (I had IceWN working only):

    # zypper up
    # zypper dup

    then REBOOT and go to runlevel 3:

    # zypper lu
    # zypper ve
    # zypper inr
    # zypper pchk
    # zypper dup

    then (if you want, you may reboot, but may do it without reboot)

    # startx

    and the Force will be with you!