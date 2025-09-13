📘 SQL Operators & Functions

SQL provides operators and functions to perform calculations, filter data, and manipulate values.
```
🔹 1. Operators in SQL
    ✅ Arithmetic Operators
          + (Addition)
          - (Subtraction)
          * (Multiplication)
          / (Division)
          % (Modulo)

Example (E-commerce order totals):

syntax: SELECT order_id, quantity, price, quantity * price AS total_amount FROM order_items;

👉 Calculates the total amount for each order.

✅ Comparison Operators
          = (Equal)
          != or <> (Not Equal)
          > (Greater Than)
          < (Less Than)
          >= (Greater or Equal)
          <= (Less or Equal)

Example (Filter expensive products):

syntax: SELECT name, price FROM products WHERE price > 50000;
------------------------------------------------------------------------------------------------------------
✅ Logical Operators

AND → Both conditions must be true
-> used to fetch rows that satisfy 2 or more condition.

OR → used to fetch rows that satisfy At least one condition true

NOT → used to Negates condition in the WHERE clause

syntax: -> select * from student where age = 12 and fees = 5000;
        -> select * from student where age =15 or fees = 10000;
        -> select * from student where not name like '%sh%';

## Multiple logical operator: 
  -> these compound condition enables us to finetune the data retrivel requirements.
  -> it works in high to low like NOT -> AND -> OR.
syntax: select * from student where age = 12 and fees = 5000 or age =15;
---------------------------------------------------------------------------------------------------------

✅ String Operators

# BETWEEN → Check if a value lies in a range
 -- check Orders placed between Jan 1 and Jan 31
query: SELECT * FROM orders WHERE order_date BETWEEN '2025-01-01' AND '2025-01-31';

# IN → Match against multiple values
-- Customers from specific cities
query: SELECT * FROM customers WHERE city IN ('Mysore', 'Bangalore', 'Chennai');

# LIKE → Pattern matching (like operator is used in 'WHERE' clause to retrive all data) 
percentage sign (%) -> represents zero or more charecters.
underscore (_) -> represent a single charecter.
examples:
* exact match : select * from student where name like 'chandu';
-> retrives whose name is exactly equals to 'chandu'

* start with : select * from student where name like 'ch%';
-> retives whose name starts with 'ch'

* ends with : select * from student where name like '%a';
-> retrives whose name ends with 'a'

* containing : select * from student where name like '%sh%';
-> retrive whose name contains with 'sh'

* pattern matching : select * from student where where address like 'm_%';
-> retives whose address starts with 'm' and have atleast 2 charecter in length.

# IS NULL → Check for null values 
---------------------------------------------------------------------------------------------------
```
## 🔹 2. Functions in SQL
## Functions are built-in methods to transform data.
```
✅ Single Row (Scalar) Functions
-> Work on individual values and return one result per row.
-> Single-row functions are typically immutable, meaning that they do not modify the original data but rather return the modified value as part of the result set
-> Single-row functions encompass a wide variety of operations, including string manipulation, numeric calculations, date and time formatting, conversion, and more.

some examples of single-row functions:
## string function:
* UPPER() & LOWER(): Convert strings to uppercase or lowercase.
* LENGTH(): Calculate the length of a string.
* CONCAT(): Concatenate two or more strings together.

syntax: -> SELECT CONCAT(UPPER(first_name), ' ', LOWER(last_name)) AS formatted_name FROM customers;
      -> SELECT UPPER(first_name) AS upper_first_name FROM employees;
      -> SELECT first_name, LENGTH(first_name) AS name_length FROM employees;
-------------------------------------------------------------------------------------------------------------------
## Number Functions:
* ROUND(): Perform rounding operations on numbers.
-> SELECT price, ROUND(price * 0.18, 2) AS gst FROM products;

* ABS(): Absolute Value- Returns the positive value of a number.
-> SELECT ABS(-25) AS result;   -- 25
-> SELECT customer_id, amount, ABS(amount) AS transaction_amount FROM transactions;

* MOD(): Modulus (Remainder)- Remainder of Division.
-> SELECT MOD(10, 3);   -- 1
-> SELECT order_id, CASE WHEN MOD(order_id,2)=0 THEN 'Even Order' ELSE 'Odd Order' END AS type FROM orders;

* CEIL(): Ceiling (Round Up)- Rounds a number up to the nearest integer.
-> SELECT CEIL(7.9);    -- 8
-> SELECT salary, CEIL(salary / 1000) * 1000 AS rounded_salary FROM employees

* FLOOR(): Floor (Round Down) - Rounds a number down to the nearest integer.
-> SELECT FLOOR(7.1);    -- 7
-> SELECT FLOOR(99.99) AS final_price;  -- 99
--------------------------------------------------------------------------------------------------------------------
## Date Functions:
* NOW(): Current Date & Time
-> SELECT NOW();      -- 2025-09-13 12:55:22
-> INSERT INTO orders (customer_id, order_date) VALUES (101, NOW());

* CURDATE(): Current Date and Time
-> SELECT emp_id, hire_date, CURDATE() as current_datetime,current_timestamp() as current_datetimestamp FROM employees;

* DATE_ADD(): Add/Subtract Time Intervals.
-> SELECT DATE_ADD('2025-09-13', INTERVAL 7 DAY);   -- 2025-09-20
-> SELECT DATE_ADD('2025-09-13', INTERVAL -1 MONTH); -- 2025-08-13
-> SELECT order_id, order_date, DATE_ADD(order_date, INTERVAL 5 DAY) AS expected_delivery FROM orders;

* DATEDIFF(): Difference Between Dates (in days)
-> SELECT DATEDIFF('2025-09-20', '2025-09-13');  -- 7
-> SELECT order_id, DATEDIFF(NOW(), order_date) AS days_passed FROM orders;
-> SELECT customer_id, DATEDIFF(subscription_end, NOW()) AS days_left FROM subscriptions;
👉 If days_left <= 5, send renewal reminder.

* EXTRACT() - Extract Part of a Date
-> SELECT emp_id, EXTRACT(YEAR FROM hire_date) AS hire_year FROM employees;

* COALESCE, NVL() - Replace NULL with a Value
-> SELECT first_name, NVL(last_name, 'Unknown') AS last_name FROM employees;
SELECT first_name, COALESCE(last_name, 'Unknown') AS last_name FROM employees;
-----------------------------------------------------------------------------------------------
* SUBSTRING(): Extract Substring
-> SELECT SUBSTRING(first_name, 1, 3) AS initials FROM employees;

* TRIM() - Remove Leading and Trailing Spaces
* LTRIM() and RTRIM() - Remove Leading and Trailing Spaces
syntax:
-> SELECT TRIM(LEADING '0' FROM emp_id) AS trimmed_id FROM employees;
-> SELECT emp_id, LTRIM(first_name) AS ltrimmed_name, RTRIM(last_name) AS rtrimmed_name FROM employees;

* INITCAP() - Convert to Initial Caps:
-> SELECT INITCAP(first_name) AS capitalized_name FROM employees;

* REPLACE() - Replace Substring in a String
-> SELECT emp_id, REPLACE(first_name, 'o', 'O') AS modified_name FROM employees;
----------------------------------------------------------------------------------------------------------
```
✅ Summary Table
```---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
|   Function                   | Description                                                               | Example                                            | Output                |
| ---------------------------- | --------------------------------------------------------------------------| -------------------------------------------------- | --------------------- |
| **ABS(x)**                   | Returns absolute (positive) value                                         | `SELECT ABS(-10);`                                 | 10                    |
| **MOD(x,y)**                 | Returns remainder of division                                             | `SELECT MOD(25,7);`                                | 4                     |
| **CEIL(x)**                  | Rounds number **up**                                                      | `SELECT CEIL(7.1);`                                | 8                     |
| **FLOOR(x)**                 | Rounds number **down**                                                    | `SELECT FLOOR(7.9);`                               | 7                     |
| **ROUND(x, d)**              | Rounds number to *d* decimals                                             | `SELECT ROUND(12.345,2);`                          | 12.35                 |
| **NOW()**                    | Returns current date & time                                               | `SELECT NOW();`                                    | `2025-09-13 13:15:45` |
| **DATE\_ADD(d, INTERVAL x)** | Adds/subtracts interval                                                   | `SELECT DATE_ADD('2025-09-13', INTERVAL 7 DAY);`   | `2025-09-20`          |
| **DATEDIFF(d1, d2)**         | Difference (days) between two dates                                       | `SELECT DATEDIFF('2025-09-20','2025-09-13');`      | 7                     |
| **EXTRACT(part FROM d)**     | Extracts part of a date                                                   | `SELECT EXTRACT(YEAR FROM '2025-09-13');`          | 2025                  |
| **REPLACE(str, from, to)**   | Replace substring                                                         | `SELECT REPLACE('SQL is easy','easy','powerful');` | SQL is powerful       |
| **INITCAP()**\*              | Capitalizes first letter of each word 
                                (not native in MySQL, use `CONCAT(UCASE(SUBSTRING(...)))`)                 | `INITCAP('mysql functions')`                       | MySQL Functions       |
| **TRIM(str)**                | Removes leading/trailing spaces                                           | `SELECT TRIM('   hello   ');`                      | `hello`               |
| **SUBSTRING(str, pos, len)** | Extracts substring                                                        | `SELECT SUBSTRING('Database',1,4);`                | `Data`                |
| **CONCAT(str1, str2, …)**    | Joins strings                                                             | `SELECT CONCAT('Data',' ','Base');`                | `Data Base`           |
| **LENGTH(str)**              | Returns length of string                                                  | `SELECT LENGTH('MySQL');`                          | 5                     |
| **UPPER(str)**               | Converts to uppercase                                                     | `SELECT UPPER('sql');`                             | SQL                   |
| **LOWER(str)**               | Converts to lowercase                                                     | `SELECT LOWER('SQL');`                             | sql                   |
| **COALESCE(v1, v2, …)**      | Returns first non-NULL value                                              | `SELECT COALESCE(NULL,NULL,'Hello');`              | Hello                 |
| **NVL(v1, v2)**\*            | Replaces NULL with given value (Oracle, use `IFNULL()` in MySQL)          | `SELECT IFNULL(NULL,'NA');`                        | NA                    |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```
## order by and distinct
```
* order by: it is used to sort result of query, by default it sorts in ascending order(asc).
            -> also specify discending order (desc).
syntax: sort student by age ?
-> select stduent_id, name, age from student order by age;
        sort student age in descending order ?
-> select student_id, name, age from student order by age desc;
        sort by multiple columns ?
-> select student_id, name, age from student order by age desc, fees asc;

* Distinct: it is used to remove duplicate values from the result set. 
          -> it only returns unique rows.
syntax: get unique student name ?
-> select distinct name from student;
        
combine with order by
-> select distinct name from student order by name desc;
---------------------------------------------------------------------------------------------
Pagination: it means fetching a limited number of rows at a time from large result set.
          -> it is often used to display page by page in application or from where to where.
## limit and offset

* limit: Limits the number of rows returned.
example: get first 5 rows 
-> select * from student limit 5;
-> select student_id, name, age from student limit 5;
-> select * from student where age = 16 order by fees limit 5;

* offset: OFFSET skips some rows before returning results.
syntax: SELECT columns FROM table LIMIT n OFFSET m;
        n = number of rows to return
        m = number of rows to skip
example: Skips the first 2 rows and then returns 3 rows starting from row 3.
-> SELECT * FROM students LIMIT 3 OFFSET 2;

* Alternative Syntax: Instead of LIMIT n OFFSET m, you can also write,
syntax: SELECT * FROM students LIMIT m, n;
query: SELECT * FROM students LIMIT 2, 3;

## wrong syntax: select * from student offset 2 limit 5;
## get error 
---------------------------------------------------------------------------------------------------------------
```
✅ ## Group (Aggregate) Functions
```
-> Work on groups of rows and return one result per group.
-> These functions are typically used with the GROUP BY clause
-> to group rows that share a common value in one or more columns. 
-> Group functions are commonly used for tasks such as calculating summaries or aggregations over groups of data.

* COUNT() → Counts the number of rows in a result set.
Example: Count the total number of employees.
-> SELECT COUNT(*) AS total_employees FROM employees;

* SUM() → Total - Calculates the sum of numeric values in a column.
Example: Calculate the total salary for all employees.
SELECT SUM(salary) AS total_salary FROM employees;

* AVG() → Average - Calculates the average value of numeric data in a column.
Example: Calculate the average salary of all employees.
SELECT AVG(salary) AS avg_salary FROM employees;

* MIN() → Smallest - Finds the minimum value in a column.
Example: Find the minimum salary among all employees.
SELECT MIN(salary) AS min_salary FROM employees;

* MAX() → Largest - Finds the maximum value in a column.
Example: Find the maximum salary among all employees.
SELECT MAX(salary) AS max_salary FROM employees;

* GROUP_CONCAT(): Concatenates multiple values from rows into a single string.
Example: Concatenate the first names of employees in a single string.
SELECT GROUP_CONCAT(first_name) AS all_first_names FROM employees;

* STDDEV(): Calculates the standard deviation of values in a column.
Example: Calculate the standard deviation of salaries for all employees.
SELECT STDDEV(salary) AS salary_stddev FROM employees;

* VARIANCE(): Calculates the variance of values in a column.
Example: Calculate the variance of salaries for all employees.
SELECT VARIANCE(salary) AS salary_variance FROM employees;
-----------------------------------------------------------------------------------------------------------

## HAVING Clause:
-> The HAVING clause is used with the GROUP BY  clause to filter the grouped results. 
-> It specifies conditions that must be met by the groups themselves, not individual rows. 
Syntax:
SELECT column1, aggregate_function(column) FROM table GROUP BY column1 HAVING condition; 
Example:
SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department
HAVING AVG(salary) > 55000;

Conditions used in the HAVING clause can involve group-level aggregate functions (like AVG, SUM, COUNT), as well as regular column values. 
The HAVING clause is applied after the GROUP BY clause and aggregate calculations have been performed.
* COUNT() with HAVING:
Example: Find departments with more than one employee.
-> SELECT department, COUNT(*) AS num_employees FROM employees GROUP BY department HAVING COUNT(*) > 1;

* SUM() with HAVING:
Example: Find departments with a total salary greater than 120000. 
-> SELECT department, SUM(salary) AS total_salary FROM employees GROUP BY department HAVING SUM(salary) > 120000;

* AVG() with HAVING:
Example: Find departments with an average salary greater than 55000.
-> SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department HAVING AVG(salary) > 55000;

* MIN() with HAVING:
Example: Find departments with a minimum salary greater than 50000. 
-> SELECT department, MIN(salary) AS min_salary FROM employees GROUP BY department HAVING MIN(salary) > 50000;

* MAX() with HAVING:
Example: Find departments with a maximum salary less than 61000.
-> SELECT department, MAX(salary) AS max_salary FROM employees GROUP BY department HAVING MAX(salary) < 61000;

* GROUP_CONCAT() with HAVING:
Example: Find departments with more than one employee and concatenate their first names.
-> SELECT department, GROUP_CONCAT(first_name) AS employee_names FROM employees GROUP BY department HAVING COUNT(*) > 1;
----------------------------------------------------------------------------------------------------------------------------------
```
## 📝 Summary
#### Operators → Perform calculations & conditions (+, -, =, AND, LIKE...).
#### Functions → Manipulate data (string, numeric, date, aggregation).
##### Both are essential for reporting, analytics, and filtering.
