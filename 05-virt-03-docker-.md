**Задача 1**

Сценарий выполения задачи:

-   создайте свой репозиторий на [https://hub.docker.com](https://hub.docker.com/);
-   выберете любой образ, который содержит веб-сервер Nginx;
-   создайте свой fork образа;
-   реализуйте функциональность: запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:

\<html\>

\<head\>

Hey, Netology

\</head\>

\<body\>

\<h1\>I’m DevOps Engineer!\</h1\>

\</body\>

\</html\>

Опубликуйте созданный форк в своем репозитории и предоставьте ответ в виде ссылки на <https://hub.docker.com/username_repo>.

**https://hub.docker.com/layers/saisprm/netology:nginx-1.0.1**

**Задача 2**

Посмотрите на сценарий ниже и ответьте на вопрос: "Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.

\--

Сценарий:

-   Высоконагруженное монолитное java веб-приложение;

    
*Изначально поставлено условие* **Высоконагруженное монолитное java веб-приложение** *лучше всего подойдет тут физический сервер, в крайнем случае, виртуальная машина, докер тут точно не подойдет.*

-   Nodejs веб-приложение;

    
*В данном случае как раз докер нам подходит т.к это веб-приложение.*

-   Мобильное приложение c версиями для Android и iOS;

    
*В данном варианте я бы за основу взял виртуальную машину для простоты использования/тестирования.*

-   Шина данных на базе Apache Kafka;

    
В данном случаее надо исходить из критичности потери данных, если потеря данных не критична то для теста в полне достаточно докера, если же критично то физически сервер или виртуалка.

-   Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;

    
Исходя из предложенного кластера и прочитав документацию по данным продуктам, я сделал выводы что elasticsearch в данном случаее будем размещать на физическом\\виртуальном сервере, более того если среда высоконагруженная то только физический сервер. А вот kibana и logstash в виде контейнера могут быть реализованы.

-   Мониторинг-стек на базе Prometheus и Grafana;

    
От Grafana есть официальный образ, Prometheus тоже есть много образов т.к данные не хранятся в приложениях вполне себе хороший вариант использовать докер.

-   MongoDB, как основное хранилище данных для java-приложения;

    
Реализовать через контейнеризацию конечно можно, но заранее создавать себе проблем не вижу смысла, достаточно проблематично реализовать администрирование этой СУБД и я думаю высока вероятность случайного удаления данных. В данном случае я бы предпочел физический хост.

-   Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.

    Docker Registry делаем в контейнере, есть даже инструкция на оф.сайте как это делается, а Gitlab сервер для реализации CI/CD процессов надо выбирать исходя из ресурсов, если ресурсы позволяют содержать свой хост/вирт.машину то лучше так, если нет реализовываем с помощью докера.

**Задача 3**

-   Запустите первый контейнер из образа **centos** c любым тэгом в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
-   Запустите второй контейнер из образа **debian** в фоновом режиме, подключив папку /data из текущей рабочей директории на хостовой машине в /data контейнера;
-   Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data;
-   Добавьте еще один файл в папку /data на хостовой машине;
-   Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.

root@vagrant:\~\# docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

**root@vagrant:\~\# docker run -v /data:/data -dt --name centos centos**

Unable to find image 'centos:latest' locally

latest: Pulling from library/centos

a1d0c7532777: Pull complete

Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177

Status: Downloaded newer image for centos:latest

91bef156367e4367a173ccc4c045452e25de5ca4a0eeb73acfe56742124df229

**root@vagrant:\~\# docker run -v /data:/data -dt --name debian debian**

Unable to find image 'debian:latest' locally

latest: Pulling from library/debian

a8ca11554fce: Pull complete

Digest: sha256:3066ef83131c678999ce82e8473e8d017345a30f5573ad3e44f62e5c9c46442b

Status: Downloaded newer image for debian:latest

0d09a79b2d3e0233711934b677e3c9a3e5b141c768e9bed36968ea1b243a987a

**root@vagrant:\~\# docker ps**

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

0d09a79b2d3e debian "bash" 23 seconds ago Up 19 seconds debian

91bef156367e centos "/bin/bash" About a minute ago Up About a minute centos

**root@vagrant:\~\# docker exec -it centos /bin/bash**

[root@91bef156367e /]\# echo 'Centos'\>/data/centos

[root@91bef156367e /]\# exit

exit

**root@vagrant:\~\# echo 'file-host'\>/data/host**

**root@vagrant:\~\# docker exec -it debian /bin/bash**

**root@0d09a79b2d3e:/\# ls -la /data**

total 16

drwxr-xr-x 2 root root 4096 Nov 22 12:40 .

drwxr-xr-x 1 root root 4096 Nov 22 12:36 ..

\-rw-r--r-- 1 root root 7 Nov 22 12:38 centos

\-rw-r--r-- 1 root root 10 Nov 22 12:40 host

**root@0d09a79b2d3e:/\# cat /data/centos**

Centos

**root@0d09a79b2d3e:/\# cat /data/host**

file-host
