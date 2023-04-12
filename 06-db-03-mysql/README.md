# Домашнее задание к занятию 3. «MySQL»

## Задача 1

Используя Docker, поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_1.jpg)
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_2.jpg)
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_3.jpg)
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_4.jpg)

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/virt-11/06-db-03-mysql/test_data) и восстановитесь из него.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_5.jpg)

Перейдите в управляющую консоль `mysql` внутри контейнера.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_7.jpg)

Используя команду `\h`, получите список управляющих команд.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_8.jpg)

Найдите команду для выдачи статуса БД и **приведите в ответе** из её вывода версию сервера БД.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_9.jpg)

Подключитесь к восстановленной БД и получите список таблиц из этой БД.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_10.jpg)

**Приведите в ответе** количество записей с `price` > 300.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_11.jpg)

В следующих заданиях мы будем продолжать работу с этим контейнером.

## Задача 2

Создайте пользователя test в БД c паролем test-pass, используя:

- плагин авторизации mysql_native_password
- срок истечения пароля — 180 дней
- количество попыток авторизации — 3
- максимальное количество запросов в час — 100
- аттрибуты пользователя:
  - Фамилия "Pretty"
  - Имя "James".

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_12.jpg)

Предоставьте привелегии пользователю `test` на операции SELECT базы `test_db`.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_13.jpg)

Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES, получите данные по пользователю `test` и **приведите в ответе к задаче**.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_15.jpg)

## Задача 3

Установите профилирование `SET profiling = 1`. Изучите вывод профилирования команд `SHOW PROFILES;`.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_17.jpg)

Исследуйте, какой `engine` используется в таблице БД `test_db` и **приведите в ответе**.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_18.jpg)

Измените `engine` и **приведите время выполнения и запрос на изменения из профайлера в ответе**:

- на `MyISAM`,
- на `InnoDB`.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_19.jpg)

## Задача 4

Изучите файл `my.cnf` в директории /etc/mysql.

Измените его согласно ТЗ (движок InnoDB):

- скорость IO важнее сохранности данных;
- нужна компрессия таблиц для экономии места на диске;
- размер буффера с незакомиченными транзакциями 1 Мб;
- буффер кеширования 30% от ОЗУ;
- размер файла логов операций 100 Мб.

Приведите в ответе изменённый файл `my.cnf`.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_20.jpg)
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-03-mysql/screen/Screenshot_21.jpg)

p.s параметры взяты от сюда солгасно ТЗ [MySQL :: MySQL 8.0 Reference Manual :: 15 The InnoDB Storage Engine](https://dev.mysql.com/doc/refman/8.0/en/innodb-storage-engine.html)
