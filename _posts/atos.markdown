Договор №MS 03 2014-04 от 17.03.2014 между ООО "Атос АйТи Солюшенс энд Сервисез" и ООО "Промсвязь-Инвест".
Контакты Сервис-Деска АТОС (в Воронеже, по идее, мультиязычный):

Email - it-support@atos.net
Phone - +7 495 737 2505.





Доступ к firewall - по ssh
Логин nlmk, дальше все стандартно для впн, как было раньше.
ip 10.170.253.1
Есть доступ к девайсам через консоль от Atos
по https
193.80.22.64 tcp/4431
193.80.22.64 tcp/4432 


193.80.22.64 on port tcp/3333
193.80.22.64 on port tcp/3334

Вся информация тут в письме, которая у нас есть.

I would like to inform you I’ve installed the console servers. The procedure to reach the devices via the console server is the following:

1.      Make an ssh connection to devices in the DC38 (firewall0, balancer0, switch0, CE0) using the IP address of 193.80.22.64 on port tcp/3333 

a.       to devices in the DC38 (firewall0, balancer0, switch0, CE0) using the IP address of 193.80.22.64 on port tcp/3333 

b.      to devices in the DC39 (firewall1, balancer1, switch1, CE1) using the IP address of 193.80.22.64 on port tcp/3334

2.      when they get a prompt use the username followed by the “:”

c.       username: NLMK_admin

d.      password: what we created for the devices itself

3.      there will be the manageable devices in the list on the screen, they have to enter what they wish to manage