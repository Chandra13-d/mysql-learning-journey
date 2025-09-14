# ** 📘 SQL Joins ** 

## 🔹 What are Joins?
  👉 In SQL, Joins are used to combine rows from two or more tables based on a related column between them (usually a foreign key).

# 🔹 Types of Joins

## 1. CROSS JOIN (Cartesian Product)
```sql 👉 A join two tables normally in a Cartesian product of the data from two tables.
   👉 A Cartesian product joins every row from the first table with every row from the second table, combining all rows.
syntax: 
  SELECT * FROM table1 CROSS JOIN table2;
  or 
  SELECT * FROM table1, table2;

## realworld example:
-> create table student (student_id int primary key, name varchar(50), class int);
-> insert into student values (1, anitha, 10);
-> create table teacher (teacher_id int primary key, name, vachar(50), student_id int, foreign key (student_id) references student (student_id);
-> insert into teacher values (101, meena, 1);

query: SELECT s.student_id, s.name AS student_name, t.teacher_id, t.name AS teacher_name
FROM Student s CROSS JOIN Teacher t;

## ✅ Output (Cartesian Product)
| student_id  | student_name  | teacher_id  | teacher_name  |
| ----------- | ------------- | ----------- | ------------- |
| 1           | Anitha        | 101         | Meena         |
| 1           | Anitha        | 102         | Suresh        |
| 2           | Ravi          | 101         | Meena         |
| 2           | Ravi          | 102         | Suresh        |

📌 Explanation:
2 students × 2 teachers = 4 rows.
Every student is paired with every teacher.
Useful in timetable generation, seating arrangements, or testing all combinations. 
-------------------------------------------------------------------------------------------------------------------------------------------
```
## 2. INNER JOIN
  👉 Returns only the rows that have matching values in both tables.
```sql syntax:  
SELECT a.column, b.column FROM tableA a
INNER JOIN tableB b
ON a.common_column = b.common_column;

Example:
    👉 Returns only matching records between Student and Teacher.
query:
SELECT s.student_id, s.name AS student_name, t.name AS teacher_name FROM Student s
INNER JOIN Teacher t ON s.student_id = t.student_id;

## ✅ Output:
| student_id  | student_name  | teacher_name  |
| ----------- | ------------- | ------------- |
| 1           | Anitha        | Meena         |
| 2           | Ravi          | Suresh        |

📌 Only students with teachers assigned are shown.
----------------------------------------------------------------------------------------
```
## 3. LEFT JOIN (LEFT OUTER JOIN)
  👉 Returns all rows from the left table, plus the matched rows from the right table. If no match → NULL.
```sql
Syntax:
SELECT a.column, b.column FROM tableA a LEFT JOIN tableB b
ON a.common_column = b.common_column;

Example:
      👉 Returns all students, with teacher info if available.
query: SELECT s.student_id, s.name AS student_name, t.name AS teacher_name FROM Student s
LEFT JOIN Teacher t ON s.student_id = t.student_id;

## ✅ Output:
| student_id  | student_name  | teacher_name  |
| ----------- | ------------- | ------------- |
| 1           | Anitha        | Meena         |
| 2           | Ravi          | Suresh        |
| 3           | Sneha         | NULL          |
| 4           | Kiran         | NULL          |

📌 Shows all students, even if no teacher assigned.
--------------------------------------------------------------------------------------------
```
## 4. RIGHT JOIN (RIGHT OUTER JOIN)
  👉 Opposite of LEFT JOIN. Returns all rows from the right table, plus matched rows from the left.

Example:
      👉 Returns all teachers, with student info if available.
```sql query:
SELECT s.student_id, s.name AS student_name, t.name AS teacher_name FROM Student s
RIGHT JOIN Teacher t ON s.student_id = t.student_id;

## ✅ Output:
| student_id  | student_name  | teacher_name  |
| ----------- | ------------- | ------------- |
| 1           | Anitha        | Meena         |
| 2           | Ravi          | Suresh        |
| NULL        | NULL          | Arjun         |

📌 Teacher Arjun is included, even though no student matches.
-------------------------------------------------------------------------------------------------------
```
## 5. FULL OUTER JOIN
  👉 Combines results of LEFT and RIGHT JOIN. Returns all rows when there is a match in either left or right table.
```sql  👉 MySQL doesn’t directly support FULL OUTER JOIN → You can simulate it using UNION.

Example (using UNION):
    (SELECT s.student_id, s.name AS student_name, t.name AS teacher_name FROM Student s
    LEFT JOIN Teacher t ON s.student_id = t.student_id)
    UNION
    (SELECT s.student_id, s.name AS student_name, t.name AS teacher_name FROM Student s
    RIGHT JOIN Teacher t ON s.student_id = t.student_id;)
    
## ✅ Output:
| student_id  | student_name  | teacher_name  |
| ----------- | ------------- | ------------- |
| 1           | Anitha        | Meena         |
| 2           | Ravi          | Suresh        |
| 3           | Sneha         | NULL          |
| 4           | Kiran         | NULL          |
| NULL        | NULL          | Arjun         |
----------------------------------------------------------------------------------------------------------------------
```
## 📝 Real-World Scenarios:
```
CROSS JOIN → Timetable creation (every student with every subject/teacher).
INNER JOIN → Students with assigned teachers.
LEFT JOIN → All students, even if no teacher assigned.
RIGHT JOIN → All teachers, even if not assigned to any student.
FULL JOIN → Combine all students + teachers, matched or not.


-------------------------------------------------THANK YOU-------------------------------------------------
