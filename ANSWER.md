# Answer homework
====================
## Склонируйте репозиторий с исходным кодом Terraform
> git clone https://github.com/hashicorp/terraform.git
> cd .//terraform
## *В клонированном репозитории:*
### 1. Найдите полный хеш и комментарий коммита, хеш которого начинается на *aefea*.
> git show "aefea"
>>commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545  
>>Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>  
>>Date:   Thu Jun 18 10:29:58 2020 -0400  
>> Update CHANGELOG.md 
### 2. Какому тегу соответствует коммит *85024d3*?
> git show "85024d3"
>> (tag: v0.12.23)
### 3. Сколько родителей у коммита **b8d720**? Напишите их хеши
> git show "b8d720"
>> commit b8d720f8340221f2146e4e4870bf2ee0bc48f2d5  
>>> Merge:  
>>> - 56cd7859e0 (commit 56cd7859e05c36c06b56d013b55a252d0bb7e158)  
>>> - 9ea88f22fc (commit 9ea88f22fc6269854151c571162c5bcf958bee2b)
### 4.Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами **v0.12.23 и v0.12.24**
> git log v0.12.23..v0.12.24 --oneline   
>
- 33ff1c03bb (tag: v0.12.24) v0.12.24  
- b14b74c493 [Website] vmc provider links  
- 3f235065b9 Update CHANGELOG.mx  
- 6ae64e247b registry: Fix panic when server is unreachable  
- 5c619ca1ba website: Remove links to the getting started guide's old location  
- 06275647e2 Update CHANGELOG.md  
- d5f9411f51 command: Fix bug when using terraform login on Windows  
- 4b6d06cc5d Update CHANGELOG.md  
- dd01a35078 Update CHANGELOG.md  
- 225466bc3e Cleanup after v0.12.23 release

### 5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так ***func providerSource(...)*** (вместо троеточия перечислены аргументы).
> git log -S "func providerSource"
>>commit 8c928e83589d90a031f811fae52a81be7153e82f
>>>Author: Martin Atkins <mart@degeneration.co.uk>  
Date:   Thu Apr 2 18:04:39 2020 -0700

### 6. Найдите все коммиты в которых была изменена функция **globalPluginDirs**
> git grep -p "globalPluginDirs("  
> git log -L :globalPluginDirs:plugins.go
>>commit 78b12205587fe839f10d946ea3fdc06719decb05  
>>>Author: Pam Selle <204372+pselle@users.noreply.github.com>  
   Date:   Mon Jan 13 16:50:05 2020 -0500  
>
>>commit 52dbf94834cb970b510f2fba853a5b49ad9b1a46  
>>>Author: James Bardin <j.bardin@gmail.com>  
   Date:   Wed Aug 9 17:46:49 2017 -0400

### 7. Кто автор функции **synchronizedWriters**
> git log -S "synchronizedWriters"  
>> commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5  
>>> Author: Martin Atkins <mart@degeneration.co.uk>  
Date:   Wed May 3 16:25:41 2017 -0700
