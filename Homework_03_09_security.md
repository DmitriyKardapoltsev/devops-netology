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

~~***3. Установите apache2, сгенерируйте самоподписанный сертификат, настройте тестовый сайт для работы по HTTPS.***~~

* Запуск командной строки Windows PowerShell от имени администратора
* Развертывание и запуск виртуальной машины на VirtualBox Ububtu-20.04. Текст **VagrantFile** приведен ниже.
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/ubuntu-20.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.10"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
 config.vm.provider "virtualbox" do |v|
 v.memory = 1024
 v.cpus = 2
end
end
```
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229989236-bfee36f5-4f95-4354-99c8-ab033f5899ba.png" width=60% height=60%> </p>

* Подключение к виртуальной машине vagrant
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229983927-de918d48-d75a-4ec7-aa71-745b67a4b30c.png" width=60% height=60%> </p>

* Обновление локального пакета, установка `apache2`, открытие портов `http` и `https`
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229984951-1a518a9a-b2b1-4f37-af1e-56d3a88198e6.png" width=50% height=50%> </p>

* Включение модуля `mod_ssl` Apache, обеспечивающего поддержку шифрования SSL. Перезапуск Apache для активации модуля.
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229985149-fa77e179-6729-448c-9b56-1267f63d0bef.png" width=70% height=70%> </p>

* Создание SSL-сертификата командой `openssl`
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229985602-4ddd8d8e-5b00-41db-acf3-215c59fe495f.png" width=70% height=70%> </p>

* Настройка Apache

```
# создание и открытие файла конфигурации
vagrant@vagrant:~$ sudo vim /etc/apache2/sites-available/www.example.com.conf
```

* Конфигурация VirtualHost
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229986684-b8a0a2b4-eb42-4e8a-a854-e840e64bd478.png" width=70% height=70%> </p>

* Создание `DocumentRoot` и помещение в него HTML

```
vagrant@vagrant:~$ sudo mkdir /var/www/www.example.com
vagrant@vagrant:~$ sudo vim /var/www/www.example.com/index.html
<h1>it worked!</h1>
```

* Включение файла конфигурации при помощи `a2ensite`, проверка ошибок конфигурации, перезагрузка Apache
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229988271-7683a17f-d326-4b58-bb2c-ada79be664e2.png" width=70% height=70%> </p>

* загрузка своего сайта в браузере GoogleChrome
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229988680-d4511259-039a-408a-8b19-5af9a37e6b4d.png" width=70% height=70%> </p>

* Запуск `curl`
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229989919-a97cc7c5-c847-4019-b8d4-9296b64942db.png" width=70% height=70%> </p>


------------------
- Выполняю последовательно команды согласно презентации стр.18 (картинка ниже), а также статье `https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-20-04` на сервере VirtualBox, который смонтировали ранее в процессе подготовки домашнего задания, но на этапе загрузки своего сайта в браузере Google Chrome (https://127.0.0.1/) выдает ошибку **Не удается получить доступ к сайту**
<p align="left"> <img src="https://user-images.githubusercontent.com/123832086/229725638-aa0a750d-2270-4dfa-aa6f-e55c60407c3e.png" width=50% height=50%> </p>
<p align="right"> <img src="https://user-images.githubusercontent.com/123832086/229726726-b17ddd0b-17b8-4c94-be20-e278964dd759.png" width=50% height=50%> </p>

4. Проверьте на TLS-уязвимости произвольный сайт в интернете (кроме сайтов МВД, ФСБ, МинОбр, НацБанк, РосКосмос, РосАтом, РосНАНО и любых госкомпаний, объектов КИИ, ВПК и т. п.).

* [x] выполнена загрузка testsl.sh 3.1dev методом клонирования из git-репозитория: `git clone --depth 1 https://github.com/drwetter/testssl.sh.git`
* [x] запущен `testssl.sh`, который проверяет службу сервера на любом порту на предмет поддержки шифров TLS/SSL, протоколов, а также некоторых криптографических ошибок.
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229481772-8252c963-0a29-40d6-a931-2f4ae6cf0d9e.png" width=80% height=80%> </p>

~~***5. Установите на Ubuntu SSH-сервер, сгенерируйте новый приватный ключ. Скопируйте свой публичный ключ на другой сервер. Подключитесь к серверу по SSH-ключу.***~~
 
~~***6. Переименуйте файлы ключей из задания 5. Настройте файл конфигурации SSH-клиента так, чтобы вход на удалённый сервер осуществлялся по имени сервера.***~~

7. Соберите дамп трафика утилитой tcpdump в формате pcap, 100 пакетов. Откройте файл pcap в Wireshark.

```
# Выполнена установка утилиты tcpdump
dkard@DKard:~$ sudo apt install tcpdump
# Запущена утилита с указанием количества пакетов и записью в файл в формате .pcap
dkard@DKard:~$ sudo tcpdump -c 100 -w dump.pcap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
100 packets captured
100 packets received by filter
0 packets dropped by kernel
# Открыт файл dump.pcap в Wireshark
```
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/229748410-b822f39d-ee91-418e-ac51-b27d5d6882c2.png" width=80% height=80% "Dump.pcap"> </p>

---
 
## Задание со звёздочкой* 

Это самостоятельное задание, его выполнение необязательно.

8. Просканируйте хост scanme.nmap.org. Какие сервисы запущены?

9. Установите и настройте фаервол UFW на веб-сервер из задания 3. Откройте доступ снаружи только к портам 22, 80, 443.

----
