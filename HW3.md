```
Задание:
1) запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/
2) добавить в контейнер hostname такой же, как hostname системы через переменную
3) заполнить БД данными через консоль
4) запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны 
```

```
**Создаем папку в корне**
cd /
sudo mkdir testdb

**Запускаем контейнер с MySql**
sudo docker run --name mydb -h host -e MYSQL_ROOT_PASSWORD=123 -d -v /testdb:/var/lib/mysql mysql

**Заходим в контейнер**
sudo docker exec -it mydb bash

**Заходим в mysql**
mysql -h 127.0.0.1 -u root -p

123

**Создаем базу данных**
CREATE DATABASE public;

**Создаем таблицу**
CREATE TABLE public.persons (id int PRIMARY KEY, lastName varchar(255), firstName varchar(255), address varchar(255));

**Заполняем таблицу**
INSERT INTO public.persons                                                                                            
    (id, firstname, lastname, address)
VALUES
    (1, 'Leha', 'Pupirishkin', 'Rododendron'),
    (2, 'Lena', 'Kuksova', 'Samara'),
    (3, 'Miha', 'Solnishkin', 'Paris');

**Проверяем таблицу**
SELECT * FROM  public.persons;

**Выходим из mysql**
\q

**Выходим из контейнера**
exit

**Запускаем контейнер с phpmyadmin**
sudo docker run -d --name php --link mydb:db -p 8082:80 phpmyadmin/phpmyadmin

**Для проверки заходим в браузер и пишем localhost:8082
Далее вводим логин - root и пароль 123**

```

