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

***Ответ:***

```
    vagrant@vagrant:~$ sudo modprobe -v dummy
         insmod /lib/modules/5.4.0-135-generic/kernel/drivers/net/dummy.ko numdummies=0
    vagrant@vagrant:~$ lsmod | grep dummy
         dummy                  16384  0
    vagrant@vagrant:~$ ifconfig -a | grep dummy
    vagrant@vagrant:~$ sudo ip link add dummy2 type dummy
    vagrant@vagrant:~$ sudo ip addr add 192.168.10.100/24 dev dummy2
    vagrant@vagrant:~$ sudo ip link set dummy2 up
    vagrant@vagrant:~$ ip route
         default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
         10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15
         10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100
         192.168.10.0/24 dev dummy2 proto kernel scope link src 192.168.10.100
         192.168.33.0/24 dev eth1 proto kernel scope link src 192.168.33.10
    vagrant@vagrant:~$ sudo ip addr add 10.0.0.100/24 dev dummy2
    vagrant@vagrant:~$ sudo ip link set dummy2 up
    vagrant@vagrant:~$ sudo ip route add to 10.10.0.0/16 via 10.0.0.100
    vagrant@vagrant:~$ sudo ip route add to 10.100.0.0/16 via 10.0.0.100
    vagrant@vagrant:~$ ip route
         default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
         10.0.0.0/24 dev dummy2 proto kernel scope link src 10.0.0.100
         10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15
         10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100
         10.10.0.0/16 via 10.0.0.100 dev dummy2
         10.100.0.0/16 via 10.0.0.100 dev dummy2
         192.168.10.0/24 dev dummy2 proto kernel scope link src 192.168.10.100
         192.168.33.0/24 dev eth1 proto kernel scope link src 192.168.33.10
    ```

3. Проверьте открытые TCP-порты в Ubuntu. Какие протоколы и приложения используют эти порты? Приведите несколько примеров.

```
vagrant@vagrant:~$ sudo ss -ntlp
State      Recv-Q     Send-Q     Local Address:Port     Peer Address:Port     Process
LISTEN     0          4096       127.0.0.53%lo:53       0.0.0.0:*             users:(("systemd-resolve",pid=606,fd=13))
LISTEN     0          128        0.0.0.0:22             0.0.0.0:*             users:(("sshd",pid=747,fd=3))
LISTEN     0          511        *:443                  *:*                   users:(("apache2",pid=885,fd=6),("apache2",pid=884,fd=6),("apache2",pid=650,fd=6))
LISTEN     0          511        *:80                   *:*                   users:(("apache2",pid=885,fd=4),("apache2",pid=884,fd=4),("apache2",pid=650,fd=4))
LISTEN     0          128        [::]:22                [::]:*                users:(("sshd",pid=747,fd=4))
```

4. Проверьте используемые UDP-сокеты в Ubuntu. Какие протоколы и приложения используют эти порты?

5. Используя diagrams.net, создайте L3-диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 

*В качестве решения пришлите ответы на вопросы, опишите, как они были получены, и приложите скриншоты при необходимости.*

 ---
 
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
