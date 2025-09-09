# 📘 MySQL Basics -
```
## 1. What is MySQL?
MySQL is a popular open-source relational database management system (RDBMS).  
It helps to store, manage, and retrieve data in tables.

## 2. what is Data ?
Any sort of information that is stored is called Data.
example : -> message & multimedia on Whatsapp
          -> products & order on Amazon 

## 3. what is Data base ?
An organized collection of data is called Data base.

## 4. what is data base management system (DBMS) ?
A software that is used to easily store and access data from the database in a secured way.

## 5. what is relational DBMS ?
Relational database organize the data in the form of tables.
example: oracle, postgre SQL, MySQL, SQLite, IBM etc.

## 6. Non- Relational DBMS ?
Non relational database store the data in a non tabular form.
example: Mongodb, Cassandra, Couchdb, Dynamodb etc.

--------------------------------------------------------------------------------------------------

## Categories of SQL command:
DDL -> To define structure ( CREATE, ALTER, DROP, TRUNCATE)
DML -> Manage Data (INSERT, UPDATE, DELETE)
DQL -> Query Data (SELECT)
DCL -> Control access (GRANT, REVOKE)
TCL -> Manage transaction (COMMIT, ROLLBACK, SAVEPOINT)

---------------------------------------------------------------------------------------------------
## SQL workflow or Commands
Database -> Table -> Insert -> Update -> Alter -> Delete -> Drop

## DATA TYPES
DATA TYPE: integer, float, string, text, date, time, datetime, boolean
SYNTAX: int, float, varchar, text, date, time,datetime, (0-false, 1-true)
----------------------------------------------------------------------------------------------------

### Create a Database
syntax : create database {database_name}
Query: CREATE DATABASE school;

# Output:
Query OK, 1 row affected (0.68 sec)

## To show available Database in system
Query: show databases;

# Output:   
+--------------------+
| Database           |
+--------------------+          
| collagedb          | 
| practise           |
| school             |
| sys                |
| universitydb       |
+--------------------+
---------------------------------------------------------------
## USE DATABASE : switch to a database before creating table
syntax: use {database_name}
Query: USE school;
# Output:
mysql> use school;
Database changed
---------------------------------------------------------------

## To create a table:
syntax: create table table_name (column_name, data type, constraints)
Query: CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    city VARCHAR(50)
);

## Describe tables: the DESCRIBE (or DESC) command is used to show the structure (schema) of a table.
syntax: DESCRIBE table_name; or DESC table_name;
Query: DESCRIBE students;

# Output:

mysql> desc student;
+--------------+---------------+------+-----+---------+----------------+
| Field        | Type          | Null | Key | Default | Extra          |
+--------------+---------------+------+-----+---------+----------------+
| class        | varchar(10)   | YES  |     | NULL    |                |
| name         | varchar(25)   | YES  |     | NULL    |                |
| student_id   | int           | NO   | PRI | NULL    | auto_increment |
| age          | int           | YES  |     | NULL    |                |
| father_name  | varchar(50)   | YES  |     | NULL    |                |
| mother_name  | varchar(50)   | YES  |     | NULL    |                |
| phone_number | varchar(15)   | YES  |     | NULL    |                |
| address      | varchar(100)  | YES  |     | NULL    |                |
| birthdate    | date          | YES  |     | NULL    |                |
| fees         | decimal(10,2) | YES  |     | NULL    |                | 
+--------------+---------------+------+-----+---------+----------------+ 
----------------------------------------------------------------------------------
## INSERT: To Insert Data or add details into the table: 
Query: INSERT INTO students (name, age, city)
        VALUES ('Ravi', 20, 'Mysore'),
       ('Anita', 22, 'Bangalore'),
       ('John', 21, 'Chennai');

## SELECT: To retrive data or view data: 
syntax: select * from table_name;
Query: SELECT * FROM students;
# Output:
+-------+----------+------------+------+-------------+-------------+--------------+----------------+------------+----------+
| class | name     | student_id | age  | father_name | mother_name | phone_number | address        | birthdate  | fees     | 
+-------+----------+------------+------+-------------+-------------+--------------+----------------+------------+----------+
| X     | moon     |          7 |   16 | dayanand    | jyothi      | 8197728782   | mysore         | 1997-04-03 | 25000.00 | 
| VI    | sidd     |         10 |   13 | swamy       | gowri       | 7740102055   | mysore         | 1996-11-10 |  7443.20 | 
| IX    | chaitra  |        120 |   15 | shiva       | NULL        | 7022782664   | narasipura     | 1997-12-07 | 20000.00 | 
| VI    | shashi   |        200 |   12 | shankar     | lakshmi     | 94876952     | mandya         | 2000-06-10 |  7443.20 | 
| X     | chinku   |        201 |   16 | premram     | ramabhai    | 7090608050   | Mysore         | 1997-12-21 | 25000.00 | 
| X     | kaveri   |        202 |   16 | shivaramu   | lakshmi     | 7090120913   | madikeri       | 1997-08-13 | 25000.00 |
+-------+----------+------------+------+-------------+-------------+--------------+----------------+------------+----------+
-------------------------------------------------------------------
## ALTER TABLE: to modify structure or modify existing table
(TO ADD new column)
syntax: alter table table_name ADD column_name datatype;
Query: alter Table student add remarks varchar(100); 

(TO Modify column name)
syntax: alter table table_name RENAME column column_name to new_column_name;
Query: alter table student rename column phone_number to contact_Detail; 

(To modify column datatype for example varchar to int or int to varchar)
syntax: alter table table_name MODIFY column_name datatype;
Query: alter table student modify contact_detail bigint;

---------------------------------------------------------------------------------------
## UPDATE: To update or change in existing table
syntax: update table_name set column1 = value where condition;
Query: update student set name = 'chandra' where student_id = 7;

## DELETE: To delete existing records from table 
specific row
syntax: delete from table_name where condition;
Query: delete from student where name = 'kaveri';

## Delete all rows but keep table
synatx: delete from table_name;
Query: delete from student;

## DROP: To delete entire table or data structure 
syntax: drop table table_name;
Query: drop table student;

## delete database permanently
syntax: drop database database_name;
Query: drop database school;
------------------------------------------------------------------------------------------------------
## NOTE: 
-> we can write a query either small letter or capital letter
        
## Real-World Example

Think of students as a school database.
Each student has:
student_id → Roll number
name → Student’s name
age → Student’s age
city → Place where the student lives

This is how schools manage student records in databases.
------------------------------------------------------------------------------------------------------

