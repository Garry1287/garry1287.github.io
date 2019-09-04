---
layout: post
title:  "Поиск ошибки в parse.py"
date:   2019-08-30 11:33:15 +0300
categories: python posts
---

# Поиск ошибки #
Ошибка была такая
```
  File "parse.py", line 201, in <module>
    domain = node.getElementsByTagName('domain')[0].childNodes[0].nodeValue.encode('idna').decode('ascii')
IndexError: list index out of range

```



Вот нашел место ошибки средством ipython
```
nalove.ru
www.kalyanspb.ru
pontorez.com
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-44-6bd6874af2d6> in <module>()
      1 for node in content:
      2     if not node.getAttribute('blockType'):
----> 3         domain = node.getElementsByTagName('domain')[0].childNodes[0].nodeValue
      4         print(domain)
      5 

IndexError: list index out of range

```



## Нашёл index элемента где была ошибка так ##


```
In [47]: for index,node in enumerate(content):
    ...:     if not node.getAttribute('blockType'):
    ...:         domain = node.getElementsByTagName('domain')[0].childNodes[0].nodeValue
    ...:         if domain == 'pontorez.com':
    ...:             print(index)
    ...:             
    ...:             
    ...:         
    ...:       
    ...:     
5942
12574
23144
23398
24869
29097
53680
61970
110300
111384
119772
119773
131223
141449
141524
142287
142288
142306
145061
146440
147378
148218
148435
148436
148617
149812
150381
150496
150731
152074
152094
152913
154174
154190
154629
155005
155118
```


[https://docs.python.org/3.7/library/xml.dom.html](https://docs.python.org/3.7/library/xml.dom.html)

Запись 155119 приводит к ошибке.

```
In [97]: content[155120].childNodes[0].toxml()
Out[97]: '<decision date="2019-06-25" number="2а-4235/2019" org="суд"/>'

In [98]: content[155120].childNodes[1].toxml()
Out[98]: '<url><![CDATA[https://standaards.com/]]></url>'

In [99]: content[155120].childNodes[2].toxml()
Out[99]: '<domain><![CDATA[standaards.com]]></domain>'

In [100]: content[155120].childNodes[3].toxml()
Out[100]: '<ip>104.18.53.33</ip>'

In [101]: content[155120].childNodes[4].toxml()
Out[101]: '<ip>104.18.52.33</ip>'

In [102]: content[155120].childNodes[5].toxml()
Out[102]: '<ipv6>2606:4700:0030:0000:0000:0000:6812:3521</ipv6>'

In [103]: content[155120].childNodes[6].toxml()
Out[103]: '<ipv6>2606:4700:0030:0000:0000:0000:6812:3421</ipv6>'

In [104]: content[155120].childNodes[7].toxml()
```

Так можно искать нужные данные

```
In [105]: content[155119].childNodes[0].toxml()
Out[105]: '<decision date="2018-12-12" number="2а-11653/2018" org="суд"/>'

In [106]: content[155119].childNodes[1].toxml()
Out[106]: '<url ts="2019-08-28T13:07:00+03:00"><![CDATA[http:/premium-diploms.com/куплю-диплом-о-высшем-образовании]]></url>'

In [107]: content[155119].childNodes[2].toxml()
Out[107]: '<ip ts="2019-08-28T13:07:00+03:00">137.74.215.56</ip>'


In [111]: content[155118].toxml()
Out[111]: '<content entryType="1" hash="113A1170FC64AFC2ED2EFE917D41D5FE" id="1676118" includeTime="2019-08-09T12:16:44"><decision date="2019-07-18" number="2а-4045/2019" org="суд"/><url><![CDATA[http://pontorez.com/node/901]]></url><domain><![CDATA[pontorez.com]]></domain><ip>198.27.106.192</ip><ipv6>2607:5300:0060:3ab7:ffff:ffff:0000:0056</ipv6></content>'


In [109]: content[155119].toxml()
Out[109]: '<content entryType="1" hash="21A22D9E1C5C85D9E9EF65403536C722" id="1676122" includeTime="2019-08-28T12:17:24" ts="2019-08-28T13:07:00+03:00"><decision date="2018-12-12" number="2а-11653/2018" org="суд"/><url ts="2019-08-28T13:07:00+03:00"><![CDATA[http:/premium-diploms.com/куплю-диплом-о-высшем-образовании]]></url><ip ts="2019-08-28T13:07:00+03:00">137.74.215.56</ip></content>'



In [110]: content[155120].toxml()
Out[110]: '<content entryType="1" hash="B56B59549751BBDAB7CB9EE026E21EE9" id="1676124" includeTime="2019-08-09T12:16:45"><decision date="2019-06-25" number="2а-4235/2019" org="суд"/><url><![CDATA[https://standaards.com/]]></url><domain><![CDATA[standaards.com]]></domain><ip>104.18.53.33</ip><ip>104.18.52.33</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:3521</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:3421</ipv6></content>'
```


# Запись без домена #

Вот запись без domain, из-за который произошла ошибка
```
<content entryType="1" hash="21A22D9E1C5C85D9E9EF65403536C722" id="1676122" includeTime="2019-08-28T12:17:24" ts="2019-08-28T13:07:00+03:00"><decision date="2018-12-12" number="2а-11653/2018" org="суд"/><url ts="2019-08-28T13:07:00+03:00"><![CDATA[http:/premium-diploms.com/куплю-диплом-о-высшем-образовании]]></url><ip ts="2019-08-28T13:07:00+03:00">137.74.215.56</ip></content>
```

Проверка на существование домена
```
In [119]: if content[155119].getElementsByTagName('domain'):
     ...:     print('yes')
     ...:     

In [120]: if not content[155119].getElementsByTagName('domain'):
     ...:     print('yes')
```

Так как доменов тоже может быть несколько, используем для доменов туже функцию, как и для ip, но проверяем на существование


```
def GetfromRKN(node, tag, file2write):
    listdata = []
#    newlistdata = []
    MyNodeList = node.getElementsByTagName(tag)    # Получаем все NodeList c ip адресами которые надо заблокировать, как domain брать нельзя, т.к ip может быть несколько
    for i in range(MyNodeList.length): #MyNodeList содержит ip адреса, которые необходимо заблокировать
        MyIPorSubnet = (MyNodeList.item(i).childNodes[0].nodeValue) #в цикле получаем каждый элемент - ip, который надо заблокироват
        listdata.append(str(MyIPorSubnet))
#    if tag == 'ip':
#        newlistdata = [ i+'/32' for i in listdata]
#    elif tag == 'ipv6':
#        newlistdata = [ i+'/128' for i in listdata]
#    else: newlistdata = listdata
#    for item in newlistdata:
    for item in listdata:
        file2write.write("{}\n".format(item))
```

Конечное исправление
```
    elif node.getAttribute('blockType') == 'domain' or node.getAttribute('blockType') == 'default' or not node.getAttribute('blockType'):
        if node.getElementsByTagName('domain'):
            GetfromRKN(node, 'domain', filedomain)
```

Надо ещё сделать с domain-mask



## Поиск записей ##
Например надо узнать есть ли запись про домен skoty.info. IP думаю также можно примерно найти

```
In [132]: for node in content:
     ...:     if node.getElementsByTagName('domain'):
     ...:         if node.getElementsByTagName('domain')[0].childNodes[0].nodeValue == "skoty.info":
     ...:             print (node.toxml())
     ...:             
     ...:         
<content entryType="1" hash="8C561541A97B1AFB60AC6C66B4D549C5" id="1265027" includeTime="2019-01-29T13:02:45"><decision date="2018-12-11" number="б/н" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/41455-svod-nal-beznal-vedet-k-fns-rzhd-i-rostekhnadzoru]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="C0DE85CFFF37893BE3E687944C9B9F6C" id="1279245" includeTime="2018-12-30T18:38:06"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/37238-ravdu-o-pohozhdeniyah-glavy-vtb-andreya-kostina-sud-zapretil-publikovat]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="7E16252D68988E3FBB6678CD07C41098" id="1279246" includeTime="2018-12-30T18:38:06"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/81609-gruppa-vtb-lichnaya-svinya-kopilka-andreya-kostina-chast-3-nailya-asker-zade]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="D65DA1C3335C020D9202CDF6FE1F2B4C" id="1283678" includeTime="2018-12-31T18:14:14"><decision date="2018-09-11" number="А56-81482" org="суд"/><url><![CDATA[http://skoty.info/zhurnalisty/item/79723-mnogozhentsy-putina-andrej-kostin-i-nailya-asker-zade]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="768ABDE65CFAD4FFD3F1D32DB04A5238" id="1316933" includeTime="2019-01-25T19:38:53"><decision date="2018-12-18" number="б/н" org="суд"/><url><![CDATA[http://skoty.info/deputaty/item/77317-tatarskaya-orda-magdeevykh-okkupiruet-shvejtsariyu]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="63504137EB2056AB33E4651EDFFD894B" id="1317476" includeTime="2019-01-25T12:21:43"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/11389-raschistka-pod-shuvalova-v-chih-interesah-gotovitsya-pozornaya-otstavka-andreya-kostina]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="528D846A314AA33509D2444CC08761F1" id="1317477" includeTime="2019-01-25T12:21:43"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/42677-andrej-kostin-sdelal-nailyu-asker-zade-zhenshchinoj-milliarderom]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="2BAAA30DBCEA0F6EF2AD1BFED610BB62" id="1317478" includeTime="2019-01-25T12:21:43"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/48847-lyubovnica-andreya-kostina-rodivshaya-prezidentu-banka]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="77699ED5FBC643CD7867764FA0A42D8A" id="1317479" includeTime="2019-01-25T12:21:43"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49050-nailya-asker-zade-chem-otlichaetsya-chlen-pravitelstva-ot-chlena-pravleniya-banka]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="F04826B2BA479C043572745C234C7665" id="1317480" includeTime="2019-01-25T12:21:44"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49418-v-bankrotstvo-andrej-kostin-zakhodil-nailyu-grustno-provodil]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="D3ADE9958D71339516488D9D047E8CE3" id="1317481" includeTime="2019-01-25T12:21:44"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49419-v-bankrotstvo-andrej-kostin-zakhodil-nailyu-grustno-provodil]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="FD054EE040B55BBC57137173237A14AF" id="1317482" includeTime="2019-01-25T12:21:44"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/rossiya/item/705-gruppa-vtb-rabotaet-na-mnogozhontsa-andreya-kostina]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="3F6920225F03F6E04FA255B0DAF6EE8A" id="1317483" includeTime="2019-01-25T12:21:44"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/78451-lyubovnica-andreya-kostina-rodivshaya-prezidentu-banka]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="887E42F8419199BFE6241E287A34197C" id="1317484" includeTime="2019-01-25T12:21:44"><decision date="2018-11-16" number="А56-121229/2018" org="суд"/><url><![CDATA[http://skoty.info/sudi/item/690-gruppa-vtb-lichnaya-svinya-kopilka-andreya-kostina]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="303E2A40CF82FE54A565D0B473571E70" id="1399876" includeTime="2019-03-07T11:18:01"><decision date="2017-10-04" number="2-2889/17" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/72272-supruga-skandalnogo-glavy-fonda-inventure-partners-azatyana-razoryaet-podrug-brilliantovymi-fenechkami]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="125F22E926AE04BFB1815A9D583B0B44" id="1532605" includeTime="2019-06-10T20:04:47"><decision date="2019-02-25" number="2-2394/2019" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/44305-svod-nal-beznal-vedet-k-fns-rzhd-i-rostehnadzoru]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="226ECDF076ABA16F9B54D3C33768A331" id="1553206" includeTime="2019-06-06T18:45:37"><decision date="2019-02-25" number="2-2394/2019" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49804-rosotkatnadzor-svetlany-radionovoj-zvezda-sechina-i-kobylkina-navela-fsb-na-mishustina-i-belozjorova]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="786290A78165E89FD2593B772CCB7415" id="1558636" includeTime="2019-06-10T20:04:47"><decision date="2019-02-25" number="2-2394/2019" org="суд"/><url><![CDATA[http://skoty.info/prokurory/item/25300-rustem-magdeev-opg-i-butik-graff]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.49.122</ip><ip>104.18.48.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="ADBA1EE18463E53D47FB2DD947303D70" id="1667766" includeTime="2019-08-06T10:36:34"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49806-vladimir-tokarev-i-ego-dela-minregion-pao-rusgidro-ooo-sts-i-drugie]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="8C6B9DB2CA1F4DABF0E0836581B84917" id="1667782" includeTime="2019-08-06T10:36:35"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49829-kak-tokarev-kapital-v-slepoy-trast-otpravlyal]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6></content>
<content entryType="1" hash="B19B8B64D2A52F390F2B693265384570" id="1667806" includeTime="2019-08-06T10:36:35"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49822-vladimir-tokarev-kompromat-na-moshennika-i-kaznokrada]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="454AC6DEBEB686482A4F72F0405D4900" id="1667845" includeTime="2019-08-06T10:36:35"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49815-vladimir-tokarev-i-ego-ugo-hugo-boss-yuriy-reylyan-kak-vorovat-dlya-deripaski-i-ne-sidet]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="559400143B7FD68A98A64F42F9FDA33E" id="1667898" includeTime="2019-08-06T10:36:36"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49800-rossiyan-obvorovali-na-milliardy-gigantskie-summy-hischeniy-chinovnika-vladimira-tokareva]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
<content entryType="1" hash="1500D61A1760028868D04CEB3D4A1AA9" id="1667906" includeTime="2019-08-06T10:36:35"><decision date="2019-05-20" number="2-3232/19" org="суд"/><url><![CDATA[http://skoty.info/novosti/item/49830-tokarev-vladimir-aleksandrovich-gotovitsya-sest-po-zhadnosti-ili-povysitsya-po-sluzhbe]]></url><domain><![CDATA[skoty.info]]></domain><ip>104.18.48.122</ip><ip>104.18.49.122</ip><ipv6>2606:4700:0030:0000:0000:0000:6812:307a</ipv6><ipv6>2606:4700:0030:0000:0000:0000:6812:317a</ipv6></content>
```
