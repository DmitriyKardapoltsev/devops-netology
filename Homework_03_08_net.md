# Домашнее задание к занятию «Компьютерные сети. Лекция 3»

## Задание

1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP.

 ```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```

***Ответ:***

```
     dkard@DKard:~$ telnet route-views.routeviews.org
          Trying 128.223.51.103...
          Connected to route-views.routeviews.org.
          Escape character is '^]'.
          C
          **********************************************************************

                              RouteViews BGP Route Viewer
                              route-views.routeviews.org

           route views data is archived on http://archive.routeviews.org

           This hardware is part of a grant by the NSF.
           Please contact help@routeviews.org if you have questions, or
           if you wish to contribute your view.

           This router has views of full routing tables from several ASes.
           The list of peers is located at http://www.routeviews.org/peers
           in route-views.oregon-ix.net.txt

           NOTE: The hardware was upgraded in August 2014.  If you are seeing
           the error message, "no default Kerberos realm", you may want to
           in Mac OS X add "default unset autologin" to your ~/.telnetrc

           To login, use the username "rviews".

           **********************************************************************

           User Access Verification

     Username: rviews
     route-views>show ip route 88.80.63.161
           Routing entry for 88.80.32.0/19
            Known via "bgp 6447", distance 20, metric 0
            Tag 3303, type external
            Last update from 217.192.89.50 7w0d ago
            Routing Descriptor Blocks:
            * 217.192.89.50, from 217.192.89.50, 7w0d ago
                Route metric is 0, traffic share count is 1
                AS Hops 3
                Route tag 3303
                MPLS label: none  
     
     route-views>show bgp 88.80.63.161
          BGP routing table entry for 88.80.32.0/19, version 2653823118
          Paths: (20 available, best #20, table default)
            Not advertised to any peer
            Refresh Epoch 1
            3333 8359 39001
              193.0.0.56 from 193.0.0.56 (193.0.0.56)
                Origin IGP, localpref 100, valid, external
                Community: 8359:5500 8359:55418
                path 7FE0AD7B3FC0 RPKI State not found
                rx pathid: 0, tx pathid: 0
            Refresh Epoch 1
            57866 1299 8359 39001
              37.139.139.17 from 37.139.139.17 (37.139.139.17)
                Origin IGP, metric 0, localpref 100, valid, external
                Community: 1299:20000 57866:100 65100:1299 65103:3 65104:31
                unknown transitive attribute: flag 0xE0 type 0x20 length 0x30
                  value 0000 E20A 0000 0064 0000 0513 0000 E20A
                        0000 0065 0000 0064 0000 E20A 0000 0067
                        0000 0003 0000 E20A 0000 0068 0000 001F

                path 7FE03FE3E998 RPKI State not found
                rx pathid: 0, tx pathid: 0
            Refresh Epoch 1
            3267 1299 8359 39001
              194.85.40.15 from 194.85.40.15 (185.141.126.1)
                Origin IGP, metric 0, localpref 100, valid, external
                path 7FE0B6AF88B0 RPKI State not found
                rx pathid: 0, tx pathid: 0
            Refresh Epoch 1
            8283 8359 39001
              94.142.247.3 from 94.142.247.3 (94.142.247.3)
                Origin IGP, metric 0, localpref 100, valid, external
                Community: 8283:1 8283:101 8359:5500 8359:55418
                unknown transitive attribute: flag 0xE0 type 0x20 length 0x24
                  value 0000 205B 0000 0000 0000 0001 0000 205B
                        0000 0005 0000 0001 0000 205B 0000 0008
                        0000 001A
                path 7FE18A48B248 RPKI State not found
                rx pathid: 0, tx pathid: 0
            Refresh Epoch 1
            7018 3356 8359 39001
              12.0.1.63 from 12.0.1.63 (12.0.1.63)
                Origin IGP, localpref 100, valid, external
                Community: 7018:5000 7018:37232
                path 7FE12BAA1898 RPKI State not found
                rx pathid: 0, tx pathid: 0
```

2. Создайте dummy-интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

3. Проверьте открытые TCP-порты в Ubuntu. Какие протоколы и приложения используют эти порты? Приведите несколько примеров.

4. Проверьте используемые UDP-сокеты в Ubuntu. Какие протоколы и приложения используют эти порты?

5. Используя diagrams.net, создайте L3-диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 

*В качестве решения пришлите ответы на вопросы, опишите, как они были получены, и приложите скриншоты при необходимости.*

 ---
 
## Задание со звёздочкой* 

Это самостоятельное задание, его выполнение необязательно.

6. Установите Nginx, настройте в режиме балансировщика TCP или UDP.

7. Установите bird2, настройте динамический протокол маршрутизации RIP.

8. Установите Netbox, создайте несколько IP-префиксов, и, используя curl, проверьте работу API.

----

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.

-----

### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.  
 
Обязательными являются задачи без звёздочки. Их выполнение необходимо для получения зачёта и диплома о профессиональной переподготовке.

Задачи со звёздочкой (*) являются дополнительными или задачами повышенной сложности. Они необязательные, но их выполнение поможет лучше разобраться в теме.
