## Домашнее задание к занятию "3.1 Работа в терминале, лекция 1"  

<details>

### 1. Установите средство виртуализации Oracle VirtualBox.

установлено

### 2. Установите средство автоматизации Hashicorp Vagrant.

установлено

### 3. В вашем основном окружении подготовьте удобный для дальнейшей работы терминал. Можно предложить:

установлен iTerm2

### 4. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

выполнено

### 5. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?  

RAM:1024mb  
CPU:2 cpu  
HDD:64gb  
video:4mb  

### 6. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?  

Добавлением команд в VagrantFile  
короткие линки  

  v.memory = 2048  
  v.cpus = 4  

или командами ВМ  

   config.vm.provider "virtualbox" do |vb|  
     vb.memory = "2048"  
     vb.cpu = "24"  
   end  

### 7. Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

выполнено

### 8. Ознакомиться с разделами man bash, почитать о настройках самого bash:

- какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?  

Число строк журнала задаётся переменной окружения HISTFILESIZE, она описана со строки 1060  

Число команд задаётся переменой окружения HISTSIZE, она описана со строки 1081  

 - что делает директива ignoreboth в bash? 

Директива ignoreboth является сокращением для ignorespace и ignoredups.

Если список значений включает в себя ignorespace, строки, начинающиеся с символа пробела, не сохраняются в списке истории.  
Значение ignoredups приводит к тому, что строки, соответствующие предыдущей записи в истории, не сохраняются.

### 9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?  

{} - зарезервированные слова, список, в т.ч. список команд, в отличие от () исполнятся в текущем инстансе, 
используется в различных условных циклах, условных операторах, или ограничивает тело функции. Статус возврата - это статус выхода из списка.  
Описана со строки 317 



### 10. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?  

100000 - да  
touch file{1..100000}  
300000 -  нет  
touch file{1..300000}  
  -bash: /usr/bin/touch: Argument list too long

### 11. В man bash поищите по `/\[\[`. Что делает конструкция `[[ -d /tmp ]]`  

Проверяет наличие каталога /tmp

### 12. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:  

bash is /tmp/new_path_directory/bash  
bash is /usr/local/bin/bash  
bash is /bin/bash  


$ ln -s /usr/bin /tmp/new_path_directory  
$ PATH=/tmp/new_path_directory:${PATH}  
$ type -a bash  
bash is /tmp/new_path_directory/bash  
bash is /usr/bin/bash  
bash is /bin/bash  

### 13. Чем отличается планирование команд с помощью batch и at?  

- at выполняется строго по расписанию  
- batch выполняется, когда позволит нагрузка на систему (load average упадёт ниже 1.5 или значения, заданного командой atd)  

### 14. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.  

% vagrant suspend

</details>

## Домашнее задание к занятию "2.4 Инструменты Git"

<details>

### 1. Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.

Решение  
git show aefea

**Ответ**  
aefead2207ef7e2aa5dc81a34aedf0cad4c32545  
Update CHANGELOG.md

### 2. Какому тегу соответствует коммит 85024d3?

Решение  
git show 85024

**Ответ**  
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)

### 3. Сколько родителей у коммита b8d720? Напишите их хеши.

Решение  
git show --pretty=format:' %P' b8d720

**Ответ**  
56cd7859e05c36c06b56d013b55a252d0bb7e158  
9ea88f22fc6269854151c571162c5bcf958bee2b

### 4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.

Решение  
git log  v0.12.23..v0.12.24  --oneline

**Ответ**  
33ff1c03b (tag: v0.12.24) v0.12.24  
b14b74c49 [Website] vmc provider links  
3f235065b Update CHANGELOG.md  
6ae64e247 registry: Fix panic when server is unreachable  
5c619ca1b website: Remove links to the getting started guide's old location  
06275647e Update CHANGELOG.md  
d5f9411f5 command: Fix bug when using terraform login on Windows  
4b6d06cc5 Update CHANGELOG.md  
dd01a3507 Update CHANGELOG.md  
225466bc3 Cleanup after v0.12.23 release  

### 5. Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).

Решение  
git log -S'func providerSource(' --oneline

**Ответ**  
8c928e835 main: Consult local directories as potential mirrors of providers

### 6. Найдите все коммиты в которых была изменена функция globalPluginDirs.

Решение  
git grep 'func globalPluginDirs'  
git log -L :'func globalPluginDirs':plugins.go --oneline  

**Ответ**  
commit 8364383c3 - создана  
commit 66ebff90c - изменена  
commit 41ab0aef7 - изменена  
commit 52dbf9483 - изменена  
commit 78b122055 - изменена  

### 7. Кто автор функции synchronizedWriters?

Решение  

git log -S'func synchronizedWriters(‘ --pretty=format:'%h - %an %ae'

bdfea50cc - James Bardin j.bardin@gmail.com  
5ac311e2a - Martin Atkins mart@degeneration.co.uk  

git show bdfea50cc - удалена  
git show 5ac311e2a - создана  

**Ответ**  
Author: Martin Atkins <mart@degeneration.co.uk>

</details>

## Домашнее задание к занятию "2.1 Системы контроля версий."

<details>

# devops-netology  
Игнорировать все файлы в директории .terraform  
Игнорировать все файлы оканчивающиеся на .tfstate и содержащие .tfstate.  
Игнорировать файл crash.log  
Игнорировать файлы оканчивающиеся на .tfvars  
Игнорировать файлы override.tf, override.tf и оканчивающиеся на _override.tf и _override.tf.json  
Игнорировать файлы .terraformrc и terraform.rc  
Игнорировать каталог .idea

</details>