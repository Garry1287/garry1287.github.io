---
layout: post
title:  "cacti-poller"
date:   2015-12-06 21:31:30 +0300
categories: cacti-poller
tags: cacti
---

# cacti-poller
Poller раз в минуту

[http://www.tolaris.com/2013/07/09/cacti-and-1-minute-polling/](http://www.tolaris.com/2013/07/09/cacti-and-1-minute-polling/)
[http://dikehtonon.blogspot.co.uk/2011/11/cacti-1-minute-polling-using-spine.html](http://dikehtonon.blogspot.co.uk/2011/11/cacti-1-minute-polling-using-spine.html)
[http://blog.unixstyle.ru/92/cacti-and-1-each-minute-polling/](http://blog.unixstyle.ru/92/cacti-and-1-each-minute-polling/)

The cron interval is how often crontab calls the poll script.  The minimum for this is 1 minute, as that's the
maximum frequency of a cron.  However, Poll interval is how often the script polls a host.  You can have your
cron at 1 minute, and your interval at 30 seconds, which basically means for each run of the poller script,
it will actually hit all your hosts twice.

As for the graphing issues.  There is at least one more place you may need to change things.

Under Data Templates, Step should match your polling interval.  By default it is 5 minutes.  This means that
graphs that are created with this template will only have one data point for every 5 minutes, even if you are
writing to them every 30 seconds.  Note, that changing this will not change existing graphs.  You'd have to
use rrdtool to modify the graph files themselves or recreate them.



acti and 1 (each) minute polling

    С появлением версии 0.8.7 в cacti реализована возможность настройки интервала опроса сенсоров. Утверждается, что она находится в зачаточном состоянии и полноценную реализацию ожидать имеет смысл не ранее версии 0.9. Однако текущей реализации воплне достаточно для того, чтобы воплотить в жизнь опрос оборудования с периодичностью раз в минуту.

    Отправной точкой является установка или обновление cacti версии не ниже 0.8.7. Для более ранней версии имеется реализация в виде набора заплаток от одного из разработчиков (нами не тестировалась).

    Изменяем интенсивность опроса через «Settings -> Poller». Устанавливаем значение «Poller Interval» в значение «Every minute». При этом значение «Cron Interval» остается прежним «Every 5 Minutes». Трогать запись в crontab не следует. Скрипт должен запускаться из cron раз в 5 минут. Логика опроса в зависимости от параметра «Poller Interval» реализована в самом скрипте poller.php. Для наглядности правильные настройки приведены на снимке экрана.

    Следующий этап подготовка соответствующего «Data Source». Рассмотрим на примере графика «Load Average» из стандартной поставки. Если сомневаетесь в своих возможностях перед изменением настроек стандартных «Data Sources» создайте их дубликаты (резервные копии). График «Load Average» использует 3-и «Data Source: «ucd/net — Load Average — 1 Minute», «ucd/net — Load Average — 5 Minute», «ucd/net — Load Average — 15 Minute». Изменим шаблон «ucd/net — Load Average — 1 Minute» следующим образом.

    В дополнение к ранее активным добавим в поле «Associated RRA’s» значение «Hourly (1 Minute Average)»;
    Поле «Step» устанавливаем в значение 60;
    Поле «Heartbeat» устанавливаем в значение 120.

    Измененные значения приведены на снимке экрана. Аналогичные изменения необходимо произвести для шаблонов «ucd/net — Load Average — 5 Minute» и «ucd/net — Load Average — 15 Minute».

    Мы приблизились к финишной прямой. Текущие изменения вступают в силу для вновь создаваемых графиков из шаблона «Load Average». Существующие придется удалить и создать снова или попытаться воспользоваться советами из сообщения разработчика. Полученный результат на снимке экрана (нами используется модифицированный шаблон «Load Average»).
    
    
    
Установка нового spine    
    [https://www.ibm.com/support/knowledgecenter/en/SSVMSD_9.1.4/RTM_faq/rtm_installing_spine_poller.html](https://www.ibm.com/support/knowledgecenter/en/SSVMSD_9.1.4/RTM_faq/rtm_installing_spine_poller.html)
    
    ./bootstrap
  ./configure
  make
  make install
  chown root:root /usr/local/spine/bin/spine
  chmod +s /usr/local/spine/bin/spine

