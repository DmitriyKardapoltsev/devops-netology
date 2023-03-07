# Домашнее задание к занятию "Работа в терминале. Лекция 1"

### Цель задания

> В результате выполнения этого задания вы:
> 1. Научитесь работать с базовым функционалом инструмента VirtualBox, который помогает с быстрой разверткой виртуальных машин.
> 2. Научитесь работать с документацией в формате man, чтобы ориентироваться в этом полезном и мощном инструменте документации.
> 3. Ознакомитесь с функциями Bash (PATH, HISTORY, batch/at), которые помогут комфортно работать с оболочкой командной строки (шеллом) и понять некоторые его ограничения.

***
### Инструкция к заданию

1. Установите средство виртуализации [Oracle VirtualBox](https://www.virtualbox.org/).

![image](https://user-images.githubusercontent.com/123832086/221342763-ec55ef81-066b-4380-ae22-be82a5e68652.png "VirtualBox")

2. Установите средство автоматизации [Hashicorp Vagrant](https://hashicorp-releases.yandexcloud.net/vagrant/).
>\> wsl --install
>![image](https://user-images.githubusercontent.com/123832086/221344397-708997b8-9ddd-4092-abf7-09e0e4a65816.png)
>![image](https://user-images.githubusercontent.com/123832086/221344520-709cc749-bba8-4733-8b3e-11c9c8ef8ae7.png "Установка на Windows WSL")
>![image](https://user-images.githubusercontent.com/123832086/221347076-21e1e858-7123-4464-b234-d8fe14d13fc3.png "Ubunta reg")
![image](https://user-images.githubusercontent.com/123832086/221348571-a98b5674-1104-4e66-be0c-ad09791f119d.png)
![image](https://user-images.githubusercontent.com/123832086/221348723-59983584-29a5-4468-bd3a-b048fa61065a.png)

3. В вашем основном окружении подготовьте удобный для дальнейшей работы терминал. Можно предложить:

	* iTerm2 в Mac OS X
	* Windows Terminal в Windows
	* выбрать цветовую схему, размер окна, шрифтов и т.д.
	* почитать о кастомизации PS1/применить при желании.

	Несколько популярных проблем:
	* Добавьте Vagrant в правила исключения перехватывающих трафик для анализа антивирусов, таких как Kaspersky, если у вас возникают связанные с SSL/TLS ошибки,
	* MobaXterm может конфликтовать с Vagrant в Windows,
	* Vagrant плохо работает с директориями с кириллицей (может быть вашей домашней директорией), тогда можно либо изменить [VAGRANT_HOME](https://www.vagrantup.com/docs/other/environmental-variables#vagrant_home), либо создать в системе профиль пользователя с английским именем,
	* VirtualBox конфликтует с Windows Hyper-V и его необходимо [отключить](https://www.vagrantup.com/docs/installation#windows-virtualbox-and-hyper-v),
	
	![image](https://user-images.githubusercontent.com/123832086/221343246-dc7d8486-1fab-4206-8a72-81e613669a29.png "Отключение Hyper-V")

	
	* [WSL2](https://docs.microsoft.com/ru-ru/windows/wsl/wsl2-faq#does-wsl-2-use-hyper-v-will-it-be-available-on-windows-10-home) использует Hyper-V, поэтому с ним VirtualBox также несовместим,
	* аппаратная виртуализация (Intel VT-x, AMD-V) должна быть активна в BIOS,
	* в Linux при установке [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads) может дополнительно потребоваться пакет `linux-headers-generic` (debian-based) / `kernel-devel` (rhel-based).


### Инструменты/ дополнительные материалы, которые пригодятся для выполнения задания

1. [Конфигурация VirtualBox через Vagrant](https://www.vagrantup.com/docs/providers/virtualbox/configuration.html)
2. [Использование условий в Bash](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html)

------

## Задание

1. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

	* Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните `vagrant init`. Замените содержимое Vagrantfile по умолчанию следующим:

		```bash
		Vagrant.configure("2") do |config|
			config.vm.box = "bento/ubuntu-20.04"
		end
		```
![VargantFile](https://user-images.githubusercontent.com/123832086/221364803-603e599f-6047-4424-bf23-921f3c01bb81.png "VargantFile")

	* Выполнение в этой директории `vagrant up` установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

![Login VargantCloud](https://user-images.githubusercontent.com/123832086/221364769-e292ed73-60fb-48a4-8aa1-8c6dcd1daaf1.png "Vargant Cloud")

![Vagrant_ready](https://user-images.githubusercontent.com/123832086/223360057-51e51084-800c-4556-b6fc-655e5e9aff41.png "Machine_ready")

	* `vagrant suspend` выключит виртуальную машину с сохранением ее состояния (т.е., при следующем `vagrant up` будут запущены все процессы внутри, которые работали на момент вызова suspend)

![Vagrant_suspend](https://user-images.githubusercontent.com/123832086/223360500-c4ca6249-fa61-48fc-a6f6-1adf46487c86.png "Vagrant_suspend")
	
	* `vagrant halt` выключит виртуальную машину штатным образом.

![Vagrant_halt](https://user-images.githubusercontent.com/123832086/223361237-30416655-e7ed-48ca-9b1d-72e98ac2a093.png "Vagrant_halt")

2. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?
	
	* _VirtualBox менеджер существует дисплей созданной виртуальной машины, где отображается командная строка._
	
	* _По умолчанию выделено 2 ядра процессора, оперативной памяти 1024 МБ, описан порядок загрузки дисков._\
3. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: [документация](https://www.vagrantup.com/docs/providers/virtualbox/configuration.html). Как добавить оперативной памяти или ресурсов процессора виртуальной машине?



4. Команда `vagrant ssh` из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

5. Ознакомьтесь с разделами `man bash`, почитайте о настройках самого bash:
    * какой переменной можно задать длину журнала `history`, и на какой строчке manual это описывается?
   Страница 3 
   ![image](https://user-images.githubusercontent.com/123832086/221367288-1b52d778-08c0-4e27-8b55-e1d4596ad2e1.png "History man")

    * что делает директива `ignoreboth` в bash?
6. В каких сценариях использования применимы скобки `{}` и на какой строчке `man bash` это описано?
7. С учётом ответа на предыдущий вопрос, как создать однократным вызовом `touch` 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?
8. В man bash поищите по `/\[\[`. Что делает конструкция `[[ -d /tmp ]]`
9. Сделайте так, чтобы в выводе команды `type -a bash` первым стояла запись с нестандартным путем, например bash is ... 
Используйте знания о просмотре существующих и создании новых переменных окружения, обратите внимание на переменную окружения PATH 

	```bash
	bash is /tmp/new_path_directory/bash
	bash is /usr/local/bin/bash
	bash is /bin/bash
	```
	(прочие строки могут отличаться содержимым и порядком)
    В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

10. Чем отличается планирование команд с помощью `batch` и `at`?

11. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.

*В качестве решения дайте ответы на вопросы свободной форме* 

---

### Правила приема домашнего задания

- В личном кабинете отправлена ссылка на .md файл в вашем репозитории.

### Критерии оценки

Зачет - выполнены все задания, ответы даны в развернутой форме, приложены соответствующие скриншоты и файлы проекта, в выполненных заданиях нет противоречий и нарушения логики.

На доработку - задание выполнено частично или не выполнено, в логике выполнения заданий есть противоречия, существенные недостатки. 
