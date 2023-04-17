# Домашнее задание к занятию «Компьютерные сети. Лекция 1»

### Цель задания

В результате выполнения задания вы: 

* научитесь работать с HTTP-запросами, чтобы увидеть, как клиенты взаимодействуют с серверами по этому протоколу;
* поработаете с сетевыми утилитами, чтобы разобраться, как их можно использовать для отладки сетевых запросов, соединений.

### Чеклист готовности к домашнему заданию

1. Убедитесь, что у вас установлены необходимые сетевые утилиты — dig, traceroute, mtr, telnet.
2. Используйте `apt install` для установки пакетов.

* [x] Утилиты (dig, traceroute, mtr, telnet) установлены.


### Дополнительные материалы для выполнения задания

1. Полезным дополнением к обозначенным выше утилитам будет пакет net-tools. Установить его можно с помощью команды `apt install net-tools`.
2. RFC протокола HTTP/1.0, в частности [страница с кодами ответа](https://www.rfc-editor.org/rfc/rfc1945#page-32).
3. [Ссылки на другие RFC для HTTP](https://blog.cloudflare.com/cloudflare-view-http3-usage/).

------

## Задание

**Шаг 1.** Работа c HTTP через telnet.

- Подключитесь утилитой telnet к сайту stackoverflow.com:

`telnet stackoverflow.com 80`
 
- Отправьте HTTP-запрос:

```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
*В ответе укажите полученный HTTP-код и поясните, что он означает.*

***Ответ:***

```
# Выполнено подключение к виртуальному серверу Vagrant Ubuntu 20.04.
# Выполнено подключение к stacoverflow.com и отправлен HTTP-запрос.
  vagrant@vagrant:~$ telnet stackoverflow.com 80
  Trying 151.101.193.69...
  Connected to stackoverflow.com.
  Escape character is '^]'.
  GET /questions HTTP/1.0
  HOST: stackoverflow.com

    HTTP/1.1 403 Forbidden
    Connection: close
    Content-Length: 1917
    Server: Varnish
    Retry-After: 0
    Content-Type: text/html
    Accept-Ranges: bytes
    Date: Mon, 17 Apr 2023 11:09:43 GMT
# Выдало ошибку на запрет подключения.
# Выполнено подключение к netology.ru и выполнен аналогичный запрос.
    vagrant@vagrant:~$ telnet netology.ru 80
        Trying 188.114.99.234...
        Connected to netology.ru.
        Escape character is '^]'.
        GET /questions HTTP/1.0
        HOST: netology.ru

        HTTP/1.1 301 Moved Permanently
        Date: Mon, 17 Apr 2023 11:25:29 GMT
        Connection: close
        Cache-Control: max-age=3600
        Expires: Mon, 17 Apr 2023 12:25:29 GMT
        Location: https://netology.ru/questions
        Server: cloudflare
        CF-RAY: 7b944eb84ce43609-FRA
        alt-svc: h3=":443"; ma=86400, h3-29=":443"; ma=86400

        Connection closed by foreign host.
# Ошибка 301 указывает на то, что ресурс навсегда перемещен в локацию с HTTPS с сохранением адреса (https://netology.ru/questions).
```

**Шаг 2.** Повторите задание 1 в браузере, используя консоль разработчика F12:

- [x] откройте вкладку `Network`;

- [x] отправьте запрос [http://netology.ru](http://netology.ru);
 
 - [x] найдите первый ответ HTTP-сервера, откройте вкладку `Headers`;
 
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/232476160-4bacfb85-2e39-4906-b30c-d20995f228c1.png" width=80% height=80% "> </p>
 
 - [x] укажите в ответе полученный HTTP-код;
 
    Код 307 Internal Redirect. Перенаправление на протокол HTTPS.
 
 - [x] проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 
    Время загрузки страницы 42сек. Дольше всего обрабатывался первый запрос 513 мсек.
 
 - [x] приложите скриншот консоли браузера в ответ.

<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/232482189-334fbdb5-5865-49e3-becc-897d724dec3c.png" width=80% height=80% "> </p>
 
**Шаг 3.** Какой IP-адрес у вас в интернете?

<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/232483673-3d6cadaa-aff8-46f4-b7f3-d79b405e14dd.png" width=80% height=80% "> </p>

**Шаг 4.** Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`.

 ***Ответ:***
 
 Провайдер JSC "Cable tv Mark", система AS39001

 ```
     vagrant@vagrant:~$ whois 88.80.60.161
            % This is the RIPE Database query service.
            % The objects are in RPSL format.
            %
            % The RIPE Database is subject to Terms and Conditions.
            % See http://www.ripe.net/db/support/db-terms-conditions.pdf

            % Note: this output has been filtered.
            %       To receive output for a database update, use the "-B" flag.

            % Information related to '88.80.54.0 - 88.80.61.255'

            % Abuse contact for '88.80.54.0 - 88.80.61.255' is 'abuse@mtu.ru'

            inetnum:        88.80.54.0 - 88.80.61.255
            netname:        TVIN-NET
            descr:          JSC "Cable tv Mark"
            country:        RU
            admin-c:        MIN24-RIPE
            tech-c:         MIN24-RIPE
            status:         ASSIGNED PA
            mnt-by:         MNT-NEWTONE
            mnt-lower:      MNT-NEWTONE
            mnt-routes:     MNT-NEWTONE
            created:        2006-12-06T15:08:04Z
            last-modified:  2012-04-10T07:53:26Z
            source:         RIPE

            role:           PJSC "Mobile TeleSystems", Izhevsk NOC fix
            address:        36, Dzerginskogo st.
            abuse-mailbox:  noc@izh.mts.ru
            address:        Izhevsk, 426000, Russian Federation
            admin-c:        AA30998-RIPE
            admin-c:        MG24450-RIPE
            admin-c:        RA9077-RIPE
            tech-c:         AA30998-RIPE
            tech-c:         MG24450-RIPE
            tech-c:         RA9077-RIPE
            remarks:        -------------------------------------------------
            remarks:        Please report SPAM and Network security issues to
            remarks:        noc@izh.mts.ru
            remarks:        -------------------------------------------------
            nic-hdl:        MIN24-RIPE
            mnt-by:         MNT-NEWTONE
            created:        2012-04-09T08:55:16Z
            last-modified:  2018-02-07T05:38:27Z
            source:         RIPE # Filtered

            % Information related to '88.80.32.0/19AS39001'

            route:          88.80.32.0/19
            descr:          Newtone
            origin:         AS39001
            mnt-by:         MNT-NEWTONE
            created:        2005-11-30T05:29:55Z
            last-modified:  2005-11-30T08:22:43Z
            source:         RIPE # Filtered

            % This query was served by the RIPE Database Query Service version 1.106 (BUSA)
```

**Шаг 5.** Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`.

***Ответ:***
 
Пакет проходит через AS - AS39001, AS8359, AS15169
 
 ```
    dkard@DKard:~$ traceroute -An 8.8.8.8
        traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
         1  * 172.22.64.1 [*]  0.283 ms  0.774 ms
         2  192.168.1.1 [*]  2.258 ms  2.227 ms  2.826 ms
         3  88.80.48.1 [AS39001]  5.416 ms  5.328 ms  5.321 ms
         4  88.80.38.128 [AS39001]  5.271 ms  5.964 ms  5.876 ms
         5  212.188.61.141 [AS8359]  9.773 ms  6.761 ms  6.359 ms
         6  212.188.2.221 [AS8359]  13.563 ms  15.188 ms  12.492 ms
         7  * * *
         8  * * *
         9  108.170.250.33 [AS15169]  27.393 ms 108.170.250.129 [AS15169]  26.817 ms 108.170.227.90 [AS15169]  26.722 ms
        10  108.170.250.146 [AS15169]  27.113 ms 108.170.250.130 [AS15169]  27.270 ms 108.170.250.83 [AS15169]  26.623 ms
        11  142.250.238.214 [AS15169]  43.624 ms 142.251.237.156 [AS15169]  39.905 ms *
        12  74.125.253.109 [AS15169]  47.365 ms 142.250.235.62 [AS15169]  40.977 ms 142.250.235.68 [AS15169]  43.111 ms
        13  142.250.210.45 [AS15169]  40.833 ms 172.253.51.221 [AS15169]  40.566 ms 172.253.51.245 [AS15169]  41.410 ms
        14  * * *
        15  * * *
        16  * * *
        17  * * *
        18  * * *
        19  * * *
        20  * * *
        21  * * *
        22  * * *
        23  8.8.8.8 [AS15169/AS263411]  40.557 ms * * 
```

**Шаг 6.** Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка — delay?

***Ответ:***
 
 Наибольшая задержка пакета на AS15169 Hostname 66.249.95.224
 
 <p align="center"> <img src="https://user-images.githubusercontent.com/123832086/232558261-cce2252d-af70-4792-837c-880b50c069da.png" width=60% height=60% "> </p>

**Шаг 7.** Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой `dig`.

```
dkard@DKard:~$ dig +short NS dns.google
    ns4.zdns.google.
    ns3.zdns.google.
    ns1.zdns.google.
    ns2.zdns.google.
dkard@DKard:~$ dig +short A dns.google
    8.8.8.8
    8.8.4.4
```

**Шаг 8.** Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой `dig`.

***Ответ:***

```
dkard@DKard:~$ dig -x 8.8.8.8

; <<>> DiG 9.18.1-1ubuntu1.3-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 59374
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 30 msec
;; SERVER: 172.22.64.1#53(172.22.64.1) (UDP)
;; WHEN: Mon Apr 17 21:20:20 +04 2023
;; MSG SIZE  rcvd: 82

dkard@DKard:~$ dig -x 8.8.4.4

; <<>> DiG 9.18.1-1ubuntu1.3-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21980
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 19 msec
;; SERVER: 172.22.64.1#53(172.22.64.1) (UDP)
;; WHEN: Mon Apr 17 21:20:33 +04 2023
;; MSG SIZE  rcvd: 82
```
