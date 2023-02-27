# Домашнее задание к занятию "2. SQL"

## Введение

Перед выполнением задания вы можете ознакомиться с [дополнительными материалами](https://github.com/netology-code/virt-homeworks/blob/virt-11/additional/README.md).

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume, в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/docker-compose.jpg)

## Задача 2

В БД из задачи 1:

- создайте пользователя test-admin-user и БД test_db
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.1.jpg)
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.2.jpg))
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.3.jpg)
- создайте пользователя test-simple-user
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.4.jpg)
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.5.jpg)

Таблица orders:

- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:

- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:

- итоговый список БД после выполнения пунктов выше,
  
  ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.6.jpg)
- описание таблиц (describe)
  
 ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.7.jpg)
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
  
  test=# SELECT grantee, table_catalog, table_name, privilege_type FROM information_schema.table_privileges WHERE table_name IN ('orders','clients');
- список пользователей с правами над таблицами test_db
  
![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/2.8.jpg)

## Задача 3

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

| Наименование | цена |
| ------------ | ---- |
| Шоколад      | 10   |
| Принтер      | 3000 |
| Книга        | 500  |
| Монитор      | 7000 |
| Гитара       | 4000 |

Таблица clients

| ФИО                  | Страна проживания |
| -------------------- | ----------------- |
| Иванов Иван Иванович | USA               |
| Петров Петр Петрович | Canada            |
| Иоганн Себастьян Бах | Japan             |
| Ронни Джеймс Дио     | Russia            |
| Ritchie Blackmore    | Russia            |

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/3.1.jpg)

Используя SQL синтаксис:

- вычислите количество записей для каждой таблицы
- приведите в ответе:
  - запросы
  - результаты их выполнения.
    
 ![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/3.1.jpg)

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

| ФИО                  | Заказ   |
| -------------------- | ------- |
| Иванов Иван Иванович | Книга   |
| Петров Петр Петрович | Монитор |
| Иоганн Себастьян Бах | Гитара  |

Приведите SQL-запросы для выполнения данных операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.

SELECT* FROM clients WHERE заказ IS NOT NULL;

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/Screenshot_1.jpg)

Подсказк - используйте директиву `UPDATE`.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/4.1.jpg)

## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 (используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/5.1.jpg)

Исходя из ответа мы видим что база данных выполнит последовательное сканирование таблицы clients, чтобы найти строки удовлетворяющие условию WHERE в запросе, где cost=0.00..18.10 это затраченные ресурсы, rows=806 это количество строк которые потребуется обработать БД, а width=72 обозначает ширину строки

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/6,1.jpg)

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/6,2.jpg)

Поднимите новый пустой контейнер с PostgreSQL.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/6,3.jpg)

Восстановите БД test_db в новом контейнере.

![image](https://github.com/SaisPRM/devops-netology/blob/main/06-db-02-sql/pic/6.4.jpg)

Приведите список операций, который вы применяли для бэкапа данных и восстановления.
