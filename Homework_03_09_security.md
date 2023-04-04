# Домашнее задание к занятию «Элементы безопасности информационных систем»

## Задание

1. Установите плагин Bitwarden для браузера. Зарегестрируйтесь и сохраните несколько паролей.

 - [x] Выполнена установка расширения Bitwarden для браузера Google Chrome.
 <p align="center"> <img src="https://user-images.githubusercontent.com/123832086/228743031-ce8cc12c-b8eb-4f88-8b79-f3a60d4235a8.png" width=30% height=30%> </p>

 - [x] Зарегистрирован пользователь и осуществлен вход.
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/228743638-0f617de8-9b26-4aa6-9061-0612bd2be8ba.png" width=50% height=50%> </p>

 - [x] Сохранены несколько логинов. 
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/228752491-84eca5b0-d6e9-4b80-85be-0fe14795c4dd.png" width=30% height=30%> </p>

2. Установите Google Authenticator на мобильный телефон. Настройте вход в Bitwarden-акаунт через Google Authenticator OTP.

* [x] Выполнена установка Google Authenticator на мобильный телефон и настроен вход в Bitwarden-акаунт через Google Authenticator OTP (двухэтапная аутентификация)
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/228757467-ce737754-90ae-4036-89c2-14ac6c47ee2c.png" width=50% height=50%> </p>

3. Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.

- Выполняю последовательно команды согласно презентации стр.18 (картинка ниже), а также статье `https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-20-04` на сервере VirtualBox, который смонтировали ранее в процессе подготовки домашнего задания, но на этапе загрузки своего сайта в браузере Google Chrome (https://127.0.0.1/) выдает ошибку **Не удается получить доступ к сайту**
<p align="left"> <img src="https://user-images.githubusercontent.com/123832086/229725638-aa0a750d-2270-4dfa-aa6f-e55c60407c3e.png" width=50% height=50%> </p>
<p align="right"> <img src="https://user-images.githubusercontent.com/123832086/229726726-b17ddd0b-17b8-4c94-be20-e278964dd759.png" width=50% height=50%> </p>

4. Проверьте на TLS-уязвимости произвольный сайт в интернете (кроме сайтов МВД, ФСБ, МинОбр, НацБанк, РосКосмос, РосАтом, РосНАНО и любых госкомпаний, объектов КИИ, ВПК и т. п.).

* [x] выполнена загрузка testsl.sh 3.1dev методом клонирования из git-репозитория: `git clone --depth 1 https://github.com/drwetter/testssl.sh.git`
* [x] запущен `testssl.sh`, который проверяет службу сервера на любом порту на предмет поддержки шифров TLS/SSL, протоколов, а также некоторых криптографических ошибок.
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229481772-8252c963-0a29-40d6-a931-2f4ae6cf0d9e.png" width=80% height=80%> </p>

5. Установите на Ubuntu SSH-сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.
 
6. Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH-клиента так, чтобы вход на удалённый сервер осуществлялся по имени сервера.

7. Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.

```
# Выполнена установка утилиты tcpdump
sudo apt install tcpdump
# Запущена утилита с указанием количества пакетов и записью в файл в формате .pcap
sudo tcpdump -c 100 -w dump.pcap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
100 packets captured
100 packets received by filter
0 packets dropped by kernel
# Открыт файл dump.pcap в Wireshark
```

---
 
## Задание со звёздочкой* 

Это самостоятельное задание, его выполнение необязательно.

8. Просканируйте хост scanme.nmap.org. Какие сервисы запущены?

9. Установите и настройте фаервол UFW на веб-сервер из задания 3. Откройте доступ снаружи только к портам 22, 80, 443.

----
