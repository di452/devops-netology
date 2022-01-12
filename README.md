# **# Дополнение к заданию 3.1.**

Задание 10 - Почему именно стэка? Как это получилось определить?

По "гуглил" ошибку что выходит и решил что это из за стэка. Где это почитать и узнать??   


Задание 11 - Что проверяет `-d /tmp` ? 

**Ответ**: Команда `[-d /tmp]` проверяет, существует ли файл, и является ли он директорией.
Как она работает не понимаю, у меня при обработке это команды выходит "bash: [-d: No such file or directory" хотя есть и папка и файл с таким названием.


# 3.1. Работа в терминале, лекция 1
**Вопрос**: Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?

**Ответ**:

ОЗУ:1024mb

Процессор:1

HDD:64gb

VGA:8mb

**Вопрос**: Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

**Ответ**:
Добавляем комманды в VagrantFile в нашей директрории на локальной машине:
 
v.memory = 1024
  
v.cpus = 2
или командами ВМ

config.vm.provider "virtualbox" do |vb|

vb.memory = "1024"

vb.cpu = "2"

**Вопрос**: какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?

**Ответ**:
1. HISTFILESIZE - максимальное число строк в файле истории для сохранения, 
Номер строчки в man 1155
2. HISTSIZE - число команд для сохранения  , 
Номер строчки в man 1178

**Вопрос**: Что делает директива ignoreboth в bash?

**Ответ**: Директива `ignoreboth` - это команда сочетает действия команд `ignorespace` и `ignoredups`. Она не запишет в журнал команды начинающиеся с пробела и совпадающие с последней выполненной командой.

**Вопрос**: В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?

**Ответ**: { } - это зарезервированные слова, список, в т.ч. список команд команд в отличии от "(...)" исполнятся в текущем инстансе, 
используется в различных условных циклах, условных операторах, или ограничивает тело функции.
В командах выполняет подстановку элементов из списка , если упрощенно то цикличное выполнение команд с подстановкой 
например touch {1..10} - создаст файлы с именами 1 до 9.
строка 343

**Вопрос**: С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

**Ответ**: Вводим команду `touch` c параметром {1..100000}. Создадутся файлы с 1 до 99999. Создать так же 300000 не возможно из за превышения размера стэка памяти равного = 8192 Kb. Лимиты этотой оболочки можно посомотреть командой `ulimit -a`   

**Вопрос**: В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

**Ответ**: Конструкция [[ -d /tmp ]] возвращает 0 или 1 в зависимости от выражения внутри.

**Вопрос**: Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:

bash is /tmp/new_path_directory/bash

bash is /usr/local/bin/bash

bash is /bin/bash

(прочие строки могут отличаться содержимым и порядком) В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

**Ответ**: Вводим команды:

vagrant@vagrant:~$ `mkdir` /tmp/new_path_directory/

vagrant@vagrant:~$ `cp` /bin/bash /tmp/new_path_directory/

vagrant@vagrant:~$ `type` -a bash

bash is /usr/bin/bash

bash is /bin/bash

vagrant@vagrant:~$ PATH=/tmp/new_path_directory/:$PATH

vagrant@vagrant:~$ type -a bash

bash is /tmp/new_path_directory/bash

bash is /usr/bin/bash

bash is /bin/bash

**Вопрос**: Чем отличается планирование команд с помощью `batch` и `at`?

**Ответ**: 
Команда `batch` дословно : выполняет команды, когда позволяют уровни загрузки системы; другими словами, когда средняя нагрузка падает ниже 1,5 или значения, указанного при вызове atd.
Команда `at` запускается в заданное время.
Команды не разбирались на лекций, как они работают не имею представления. 