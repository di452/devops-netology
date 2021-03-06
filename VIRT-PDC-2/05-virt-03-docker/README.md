
# Домашнее задание к занятию "5.3. Введение. Экосистема docker run --name some-nginx -d some-content-nginx. Архитектура. Жизненный цикл Docker контейнера"

## Задача 1

Сценарий выполения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберете любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
Опубликуйте созданный форк в своем репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.

https://hub.docker.com/repository/docker/di452/nginx-test

## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- Высоконагруженное монолитное java веб-приложение;
- Nodejs веб-приложение;
- Мобильное приложение c версиями для Android и iOS;
- Шина данных на базе Apache Kafka;
- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
- Мониторинг-стек на базе Prometheus и Grafana;
- MongoDB, как основное хранилище данных для java-приложения;
- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

- Ответы:

Высоконагруженное монолитное java веб-приложение;

- физический сервер, т.к. монолитное, требуется изменение кода, т.к. высоконагруженное необходим доступ к ресурсами. 

Nodejs веб-приложение;
 - докер подходит, т.к. веб приложение. 

Мобильное приложение c версиями для Android и iOS;
 - Виртаулка. Приложение в докере не имеет GUI. 

Шина данных на базе Apache Kafka;
 - зависит от объема данных или контура (тестовый или прод). Для прода лучше Вируалка, для теста достаточно Докера. 

Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
 - Elasticsearch на виртуалку (отказоустойчивость), logstash и две ноды kibana в докер контейнер, или так же на виртуалках.

Мониторинг-стек на базе prometheus и grafana;
 - системы не хранят данные, можно развернуть на Докере (скорость развертывания, возможность масштабирования).

MongoDB, как основное хранилище данных для java-приложения;
 - Виртуальная машина, т.к. хранилище и хранение в контейнере не подходит для физического сервера.

Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.
 - класический кейс для контейнерной реализации Докер, данных хранить не требуется. 


## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тэгом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```;
- Добавьте еще один файл в папку ```/data``` на хостовой машине;
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

vagrant@vagrant:~$ docker pull centos
Using default tag: latest
latest: Pulling from library/centos
a1d0c7532777: Pull complete
Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
Status: Downloaded newer image for centos:latest
docker.io/library/centos:latest
vagrant@vagrant:~$ docker run -it -d --name mycentos -v /data:/data centos bash
386d6509b4602324a33826c31d9ada06ff74990504e49dca6599ca2feaef8c14

vagrant@vagrant:~$ docker pull debian
Using default tag: latest
latest: Pulling from library/debian
0c6b8ff8c37e: Pull complete
Digest: sha256:fb45fd4e25abe55a656ca69a7bef70e62099b8bb42a279a5e0ea4ae1ab410e0d
Status: Downloaded newer image for debian:latest
docker.io/library/debian:latest
vagrant@vagrant:~$ docker run -it -d --name mydebian -v /data:/data debian bash
8e2485b92ac9ae55cd03a04423df338291da5b9eda134f011b0e080bde4519b6

vagrant@vagrant:/$ docker exec -it mycentos bash
[root@386d6509b460 /]# echo mycentos > data/test
[root@386d6509b460 /]# cat data/test
mycentos
root@8e2485b92ac9:/# exit
exit
vagrant@vagrant:/$ sudo nano data/test
vagrant@vagrant:/$ sudo cat data/test
mycentos
localhost
vagrant@vagrant:/$ docker exec -it mydebian bash
root@8e2485b92ac9:/# cat data/test
mycentos
localhost

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

Соберите Docker образ с Ansible, загрузите на Docker Hub и пришлите ссылку вместе с остальными ответами к задачам.


---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---