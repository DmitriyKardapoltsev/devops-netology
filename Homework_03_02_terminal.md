# Домашнее задание к занятию «Работа в терминале. Лекция 2»

------

## Задание

Ответьте на вопросы:

1. Какого типа команда `cd`? Попробуйте объяснить, почему она именно такого типа: опишите ход своих мыслей и поясните, если считаете, что она могла бы быть другого типа.

	**Ответ:**
- команда `change directory` является встроенной `cd is a shell builtin` в оболочку, иначе для изменения текущей директории потребуется запускать отдельный дополнительный процесс, а также, в случае сбоев, либо случайных некорректных изменений, можно будет восстановить функционал и работоспособность системы.

2. Какая альтернатива без pipe для команды `grep <some_string> <some_file> | wc -l`?   

	* [x] Изучите [документ](http://www.smallo.ruhr.de/award.html) о других подобных некорректных вариантах использования pipe.
	
	**Ответ:**
- команда `| - pipe` позволяет связать между собой в данном случае утилиту `grep` поиска и утилиту `wc` подсчета данных, `-l` выводит количество строк в объекте. Таким образом мы производим поиск некоторых строк в файле, а потом производим подсчет этих строк. 
- Функциона `grep` содержит внутреннюю установку для подсчета строк, а, именно, опция `grep -c` выведет количество совпадающих строк в файле.
- Поэтому вместо `grep <some_string> <some_file> | wc -l` нужно использовать команду `grep -с <some_string> <some_file>`

3. Какой процесс с PID `1` является родителем для всех процессов в вашей виртуальной машине Ubuntu 20.04?

	**Ответ:**
- Для всех процессов с PPID `1` в виртуальной машине является родитель с PID `1` созданный пользователем `root` (суперпользователь) по команде `systemd` 
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/226164123-10c42305-4edd-4a95-b775-7a5dbf7499e7.png" width=60% height=60% "PID_1"> </p>

4. Как будет выглядеть команда, которая перенаправит вывод stderr `ls` на другую сессию терминала?

	**Ответ:**
- Для `ls` (на примере отсутствующей директории `/test`) команда для вывода ошибки в другой терминал будет выглядеть следующим образом `ls /test 2> /dev/pts/0`
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/226168355-10f4541a-4327-4cfb-8aad-74f2bd4339f1.png" width=80% height=80% "stderr_ls_term_1_print_0"> </p>

5. Получится ли одновременно передать команде файл на stdin и вывести её stdout в другой файл? Приведите работающий пример.

	**Ответ:**
- Да, получится. Пример приведен ниже для стандартного потока данных при помощи команды `tee` (файл остается прежним) и отдельно для записи файла.
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/226171367-31a805e4-1ba9-46e2-a9d3-682600ebf1bf.png" width=60% height=60% "stdin_stout_command_tee"> </p>

- Команда `cat` принимает данные из файла `input.txt` и выводит (в данном случае добавляет `>>` вместо `>`) в файл `output.txt` 
<p align="center"> <img src="https://user-images.githubusercontent.com/123832086/226169607-00354a3f-5e4b-4b4d-8000-f3b766e2011d.png" width=60% height=60% "stdin_stout_other_file"> </p>

6. Получится ли, находясь в графическом режиме, вывести данные из PTY в какой-либо из эмуляторов TTY? Сможете ли вы наблюдать выводимые данные?

	**Ответ:**
* Если отправим данные нахоядсь в графическом режиме, например, ` echo 'hello' >/dev/tty1`, то PTY вывод мы не увидим, а в эмуляторе TTY выведется `hello`   

7. Выполните команду `bash 5>&1`. К чему она приведёт? Что будет, если вы выполните `echo netology > /proc/$$/fd/5`? Почему так происходит?

	**Ответ:**
```
# Команда `bash 5>&1` создает файловый дискриптор и перенаправляет его в стандартный вывод данных.
	vagrant@vagrant:~$ bash 5>&1
	vagrant@vagrant:~$ lsof -p $$
		COMMAND  PID    USER   FD   TYPE DEVICE SIZE/OFF    NODE NAME
		bash    1605 vagrant  cwd    DIR  253,0     4096 1314079 /home/vagrant
		bash    1605 vagrant  rtd    DIR  253,0     4096       2 /
		bash    1605 vagrant  txt    REG  253,0  1183448  131546 /usr/bin/bash
		bash    1605 vagrant  mem    REG  253,0    51856  137862 /usr/lib/x86_64-linux-gnu/libnss_files-2.31.so
		bash    1605 vagrant  mem    REG  253,0  3035952  131073 /usr/lib/locale/locale-archive
		bash    1605 vagrant  mem    REG  253,0  2029592  137717 /usr/lib/x86_64-linux-gnu/libc-2.31.so
		bash    1605 vagrant  mem    REG  253,0    18848  137735 /usr/lib/x86_64-linux-gnu/libdl-2.31.so
		bash    1605 vagrant  mem    REG  253,0   192032  137935 /usr/lib/x86_64-linux-gnu/libtinfo.so.6.2
		bash    1605 vagrant  mem    REG  253,0    27002  266488 /usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache
		bash    1605 vagrant  mem    REG  253,0   191504  137676 /usr/lib/x86_64-linux-gnu/ld-2.31.so
		bash    1605 vagrant    0u   CHR  136,0      0t0       3 /dev/pts/0
		bash    1605 vagrant    1u   CHR  136,0      0t0       3 /dev/pts/0
		bash    1605 vagrant    2u   CHR  136,0      0t0       3 /dev/pts/0
		bash    1605 vagrant    5u   CHR  136,0      0t0       3 /dev/pts/0
		bash    1605 vagrant  255u   CHR  136,0      0t0       3 /dev/pts/0
# Команда `echo netology > /proc/$$/fd/5` перенаправляет вывод слова netology в созданный дискриптор 5, а тот, в свою очередь, перенаправляет на стандартный вывод данных (задано ранее при создании дискриптора). В следствие чего, мы увидим слово netology на экране терминала
	vagrant@vagrant:~$ echo netology > /proc/$$/fd/5
		netology
```

8. Получится ли в качестве входного потока для pipe использовать только stderr команды, не потеряв отображение stdout на pty?  
	Напоминаем: по умолчанию через pipe передаётся только stdout команды слева от `|` на stdin команды справа.
Это можно сделать, поменяв стандартные потоки местами через промежуточный новый дескриптор, который вы научились создавать в предыдущем вопросе.

**Ответ:**
```
# Да, получится, если использовать промежуточный дескриптор. Перенаправляем поток данных из 5u и 2u (stderr) в 1u (stdout), а затем stdout напраляем в 5u, тем самым не потеряв вывод stdout.
vagrant@vagrant:~$ cat file 5>&1 2>&1 1>&5 | grep 'No such file'
cat: file: No such file or directory
```

9. Что выведет команда `cat /proc/$$/environ`? Как ещё можно получить аналогичный по содержанию вывод?

**Ответ:**

* Команда `cat /proc/$$/environ` выводит переменные окружения. Аналогичный по содержанию вывод у команды `env`

10. Используя `man`, опишите, что доступно по адресам `/proc/<PID>/cmdline`, `/proc/<PID>/exe`.

**Ответ:**
* По данным адресам доступнf папка с файловой системой `proc` для каждого запущенного в системе процесса с номером `PID`. Каталог `cmdline` содержит команду с помощью которой был запущен процесс, а также переданные ей параметры, `exe` - ссылкe на исполняемый файл, из которого вызвана программ с номером `PID`.

11. Узнайте, какую наиболее старшую версию набора инструкций SSE поддерживает ваш процессор с помощью `/proc/cpuinfo`.

```
# Наиболее старшая версия инструкций sse4_1
	vagrant@vagrant:~$ grep sse /proc/cpuinfo
		flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm 		constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni ssse3 cx16 pcid sse4_1 ss
	4_2 popcnt hypervisor lahf_lm invpcid_single ibrs_enhanced fsgsbase invpcid md_clear flush_l1d arch_capabilities
		flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm 		constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni ssse3 cx16 pcid sse4_1 ss
	4_2 popcnt hypervisor lahf_lm invpcid_single ibrs_enhanced fsgsbase invpcid md_clear flush_l1d arch_capabilities

```

12. При открытии нового окна терминала и `vagrant ssh` создаётся новая сессия и выделяется pty.  
	Это можно подтвердить командой `tty`, которая упоминалась в лекции 3.2.  
	
	Однако:

    ```bash
	vagrant@netology1:~$ ssh localhost 'tty'
	not a tty
    ```

	Почитайте, почему так происходит и как изменить поведение.

**Ответ:**

* Фраза `ssh localhost 'tty'` передает команду на выполнение, под нее не создается терминал. Используя флаг `-t` будет принудительно выделяться псевдотерминал.

13. Бывает, что есть необходимость переместить запущенный процесс из одной сессии в другую. Попробуйте сделать это, воспользовавшись `reptyr`. Например, так можно перенести в `screen` процесс, который вы запустили по ошибке в обычной SSH-сессии.

**Ответ:**
```
# Запустил процесс top
	vagrant@vagrant:~$ top
		top - 07:10:01 up  1:14,  1 user,  load average: 0.00, 0.00, 0.00
		Tasks: 107 total,   1 running, 106 sleeping,   0 stopped,   0 zombie
		%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.2 si,  0.0 st
		MiB Mem :    976.7 total,    170.8 free,    137.3 used,    668.5 buff/cache
		MiB Swap:   1953.0 total,   1953.0 free,      0.0 used.    685.7 avail Mem

    		PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    		392 root      20   0       0      0      0 I   0.3   0.0   0:06.45 kworker/0:4-events
   		1923 vagrant   20   0    9236   4020   3368 R   0.3   0.4   0:00.05 top
# Перевел в фоновый режим
		[1]+  Stopped                 top
# Возобновил процесс в фоновом режиме
	vagrant@vagrant:~$ bg
		[1]+ top &
# Отключил процесс от текущего родителя и запустил терминальный мультплексор tmux
	vagrant@vagrant:~$ disown top
		-bash: warning: deleting stopped job 1 with process group 1923
	vagrant@vagrant:~$ jobs
	vagrant@vagrant:~$ ps -a
    		PID TTY          TIME CMD
   		1923 pts/0    00:00:00 top
   		1927 pts/0    00:00:00 ps
	vagrant@vagrant:~$ tmux
# Подключиться к фоновому процессу не удалось (я так понимаю недостаточно прав)
	vagrant@vagrant:~$ reptyr 1923
		Unable to attach to pid 1923: Operation not permitted
		The kernel denied permission while attaching. If your uid matches
		the target's, check the value of /proc/sys/kernel/yama/ptrace_scope.
		For more information, see /etc/sysctl.d/10-ptrace.conf
# Отключили мультиплексор терминала Ctrl+B d
# Отключился от сервера
	vagrant@vagrant:~$ exit
		logout
		Connection to 127.0.0.1 closed.
# Повторное подключение
	PS C:\vagrant2> vagrant ssh
		Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 5.4.0-135-generic x86_64)
		.....
# Подключение к существующей сессии мультиплексора
	vagrant@vagrant:~$ tmux attach
# Информация сохранилась
	vagrant@vagrant:~$ reptyr 1923
		Unable to attach to pid 1923: Operation not permitted
		The kernel denied permission while attaching. If your uid matches
		the target's, check the value of /proc/sys/kernel/yama/ptrace_scope.
		For more information, see /etc/sysctl.d/10-ptrace.conf
	vagrant@vagrant:~$
	vagrant@vagrant:~$
```

14. `sudo echo string > /root/new_file` не даст выполнить перенаправление под обычным пользователем, так как перенаправлением занимается процесс shell, который запущен без `sudo` под вашим пользователем. Для решения этой проблемы можно использовать конструкцию `echo string | sudo tee /root/new_file`. Узнайте, что делает команда `tee` и почему в отличие от `sudo echo` команда с `sudo tee` будет работать.

**Ответ:**

* Команда `tee` записывает вывод любой команды в файл (или несколько файлов) и в стандартный вывод. В примере `echo string | sudo tee /root/new_file` команда читает стандартный ввод, перенаправленный через `pipe` в стандартный вывод, а так как команда запущена от `sudo`, поэтому имеет права на запись.
----

