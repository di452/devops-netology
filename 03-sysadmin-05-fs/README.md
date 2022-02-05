# 3.4 Файловые системы

**Вопрос** №1: Узнайте о sparse (разряженных) файлах.

**Ответ**: 

**Вопрос** №2: Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

**Ответ**:

**Вопрос** №3: Сделайте vagrant destroy на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.provider :virtualbox do |vb|
    lvm_experiments_disk0_path = "/tmp/lvm_experiments_disk0.vmdk"
    lvm_experiments_disk1_path = "/tmp/lvm_experiments_disk1.vmdk"
    vb.customize ['createmedium', '--filename', lvm_experiments_disk0_path, '--size', 2560]
    vb.customize ['createmedium', '--filename', lvm_experiments_disk1_path, '--size', 2560]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk0_path]
    vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk1_path]
  end
end
Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.

**Ответ**: 

**Вопрос** №4: Используя fdisk, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство. 

**Ответ**:  ![img.png](img.png)

**Вопрос** №5: Используя sfdisk, перенесите данную таблицу разделов на второй диск.

**Ответ**: C помощью флага -d делаем образ системы и переносим на новый диск 

![img_4.png](img_4.png)

Результат: 

![img_1.png](img_1.png)

**Вопрос** №6: Соберите mdadm RAID1 на паре разделов 2 Гб.

**Ответ**: Создал RAID1 массив

![img_7.png](img_7.png)

**Вопрос** №7: Соберите mdadm RAID0 на второй паре маленьких разделов.

**Ответ**: Создал RAIDO массив 

![img_8.png](img_8.png)

**Вопрос** №8: Создайте 2 независимых PV на получившихся md-устройствах.

**Ответ**:  ![img_9.png](img_9.png)

**Вопрос** №9: Создайте общую volume-group на этих двух PV.

**Ответ**: ![img_10.png](img_10.png)

**Вопрос** №10: Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

**Ответ**: ![img_11.png](img_11.png)

**Вопрос** №11: Создайте mkfs.ext4 ФС на получившемся LV.

**Ответ**:  ![img_13.png](img_13.png)

**Вопрос** №12: Смонтируйте этот раздел в любую директорию, например, /tmp/new.

**Ответ**: ![img_14.png](img_14.png)

**Вопрос** №13: Поместите туда тестовый файл, например wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz.

**Ответ**: ![img_15.png](img_15.png)

**Вопрос** №14: Прикрепите вывод lsblk.

**Ответ**: ![img_16.png](img_16.png)

**Вопрос** №15: Протестируйте целостность файла:

root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0

**Ответ**: 

![img_18.png](img_18.png)

**Вопрос** №16: Используя pvmove, переместите содержимое PV с RAID0 на RAID1

**Ответ**:  

![img_19.png](img_19.png)

**Вопрос** №17: Сделайте --fail на устройство в вашем RAID1 md.

**Ответ**: 

**Вопрос** №18: Подтвердите выводом dmesg, что RAID1 работает в деградированном состоянии.

**Ответ**: 

**Вопрос** №19: Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:

root@vagrant:~# gzip -t /tmp/new/test.gz
root@vagrant:~# echo $?
0

**Ответ**:

**Вопрос** №20: Погасите тестовый хост, vagrant destroy.

**Ответ**: 
