# Домашнее задание к занятию «Использование Python для решения типовых DevOps-задач»

------

## Задание 1

Есть скрипт:

```python
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b
```

### Вопросы:

| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной `c`?  | ошибка, пытаемся сложить разный тип переменных int и str |
| Как получить для переменной `c` значение 12?  | необходимо сложить строковый тип переменных, для этого следует изменить тип параметра `a`, str_c = str(a) + b |
| Как получить для переменной `c` значение 3?  | необходимо сложить целочисленный тип переменных, для этого следует изменить тип параметра `b`, int_c = a + int(b) |

------

## Задание 2

Мы устроились на работу в компанию, где раньше уже был DevOps-инженер. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. 

Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

```python

#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break

```

### Ваш скрипт:

```python
#!/usr/bin/env python3
import os
bash_command = ["cd ~/devops-netology", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
#is_change = False - исключена ненужная переменная
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:      ', '')
        #добавлена функция, которая возвращает текущий каталог
        print(os.getcwd() ,'/' , prepare_result, sep='')
        #break - исключено прерывание после первого успешного найденного значения
```

### Вывод скрипта при запуске во время тестирования:

```vim
dkard@DKard:~/devops-netology$ python3 homework_423.py
/home/dkard/devops-netology/    modified:   ANSWER.md
/home/dkard/devops-netology/    modified:   README.md
```

------

## Задание 3

Доработать скрипт выше так, чтобы он не только мог проверять локальный репозиторий в текущей директории, но и умел воспринимать путь к репозиторию, который мы передаём, как входной параметр. Мы точно знаем, что начальство будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

### Ваш скрипт:

```python
#!/usr/bin/env python3
import os
import sys
path=os.getcwd()
if len(sys.argv)!=1:
    path=sys.argv[1]
    bash_command = [f'cd {path}', 'git status 2>&1']
    result_os = os.popen(' && '.join(bash_command)).read()
    for result in result_os.split('\n'):
        if result.find('fatal') != -1:
            print('There is no GIT repository on the entered path')
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:      ', '')
            print(os.getcwd() ,'/' , prepare_result, sep='')
```

### Вывод скрипта при запуске во время тестирования:

```vim
dkard@DKard:~/devops-netology$ python3 homework_424.py /home/dkard/devops-netology
/home/dkard/devops-netology/    modified:   ANSWER.md
/home/dkard/devops-netology/    modified:   README.md
dkard@DKard:~/devops-netology$ python3 homework_424.py /home
There is no GIT repository on the entered path
```

------

## Задание 4

Наша команда разрабатывает несколько веб-сервисов, доступных по HTTPS. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. 

Проблема в том, что отдел, занимающийся нашей инфраструктурой, очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS-имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. 

Мы хотим написать скрипт, который: 

- опрашивает веб-сервисы; 
- получает их IP; 
- выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. 

Также должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена — оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: `drive.google.com`, `mail.google.com`, `google.com`.

### Ваш скрипт:

```python
#!/usr/bin/env python3
import socket
hosts = {'drive.google.com':'192.168.0.0', 'mail.google.com':'192.168.0.1', 'google.com':'192.168.0.2'}
while 1 == 1 :
    for host in hosts :
        ip = socket.gethostbyname(host)
        if ip != hosts[host] :
            print(' [ERROR] ' + str(host) +' IP mistmatch: '+hosts[host]+' '+ip)
            hosts[host]=ip
        else :
            print(str(host) + ' ' + ip)
```

### Вывод скрипта при запуске во время тестирования:

```vim
dkard@DKard:~/devops-netology$ python3 homework_425.py
 [ERROR] drive.google.com IP mistmatch: 192.168.0.0 64.233.164.194
 [ERROR] mail.google.com IP mistmatch: 192.168.0.1 142.250.150.17
 [ERROR] google.com IP mistmatch: 192.168.0.2 74.125.205.113
drive.google.com 64.233.164.194
mail.google.com 142.250.150.17
google.com 74.125.205.113
drive.google.com 64.233.164.194
mail.google.com 142.250.150.17
google.com 74.125.205.113
drive.google.com 64.233.164.194
mail.google.com 142.250.150.17
google.com 74.125.205.113
...
```
