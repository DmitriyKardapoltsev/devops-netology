# Домашнее задание к занятию «Компьютерные сети. Лекция 1»

### Цель задания

В результате выполнения задания вы: 

* научитесь работать с HTTP-запросами, чтобы увидеть, как клиенты взаимодействуют с серверами по этому протоколу;
* поработаете с сетевыми утилитами, чтобы разобраться, как их можно использовать для отладки сетевых запросов, соединений.

### Чеклист готовности к домашнему заданию

1. Убедитесь, что у вас установлены необходимые сетевые утилиты — dig, traceroute, mtr, telnet.
2. Используйте `apt install` для установки пакетов.

```
* Утилиты (dig, traceroute, mtr, telnet) установлены.
```

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

```
# Выполнено подключение к виртуальному серверу Vagrant Ubuntu 20.04.
# Выполнено подключение и отправлен HTTP-запрос.
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
    Via: 1.1 varnish
    X-Served-By: cache-fra-eddf8230066-FRA
    X-Cache: MISS
    X-Cache-Hits: 0
    X-Timer: S1681729784.674971,VS0,VE1
    X-DNS-Prefetch-Control: off

    <!DOCTYPE html>
    <html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <title>Forbidden - Stack Exchange</title>
        <style type="text/css">
                    body
                    {
                            color: #333;
                            font-family: 'Helvetica Neue', Arial, sans-serif;
                            font-size: 14px;
                            background: #fff url('img/bg-noise.png') repeat left top;
                            line-height: 1.4;
                    }
                    h1
                    {
                            font-size: 170%;
                            line-height: 34px;
                            font-weight: normal;
                    }
                    a { color: #366fb3; }
                    a:visited { color: #12457c; }
                    .wrapper {
                            width:960px;
                            margin: 100px auto;
                            text-align:left;
                    }
                    .msg {
                            float: left;
                            width: 700px;
                            padding-top: 18px;
                            margin-left: 18px;
                    }
        </style>
    </head>
    <body>
        <div class="wrapper">
                    <div style="float: left;">
                            <img src="https://cdn.sstatic.net/stackexchange/img/apple-touch-icon.png" alt="Stack Exchange" />
                    </div>
                    <div class="msg">
                            <h1>Access Denied</h1>
                            <p>This IP address (88.80.60.161) has been blocked from access to our services. If you believe this to be in error, please contact us at <a href="mailto:team@stackexchange.com?Subject=Blocked%2088.80.60.161%20(Request%20ID%3A%202955911997-FRA)">team@stackexchange.com</a>.</p>
                            <p>When contacting us, please include the following information in the email:</p>
                            <p>Method: block</p>
                            <p>XID: 2955911997-FRA</p>
                            <p>IP: 88.80.60.161</p>
                            <p>X-Forwarded-For: </p>
                            <p>User-Agent: </p>

                            <p>Time: Mon, 17 Apr 2023 11:09:43 GMT</p>
                            <p>URL: stackoverflow.com/questions</p>
                            <p>Browser Location: <span id="jslocation">(not loaded)</span></p>
                    </div>
            </div>
            <script>document.getElementById('jslocation').innerHTML = window.location.href;</script>
    </body>
    </html>Connection closed by foreign host.

# Аналогичная ошибка, если запрос отправлять с команой строки Ubuntu, установленной на Windows.

  dkard@DKard:~$ sudo telnet stackoverflow.com 80
    [sudo] password for dkard:
    Trying 151.101.65.69...
    Connected to stackoverflow.com.
    Escape character is '^]'.
    GET /questions HTTP/1.0
    HOST: stackoverflow.com

      HTTP/1.1 403 Forbidden
      Connection: close
      Content-Length: 1920
      Server: Varnish
      Retry-After: 0
      Content-Type: text/html
      Accept-Ranges: bytes
      Date: Fri, 14 Apr 2023 07:44:49 GMT
      Via: 1.1 varnish
      X-Served-By: cache-fra-eddf8230127-FRA
      X-Cache: MISS
      X-Cache-Hits: 0
      X-Timer: S1681458289.275038,VS0,VE1
      X-DNS-Prefetch-Control: off

      <!DOCTYPE html>
      <html>
      <head>
          <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
          <title>Forbidden - Stack Exchange</title>
          <style type="text/css">
                      body
                      {
                              color: #333;
                              font-family: 'Helvetica Neue', Arial, sans-serif;
                              font-size: 14px;
                              background: #fff url('img/bg-noise.png') repeat left top;
                              line-height: 1.4;
                      }
                      h1
                      {
                              font-size: 170%;
                              line-height: 34px;
                              font-weight: normal;
                      }
                      a { color: #366fb3; }
                      a:visited { color: #12457c; }
                      .wrapper {
                              width:960px;
                              margin: 100px auto;
                              text-align:left;
                      }
                      .msg {
                              float: left;
                              width: 700px;
                              padding-top: 18px;
                              margin-left: 18px;
                      }
          </style>
      </head>
      <body>
          <div class="wrapper">
                      <div style="float: left;">
                              <img src="https://cdn.sstatic.net/stackexchange/img/apple-touch-icon.png" alt="Stack Exchange" />
                      </div>
                      <div class="msg">
                              <h1>Access Denied</h1>
                              <p>This IP address (92.39.215.225) has been blocked from access to our services. If you believe this to be in error, please contact us at <a href="mailto:team@stackexchange.com?Subject=Blocked%2092.39.215.225%20(Request%20ID%3A%202899392748-FRA)">team@stackexchange.com</a>.</p>
                              <p>When contacting us, please include the following information in the email:</p>
                              <p>Method: block</p>
                              <p>XID: 2899392748-FRA</p>
                              <p>IP: 92.39.215.225</p>
                              <p>X-Forwarded-For: </p>
                              <p>User-Agent: </p>

                              <p>Time: Fri, 14 Apr 2023 07:44:49 GMT</p>
                              <p>URL: stackoverflow.com/questions</p>
                              <p>Browser Location: <span id="jslocation">(not loaded)</span></p>
                      </div>
              </div>
              <script>document.getElementById('jslocation').innerHTML = window.location.href;</script>
      </body>
      </html>Connection closed by foreign host.

```

**Шаг 2.** Повторите задание 1 в браузере, используя консоль разработчика F12:

 - откройте вкладку `Network`;
 - отправьте запрос [http://stackoverflow.com](http://stackoverflow.com);
 - найдите первый ответ HTTP-сервера, откройте вкладку `Headers`;
 - укажите в ответе полученный HTTP-код;
 - проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 - приложите скриншот консоли браузера в ответ.

**Шаг 3.** Какой IP-адрес у вас в интернете?

**Шаг 4.** Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`.

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
