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

**Шаг 6.** Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка — delay?

**Шаг 7.** Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой `dig`.

**Шаг 8.** Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой `dig`.

*В качестве ответов на вопросы приложите лог выполнения команд в консоли или скриншот полученных результатов.*

----

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.


### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки. 
