А вот так нельзя сделать? мне так проще чем через копирования файла. ( если делать через копирования то мы создаем файл index.html, заполняем его и в докерфайле в RUN пишем COPY index.html /usr/share/nginx/html/ )

**root@vagrant:~# mc**

**root@vagrant:/home/vagrant/Docker# vi Dockerfile**
**root@vagrant:/home/vagrant/Docker# cat Dockerfile**

FROM nginx:stable

RUN echo '<html><head>Hey, Netology</head><body><h1>I am DevOps Engineer!</h1></body></html>' > /usr/share/nginx/html/index.html

**docker build -f Dockerfile -t saisprm\netlogy:nginx-1.0.4 .**

Sending build context to Docker daemon 2.048kB
Step 1/2 : FROM nginx:stable
 ---> 404359394820
Step 2/2 : RUN echo '<html><head>Hey, Netology</head><body><h1>I am DevOps Engineer!</h1></body></html>' > /usr/share/nginx/html/index.html
 ---> Running in ca759fe7eea9
Removing intermediate container ca759fe7eea9
 ---> 4b5089722127
Successfully built 4b5089722127
Successfully tagged saisprmnetlogy:nginx-1.0.4

**root@vagrant:~# docker run --name test1 -p 80:80 -d saisprmnetlogy:nginx-1.0.4**

**root@vagrant:~# curl localhost**

<html><head>Hey, Netology</head><body><h1>I am DevOps Engineer!</h1></body></html>
