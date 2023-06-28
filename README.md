APARECEN LAS CREDENCIALES DE KONNY EN LOS DOS PRIMEROS COMMITS PORQUE OLVIDÉ CERRAR SUS CREDENCIALES DE GIT GRAPH.


Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.33-0ubuntu0.22.04.2 (Ubuntu)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database campuslands;
Query OK, 1 row affected (0,01 sec)

mysql> show databases
    -> 
    -> show databases;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'show databases' at line 3
mysql> show database;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'database' at line 1
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| CRUD_PHP           |
| campuslands        |
| ejemploDB          |
| information_schema |
| mysql              |
| pais               |
| performance_schema |
| phpmyadmin         |
| sys                |
+--------------------+
9 rows in set (0,00 sec)

mysql> use campuslands;
Database changed
mysql> CREATE TABLE campers(idCamper int not null auto_increment, nombreCamper varchar(50) not null,
apellidoCamper varchar(50), fechaNac date, idReg int auto_increment);
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
mysql> CREATE TABLE campers(idCamper int not null auto_increment, nombreCamper varchar(50) not null,
apellidoCamper varchar(50), fechaNac date, idReg int auto_increment, primary key(idCamper));
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
mysql> CREATE TABLE campers(idCamper int not null auto_increment, nombreCamper varchar(50) not null,
apellidoCamper varchar(50), fechaNac date, idReg int, primary key(idCamper));
Query OK, 0 rows affected (0,03 sec)

mysql> SHOW TABLES;
+-----------------------+
| Tables_in_campuslands |
+-----------------------+
| campers               |
+-----------------------+
1 row in set (0,00 sec)

mysql> CREATE TABLE region(idReg int not null, nombreReg varchar(50) not null, idDep int not null, foreign key(idCamper));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 1
mysql> 
mysql> CREATE TABLE region(idReg int not null, nombreReg varchar(50) not null, idDep int not null, foreign key(idCamper));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 1
mysql> CREATE TABLE region(idReg int not null, nombreReg varchar(50) not null, idDep int not null, foreign key idCamper);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ')' at line 1
mysql> CREATE TABLE region(idReg int not null, nombreReg varchar(50) not null, idDep int not null, CONSTRAINT pk_region PRIMARY KEY (idReg));
Query OK, 0 rows affected (0,03 sec)

mysql> SHOW TABLES;
+-----------------------+
| Tables_in_campuslands |
+-----------------------+
| campers               |
| region                |
+-----------------------+
2 rows in set (0,00 sec)

mysql> describe region;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| idReg     | int         | NO   | PRI | NULL    |       |
| nombreReg | varchar(50) | NO   |     | NULL    |       |
| idDep     | int         | NO   |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
3 rows in set (0,00 sec)

mysql> describe campers;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| idCamper       | int         | NO   | PRI | NULL    | auto_increment |
| nombreCamper   | varchar(50) | NO   |     | NULL    |                |
| apellidoCamper | varchar(50) | YES  |     | NULL    |                |
| fechaNac       | date        | YES  |     | NULL    |                |
| idReg          | int         | YES  |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)

mysql> drop table region
    -> drop table region;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'drop table region' at line 2
mysql> DROP TABLE region;
Query OK, 0 rows affected (0,02 sec)

mysql> show tables;
+-----------------------+
| Tables_in_campuslands |
+-----------------------+
| campers               |
+-----------------------+
1 row in set (0,01 sec)

mysql> CREATE TABLE pais(idPais int not null auto_increment, nombrePais varchar(50) not null, CONSTRAINT pk_pais PRIMARY KEY (idPais));
Query OK, 0 rows affected (0,03 sec)

mysql> CREATE TABLE departamento(inDep int not null auto_increment, nombreDep varchar(50) not null, idPais int, CONSTRAINT pk_departamento PRIMARY KEY (inDep), CONSTRAINT fk_PaisDep FOREIGN KEY (idPais) REFERENCES pais(idPais));
Query OK, 0 rows affected (0,04 sec)

mysql> CREATE TABLE region(idReg int not null auto_increment, nombreReg varchar(50) not null, inDep int, CONSTRAINT pk_region PRIMARY KEY (idReg), CONSTRAINT fk_DepRegion FOREIGN KEY (idDep) REFERENCES departamento(idDep));
ERROR 1072 (42000): Key column 'idDep' doesn't exist in table
mysql> CREATE TABLE region(idReg int not null auto_increment, nombreReg varchar(50) not null, inDep int, CONSTRAINT pk_region PRIMARY KEY (idReg), CONSTRAINT fk_DepRegion FOREIGN KEY (inDep) REFERENCES departamento(inDep));
Query OK, 0 rows affected (0,03 sec)

mysql> SHOW TABLES;
+-----------------------+
| Tables_in_campuslands |
+-----------------------+
| campers               |
| departamento          |
| pais                  |
| region                |
+-----------------------+
4 rows in set (0,00 sec)

mysql> describe campers
    -> describe campers;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'describe campers' at line 2
mysql> DESCRIBE campers;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| idCamper       | int         | NO   | PRI | NULL    | auto_increment |
| nombreCamper   | varchar(50) | NO   |     | NULL    |                |
| apellidoCamper | varchar(50) | YES  |     | NULL    |                |
| fechaNac       | date        | YES  |     | NULL    |                |
| idReg          | int         | YES  |     | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)

mysql> DESCRIBE departamento;
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| inDep     | int         | NO   | PRI | NULL    | auto_increment |
| nombreDep | varchar(50) | NO   |     | NULL    |                |
| idPais    | int         | YES  | MUL | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
3 rows in set (0,01 sec)

mysql> DESCRIBE pais;
+------------+-------------+------+-----+---------+----------------+
| Field      | Type        | Null | Key | Default | Extra          |
+------------+-------------+------+-----+---------+----------------+
| idPais     | int         | NO   | PRI | NULL    | auto_increment |
| nombrePais | varchar(50) | NO   |     | NULL    |                |
+------------+-------------+------+-----+---------+----------------+
2 rows in set (0,00 sec)

mysql> DESCRIBE region;
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| idReg     | int         | NO   | PRI | NULL    | auto_increment |
| nombreReg | varchar(50) | NO   |     | NULL    |                |
| inDep     | int         | YES  | MUL | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
3 rows in set (0,00 sec)

mysql> ALTER TABLE campers ADD CONSTRAINT fk_CamperReg FOREIGN KEY (idReg) REFERENCES region(idReg);
Query OK, 0 rows affected (0,07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE campers;
+----------------+-------------+------+-----+---------+----------------+
| Field          | Type        | Null | Key | Default | Extra          |
+----------------+-------------+------+-----+---------+----------------+
| idCamper       | int         | NO   | PRI | NULL    | auto_increment |
| nombreCamper   | varchar(50) | NO   |     | NULL    |                |
| apellidoCamper | varchar(50) | YES  |     | NULL    |                |
| fechaNac       | date        | YES  |     | NULL    |                |
| idReg          | int         | YES  | MUL | NULL    |                |
+----------------+-------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)
