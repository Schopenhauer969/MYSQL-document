# 🐬 MySQL — Beginner to Advanced

> A complete MySQL learning guide from **Beginner → Intermediate → Advanced** with practical SQL examples and explanations in **English 🇬🇧 + Khmer 🇰🇭**.

---

## 📚 Table of Contents

* [1. What is MySQL?](#1-what-is-mysql)
* [2. Installing MySQL](#2-installing-mysql)
* [3. Connecting to MySQL](#3-connecting-to-mysql)
* [4. MySQL Basics](#4-mysql-basics)
* [5. Databases](#5-databases)
* [6. Tables](#6-tables)
* [7. Data Types](#7-data-types)
* [8. INSERT](#8-insert)
* [9. SELECT](#9-select)
* [10. WHERE](#10-where)
* [11. UPDATE](#11-update)
* [12. DELETE](#12-delete)
* [13. ORDER BY](#13-order-by)
* [14. LIMIT](#14-limit)
* [15. DISTINCT](#15-distinct)
* [16. Operators](#16-operators)
* [17. LIKE](#17-like)
* [18. NULL](#18-null)
* [19. Aggregate Functions](#19-aggregate-functions)
* [20. GROUP BY](#20-group-by)
* [21. HAVING](#21-having)
* [22. Constraints](#22-constraints)
* [23. Primary Key](#23-primary-key)
* [24. Foreign Key](#24-foreign-key)
* [25. UNIQUE](#25-unique)
* [26. JOIN](#26-join)
* [27. INNER JOIN](#27-inner-join)
* [28. LEFT JOIN](#28-left-join)
* [29. RIGHT JOIN](#29-right-join)
* [30. CROSS JOIN](#30-cross-join)
* [31. Self Join](#31-self-join)
* [32. Subqueries](#32-subqueries)
* [33. EXISTS](#33-exists)
* [34. CASE](#34-case)
* [35. String Functions](#35-string-functions)
* [36. Date and Time](#36-date-and-time)
* [37. Mathematical Functions](#37-mathematical-functions)
* [38. Views](#38-views)
* [39. Indexes](#39-indexes)
* [40. Transactions](#40-transactions)
* [41. ACID](#41-acid)
* [42. Stored Procedures](#42-stored-procedures)
* [43. Functions](#43-functions)
* [44. Triggers](#44-triggers)
* [45. CTE](#45-cte)
* [46. Recursive CTE](#46-recursive-cte)
* [47. Window Functions](#47-window-functions)
* [48. Common Table Expressions + Window Functions](#48-common-table-expressions--window-functions)
* [49. UNION](#49-union)
* [50. JSON](#50-json)
* [51. User Management](#51-user-management)
* [52. Roles and Privileges](#52-roles-and-privileges)
* [53. Backup and Restore](#53-backup-and-restore)
* [54. EXPLAIN](#54-explain)
* [55. Query Optimization](#55-query-optimization)
* [56. Normalization](#56-normalization)
* [57. Database Relationships](#57-database-relationships)
* [58. Transactions and Locking](#58-transactions-and-locking)
* [59. MySQL Project](#59-mysql-project)
* [60. Best Practices](#60-best-practices)
* [61. Cheat Sheet](#61-cheat-sheet)

---

# 1. What is MySQL?

## English

**MySQL** is an open-source relational database management system (RDBMS).

It stores data inside:

```text
Database
   ↓
Tables
   ↓
Rows
   ↓
Columns
```

MySQL uses **SQL (Structured Query Language)** to create, read, update, and delete data.

## Khmer

**MySQL** គឺជា Database Management System ប្រភេទ Relational Database។

វារក្សាទុកទិន្នន័យជា៖

```text
Database
   ↓
Table
   ↓
Row
   ↓
Column
```

យើងប្រើ **SQL** ដើម្បីធ្វើការជាមួយ Database ដូចជា៖

* បង្កើត Database
* បង្កើត Table
* បញ្ចូល Data
* អាន Data
* កែប្រែ Data
* លុប Data

---

# 2. Installing MySQL

You can install MySQL Server and MySQL client tools.

Common tools:

* MySQL Server
* MySQL Workbench
* MySQL Shell
* MySQL command-line client

After installation, verify:

```sql
SELECT VERSION();
```

Example result:

```text
8.x.x
```

---

# 3. Connecting to MySQL

From the command line:

```bash
mysql -u root -p
```

Then enter your password.

## Khmer

Command នេះមានន័យថា៖

```text
mysql → បើក MySQL client
-u     → username
root   → username
-p     → password
```

---

# 4. MySQL Basics

## SQL statement

```sql
SELECT 1;
```

Result:

```text
1
```

SQL statements normally end with:

```text
;
```

Example:

```sql
SELECT 'Hello MySQL';
```

---

# 5. Databases

## Create Database

```sql
CREATE DATABASE school;
```

## Create only if it does not exist

```sql
CREATE DATABASE IF NOT EXISTS school;
```

## Show Databases

```sql
SHOW DATABASES;
```

## Select Database

```sql
USE school;
```

## Delete Database

```sql
DROP DATABASE school;
```

⚠️ `DROP DATABASE` permanently removes the database and its tables.

## Khmer

Database គឺជាកន្លែងធំសម្រាប់ផ្ទុក Tables។

```text
school
 ├── students
 ├── teachers
 └── courses
```

---

# 6. Tables

Create a table:

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    email VARCHAR(255)
);
```

Show tables:

```sql
SHOW TABLES;
```

Describe table:

```sql
DESCRIBE students;
```

Alternative:

```sql
DESC students;
```

Delete table:

```sql
DROP TABLE students;
```

---

# 7. Data Types

## Numeric Types

```sql
INT
BIGINT
DECIMAL(10,2)
FLOAT
DOUBLE
```

Example:

```sql
CREATE TABLE products (
    id INT,
    price DECIMAL(10,2),
    quantity INT
);
```

---

## String Types

```sql
CHAR(10)
VARCHAR(255)
TEXT
MEDIUMTEXT
LONGTEXT
```

Example:

```sql
CREATE TABLE users (
    username VARCHAR(100),
    description TEXT
);
```

---

## Date and Time

```sql
DATE
TIME
DATETIME
TIMESTAMP
YEAR
```

Example:

```sql
CREATE TABLE events (
    event_date DATE,
    event_time TIME,
    created_at DATETIME
);
```

---

## Boolean

MySQL supports:

```sql
BOOLEAN
```

which is effectively an alias for:

```sql
TINYINT(1)
```

Example:

```sql
CREATE TABLE users (
    id INT,
    is_active BOOLEAN
);
```

---

# 8. INSERT

Insert one row:

```sql
INSERT INTO students (id, name, age, email)
VALUES (1, 'Dara', 20, 'dara@example.com');
```

Insert multiple rows:

```sql
INSERT INTO students (id, name, age, email)
VALUES
    (2, 'Sokha', 21, 'sokha@example.com'),
    (3, 'Vanna', 19, 'vanna@example.com'),
    (4, 'Rina', 22, 'rina@example.com');
```

## Khmer

`INSERT` ប្រើសម្រាប់បញ្ចូល Data ថ្មីទៅក្នុង Table។

---

# 9. SELECT

Select everything:

```sql
SELECT *
FROM students;
```

Select specific columns:

```sql
SELECT id, name, age
FROM students;
```

Select one row:

```sql
SELECT *
FROM students
WHERE id = 1;
```

---

# 10. WHERE

`WHERE` filters records.

```sql
SELECT *
FROM students
WHERE age = 20;
```

Greater than:

```sql
SELECT *
FROM students
WHERE age > 20;
```

Less than:

```sql
SELECT *
FROM students
WHERE age < 20;
```

Multiple conditions:

```sql
SELECT *
FROM students
WHERE age >= 20
  AND age <= 25;
```

---

# 11. UPDATE

Update one row:

```sql
UPDATE students
SET age = 21
WHERE id = 1;
```

Update multiple columns:

```sql
UPDATE students
SET
    name = 'Dara Chan',
    age = 22
WHERE id = 1;
```

⚠️ Always be careful with `UPDATE`.

Dangerous:

```sql
UPDATE students
SET age = 30;
```

This updates **every row**.

---

# 12. DELETE

Delete one row:

```sql
DELETE FROM students
WHERE id = 1;
```

Delete all rows:

```sql
DELETE FROM students;
```

⚠️ Always use `WHERE` when you only want to remove specific records.

---

# 13. ORDER BY

Ascending:

```sql
SELECT *
FROM students
ORDER BY age ASC;
```

Descending:

```sql
SELECT *
FROM students
ORDER BY age DESC;
```

Multiple columns:

```sql
SELECT *
FROM students
ORDER BY age DESC, name ASC;
```

---

# 14. LIMIT

Get first 5 rows:

```sql
SELECT *
FROM students
LIMIT 5;
```

Pagination:

```sql
SELECT *
FROM students
LIMIT 10 OFFSET 20;
```

This means:

```text
Skip 20 rows
Then return 10 rows
```

---

# 15. DISTINCT

Remove duplicate values:

```sql
SELECT DISTINCT age
FROM students;
```

Multiple columns:

```sql
SELECT DISTINCT age, name
FROM students;
```

---

# 16. Operators

## Comparison

```sql
=
<>
!=
>
<
>=
<=
```

Example:

```sql
SELECT *
FROM students
WHERE age >= 20;
```

---

## AND

```sql
SELECT *
FROM students
WHERE age >= 18
  AND age <= 25;
```

---

## OR

```sql
SELECT *
FROM students
WHERE age = 18
   OR age = 20;
```

---

## NOT

```sql
SELECT *
FROM students
WHERE NOT age = 20;
```

---

## BETWEEN

```sql
SELECT *
FROM students
WHERE age BETWEEN 18 AND 25;
```

---

## IN

```sql
SELECT *
FROM students
WHERE age IN (18, 20, 25);
```

---

# 17. LIKE

Starts with `D`:

```sql
SELECT *
FROM students
WHERE name LIKE 'D%';
```

Ends with `a`:

```sql
SELECT *
FROM students
WHERE name LIKE '%a';
```

Contains `ar`:

```sql
SELECT *
FROM students
WHERE name LIKE '%ar%';
```

One character:

```sql
SELECT *
FROM students
WHERE name LIKE '_ara';
```

## Khmer

`%` មានន័យថា characters ច្រើន ឬ 0 characters។

`_` មានន័យថា character មួយ។

---

# 18. NULL

Find NULL:

```sql
SELECT *
FROM students
WHERE email IS NULL;
```

Find non-NULL:

```sql
SELECT *
FROM students
WHERE email IS NOT NULL;
```

Do NOT use:

```sql
WHERE email = NULL
```

Correct:

```sql
WHERE email IS NULL
```

---

# 19. Aggregate Functions

## COUNT

```sql
SELECT COUNT(*) AS total_students
FROM students;
```

## SUM

```sql
SELECT SUM(age) AS total_age
FROM students;
```

## AVG

```sql
SELECT AVG(age) AS average_age
FROM students;
```

## MIN

```sql
SELECT MIN(age) AS youngest
FROM students;
```

## MAX

```sql
SELECT MAX(age) AS oldest
FROM students;
```

---

# 20. GROUP BY

Example:

```sql
SELECT age, COUNT(*) AS total
FROM students
GROUP BY age;
```

With products:

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    category VARCHAR(100),
    price DECIMAL(10,2)
);
```

Query:

```sql
SELECT
    category,
    COUNT(*) AS total_products
FROM products
GROUP BY category;
```

## Khmer

`GROUP BY` ប្រើសម្រាប់បែងចែក Data ជាក្រុម។

ឧទាហរណ៍៖

```text
Phones → 10
Laptops → 5
Tablets → 8
```

---

# 21. HAVING

`HAVING` filters groups.

```sql
SELECT
    category,
    COUNT(*) AS total_products
FROM products
GROUP BY category
HAVING COUNT(*) > 5;
```

Important:

```text
WHERE  → filter rows
HAVING → filter groups
```

---

# 22. Constraints

Common constraints:

```text
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
DEFAULT
CHECK
```

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'active'
);
```

---

# 23. Primary Key

A primary key uniquely identifies each row.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Composite primary key:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

## Khmer

Primary Key គឺជា ID ដែលមិនអាចមានតម្លៃដូចគ្នា ហើយមិនអាច `NULL`។

---

# 24. Foreign Key

Create parent table:

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

Create child table:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(id)
);
```

Insert:

```sql
INSERT INTO departments (id, name)
VALUES
    (1, 'IT'),
    (2, 'HR');
```

```sql
INSERT INTO employees (id, name, department_id)
VALUES
    (1, 'Dara', 1),
    (2, 'Sokha', 2);
```

---

# 25. UNIQUE

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

This prevents duplicate email values.

---

# 26. JOIN

Suppose:

```text
departments
----------------
id | name

1  | IT
2  | HR
```

and:

```text
employees
-----------------------
id | name  | department_id

1  | Dara  | 1
2  | Sokha | 2
```

A JOIN combines related data.

---

# 27. INNER JOIN

```sql
SELECT
    e.id,
    e.name,
    d.name AS department
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.id;
```

Result:

```text
id | name  | department
1  | Dara  | IT
2  | Sokha | HR
```

## Khmer

`INNER JOIN` បង្ហាញតែ Records ដែលមានទំនាក់ទំនងគ្នា។

---

# 28. LEFT JOIN

```sql
SELECT
    e.id,
    e.name,
    d.name AS department
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.id;
```

`LEFT JOIN` keeps every row from the left table.

---

# 29. RIGHT JOIN

```sql
SELECT
    e.id,
    e.name,
    d.name AS department
FROM employees e
RIGHT JOIN departments d
    ON e.department_id = d.id;
```

`RIGHT JOIN` keeps every row from the right table.

---

# 30. CROSS JOIN

```sql
SELECT
    e.name AS employee,
    d.name AS department
FROM employees e
CROSS JOIN departments d;
```

This creates every possible combination.

If there are:

```text
3 employees
2 departments
```

Result:

```text
3 × 2 = 6 rows
```

---

# 31. Self Join

A table can join itself.

Example employee manager relationship:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT,
    FOREIGN KEY (manager_id)
        REFERENCES employees(id)
);
```

Query:

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.id;
```

---

# 32. Subqueries

A subquery is a query inside another query.

Example:

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

This finds products whose price is above the average.

---

# 33. EXISTS

```sql
SELECT d.*
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.id
);
```

This finds departments that have employees.

---

# 34. CASE

```sql
SELECT
    name,
    age,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age < 60 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM students;
```

Another example:

```sql
SELECT
    name,
    price,
    CASE
        WHEN price >= 1000 THEN 'Expensive'
        WHEN price >= 500 THEN 'Medium'
        ELSE 'Cheap'
    END AS price_category
FROM products;
```

---

# 35. String Functions

## CONCAT

```sql
SELECT CONCAT('Hello ', 'MySQL') AS message;
```

## CONCAT columns

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM users;
```

## UPPER

```sql
SELECT UPPER(name)
FROM students;
```

## LOWER

```sql
SELECT LOWER(name)
FROM students;
```

## LENGTH

```sql
SELECT LENGTH(name)
FROM students;
```

## TRIM

```sql
SELECT TRIM('   MySQL   ');
```

## SUBSTRING

```sql
SELECT SUBSTRING('Hello MySQL', 1, 5);
```

---

# 36. Date and Time

Current date:

```sql
SELECT CURDATE();
```

Current time:

```sql
SELECT CURTIME();
```

Current date and time:

```sql
SELECT NOW();
```

Extract year:

```sql
SELECT YEAR(NOW());
```

Extract month:

```sql
SELECT MONTH(NOW());
```

Extract day:

```sql
SELECT DAY(NOW());
```

Date addition:

```sql
SELECT DATE_ADD(
    '2026-01-01',
    INTERVAL 7 DAY
);
```

Date subtraction:

```sql
SELECT DATE_SUB(
    '2026-01-01',
    INTERVAL 7 DAY
);
```

Date difference:

```sql
SELECT DATEDIFF(
    '2026-12-31',
    '2026-01-01'
);
```

---

# 37. Mathematical Functions

```sql
SELECT ABS(-10);
```

```sql
SELECT ROUND(123.456, 2);
```

```sql
SELECT CEIL(10.2);
```

```sql
SELECT FLOOR(10.9);
```

```sql
SELECT POWER(2, 3);
```

```sql
SELECT SQRT(25);
```

---

# 38. Views

A view is a stored query that behaves like a virtual table.

Create:

```sql
CREATE VIEW employee_details AS
SELECT
    e.id,
    e.name,
    d.name AS department
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.id;
```

Use:

```sql
SELECT *
FROM employee_details;
```

Delete:

```sql
DROP VIEW employee_details;
```

---

# 39. Indexes

Indexes improve lookup performance.

Create:

```sql
CREATE INDEX idx_students_name
ON students(name);
```

Multiple-column index:

```sql
CREATE INDEX idx_students_name_age
ON students(name, age);
```

Unique index:

```sql
CREATE UNIQUE INDEX idx_users_email
ON users(email);
```

Show indexes:

```sql
SHOW INDEX FROM students;
```

Delete index:

```sql
DROP INDEX idx_students_name
ON students;
```

## Khmer

Index ជួយឱ្យ Database ស្វែងរក Data បានលឿន។

ប៉ុន្តែ Index ច្រើនពេកអាចធ្វើឱ្យ:

```text
INSERT
UPDATE
DELETE
```

យឺតជាងមុន ព្រោះ Index ត្រូវ update ផងដែរ។

---

# 40. Transactions

A transaction groups multiple SQL statements into one logical operation.

Start:

```sql
START TRANSACTION;
```

Example:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;
```

If something goes wrong:

```sql
ROLLBACK;
```

---

# 41. ACID

Transactions follow the ACID principles.

## A — Atomicity

All operations succeed or all are rolled back.

## C — Consistency

Data remains valid according to database rules.

## I — Isolation

Concurrent transactions are isolated according to the configured isolation level.

## D — Durability

Committed changes survive normal server failures.

## Khmer

ACID គឺជាគោលការណ៍សំខាន់សម្រាប់ Database Transaction។

```text
A = Atomicity
C = Consistency
I = Isolation
D = Durability
```

---

# 42. Stored Procedures

Create:

```sql
DELIMITER //

CREATE PROCEDURE GetStudents()
BEGIN
    SELECT *
    FROM students;
END //

DELIMITER ;
```

Call:

```sql
CALL GetStudents();
```

Procedure with parameter:

```sql
DELIMITER //

CREATE PROCEDURE GetStudentById(
    IN student_id INT
)
BEGIN
    SELECT *
    FROM students
    WHERE id = student_id;
END //

DELIMITER ;
```

Call:

```sql
CALL GetStudentById(1);
```

Drop:

```sql
DROP PROCEDURE GetStudents;
```

---

# 43. Functions

Create a stored function:

```sql
DELIMITER //

CREATE FUNCTION AddNumbers(
    a INT,
    b INT
)
RETURNS INT
DETERMINISTIC
RETURN a + b //

DELIMITER ;
```

Use:

```sql
SELECT AddNumbers(10, 20);
```

Result:

```text
30
```

Drop:

```sql
DROP FUNCTION AddNumbers;
```

---

# 44. Triggers

A trigger automatically executes when a specified database event occurs.

Example:

```sql
CREATE TABLE user_logs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    action VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Trigger:

```sql
DELIMITER //

CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO user_logs (user_id, action)
    VALUES (NEW.id, 'USER_CREATED');
END //

DELIMITER ;
```

Now:

```sql
INSERT INTO users (id, username)
VALUES (10, 'dara');
```

The trigger automatically inserts a log.

## `NEW` and `OLD`

For triggers:

```text
NEW → new row value
OLD → previous row value
```

---

# 45. CTE

CTE means **Common Table Expression**.

Syntax:

```sql
WITH student_data AS (
    SELECT *
    FROM students
)
SELECT *
FROM student_data;
```

Example:

```sql
WITH expensive_products AS (
    SELECT *
    FROM products
    WHERE price > 1000
)
SELECT *
FROM expensive_products;
```

CTEs make complex queries easier to read.

---

# 46. Recursive CTE

Recursive CTEs can work with hierarchical data.

Example:

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS n

    UNION ALL

    SELECT n + 1
    FROM numbers
    WHERE n < 10
)
SELECT *
FROM numbers;
```

Result:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 47. Window Functions

Window functions calculate values across related rows without collapsing them into one row.

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average
FROM employees;
```

---

## ROW_NUMBER

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_number
FROM employees;
```

---

## RANK

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

## DENSE_RANK

```sql
SELECT
    name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 48. Common Table Expressions + Window Functions

Example:

```sql
WITH ranked_employees AS (
    SELECT
        id,
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS ranking
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE ranking <= 3;
```

This finds the top 3 employees by salary in each department.

---

# 49. UNION

Combine results:

```sql
SELECT name
FROM students

UNION

SELECT name
FROM teachers;
```

`UNION` removes duplicate rows.

`UNION ALL` keeps duplicates:

```sql
SELECT name
FROM students

UNION ALL

SELECT name
FROM teachers;
```

The corresponding SELECT statements must have compatible numbers and types of columns.

---

# 50. JSON

MySQL supports a native `JSON` data type.

Create:

```sql
CREATE TABLE products_json (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    attributes JSON
);
```

Insert:

```sql
INSERT INTO products_json
    (id, name, attributes)
VALUES
    (
        1,
        'Laptop',
        '{"brand":"Dell","ram":16,"storage":512}'
    );
```

Read JSON:

```sql
SELECT attributes
FROM products_json;
```

Get a JSON property:

```sql
SELECT
    JSON_EXTRACT(attributes, '$.brand') AS brand
FROM products_json;
```

Using arrow syntax:

```sql
SELECT
    attributes->'$.brand' AS brand
FROM products_json;
```

Unquoted scalar:

```sql
SELECT
    attributes->>'$.brand' AS brand
FROM products_json;
```

---

# 51. User Management

Create a MySQL user:

```sql
CREATE USER 'app_user'@'localhost'
IDENTIFIED BY 'StrongPassword123!';
```

Change password:

```sql
ALTER USER 'app_user'@'localhost'
IDENTIFIED BY 'NewStrongPassword123!';
```

Drop user:

```sql
DROP USER 'app_user'@'localhost';
```

---

# 52. Roles and Privileges

Create role:

```sql
CREATE ROLE 'app_read_only';
```

Grant permission:

```sql
GRANT SELECT
ON school.*
TO 'app_read_only';
```

Assign role:

```sql
GRANT 'app_read_only'
TO 'app_user'@'localhost';
```

Set default role:

```sql
SET DEFAULT ROLE 'app_read_only'
TO 'app_user'@'localhost';
```

Show grants:

```sql
SHOW GRANTS FOR 'app_user'@'localhost';
```

Revoke:

```sql
REVOKE SELECT
ON school.*
FROM 'app_read_only';
```

---

# 53. Backup and Restore

## Backup

Using `mysqldump`:

```bash
mysqldump -u root -p school > school_backup.sql
```

## Restore

```bash
mysql -u root -p school < school_backup.sql
```

## Backup multiple databases

```bash
mysqldump -u root -p \
    --databases school company \
    > databases_backup.sql
```

## Backup all databases

```bash
mysqldump -u root -p \
    --all-databases \
    > all_databases.sql
```

> For large production systems, choose a backup strategy appropriate to your MySQL deployment, including physical backup tooling and point-in-time recovery where required.

---

# 54. EXPLAIN

`EXPLAIN` helps understand how MySQL plans to execute a query.

```sql
EXPLAIN
SELECT *
FROM students
WHERE name = 'Dara';
```

For a more detailed execution analysis, MySQL also supports:

```sql
EXPLAIN ANALYZE
SELECT *
FROM students
WHERE name = 'Dara';
```

Important things to inspect include:

```text
access method
possible keys
chosen key
rows examined
estimated cost
```

---

# 55. Query Optimization

## Bad

```sql
SELECT *
FROM students;
```

If you only need two columns:

## Better

```sql
SELECT id, name
FROM students;
```

---

## Add an appropriate index

```sql
CREATE INDEX idx_students_name
ON students(name);
```

Then:

```sql
SELECT id, name
FROM students
WHERE name = 'Dara';
```

---

## Avoid unnecessary functions on indexed columns

Instead of:

```sql
SELECT *
FROM users
WHERE YEAR(created_at) = 2026;
```

Prefer a range when appropriate:

```sql
SELECT *
FROM users
WHERE created_at >= '2026-01-01'
  AND created_at < '2027-01-01';
```

---

## Use LIMIT when appropriate

```sql
SELECT id, name
FROM students
ORDER BY id
LIMIT 20;
```

---

# 56. Normalization

Normalization organizes data to reduce unnecessary duplication and improve consistency.

## Bad design

```text
orders

id | customer_name | customer_email | product_name
```

If the same customer creates 100 orders, their information is repeated many times.

## Better design

```text
customers
---------
id
name
email

orders
------
id
customer_id
```

Relationship:

```text
customers
    |
    | 1
    |
    | N
  orders
```

---

## 1NF

First Normal Form:

* Atomic values
* No repeating groups

Bad:

```text
phone_numbers = "111,222,333"
```

Better:

```text
customer_phones
---------------
customer_id
phone
```

---

## 2NF

Must be in 1NF and non-key attributes must depend on the whole primary key.

This matters especially with composite keys.

---

## 3NF

Must be in 2NF and non-key attributes should not depend on other non-key attributes.

---

# 57. Database Relationships

## One-to-One

```text
User
 |
 | 1
 |
 | 1
 |
Profile
```

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE profiles (
    id INT PRIMARY KEY,
    user_id INT NOT NULL UNIQUE,
    bio TEXT,
    FOREIGN KEY (user_id)
        REFERENCES users(id)
);
```

---

## One-to-Many

One department has many employees.

```text
Department
    |
    | 1
    |
    | N
 Employee
```

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT NOT NULL,
    FOREIGN KEY (department_id)
        REFERENCES departments(id)
);
```

---

## Many-to-Many

Students can enroll in many courses.

Courses can have many students.

Use a junction table:

```text
students
   |
   |
student_courses
   |
   |
courses
```

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE courses (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    enrolled_at DATETIME DEFAULT CURRENT_TIMESTAMP,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(id),

    FOREIGN KEY (course_id)
        REFERENCES courses(id)
);
```

---

# 58. Transactions and Locking

Transactions can be used together with row-level locking.

Example:

```sql
START TRANSACTION;

SELECT
    id,
    balance
FROM accounts
WHERE id = 1
FOR UPDATE;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

COMMIT;
```

`FOR UPDATE` requests locking behavior appropriate for protecting rows during a transaction.

Another useful option is:

```sql
SELECT *
FROM accounts
WHERE id = 1
FOR SHARE;
```

Use locking carefully because locks can cause waiting and deadlocks.

---

# 59. MySQL Project

Let's build a small **Shop Management Database**.

---

## Step 1 — Create Database

```sql
CREATE DATABASE shop_db;

USE shop_db;
```

---

## Step 2 — Create Customers

```sql
CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    phone VARCHAR(30),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Step 3 — Create Categories

```sql
CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
```

---

## Step 4 — Create Products

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    category_id INT NOT NULL,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_products_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id),

    CONSTRAINT chk_products_price
        CHECK (price >= 0),

    CONSTRAINT chk_products_stock
        CHECK (stock >= 0)
);
```

---

## Step 5 — Create Orders

```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_customer
        FOREIGN KEY (customer_id)
        REFERENCES customers(id)
);
```

---

## Step 6 — Create Order Items

```sql
CREATE TABLE order_items (
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,

    PRIMARY KEY (order_id, product_id),

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id),

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id),

    CONSTRAINT chk_order_items_quantity
        CHECK (quantity > 0),

    CONSTRAINT chk_order_items_price
        CHECK (unit_price >= 0)
);
```

---

## Step 7 — Insert Categories

```sql
INSERT INTO categories (name)
VALUES
    ('Laptop'),
    ('Phone'),
    ('Tablet');
```

---

## Step 8 — Insert Products

```sql
INSERT INTO products
    (category_id, name, price, stock)
VALUES
    (1, 'Dell Laptop', 850.00, 10),
    (1, 'HP Laptop', 900.00, 8),
    (2, 'iPhone', 1200.00, 15),
    (2, 'Samsung Galaxy', 800.00, 20),
    (3, 'iPad', 700.00, 12);
```

---

## Step 9 — Insert Customers

```sql
INSERT INTO customers
    (name, email, phone)
VALUES
    ('Dara', 'dara@example.com', '012345678'),
    ('Sokha', 'sokha@example.com', '098765432'),
    ('Vanna', 'vanna@example.com', '011223344');
```

---

## Step 10 — Insert Orders

```sql
INSERT INTO orders (customer_id)
VALUES
    (1),
    (2);
```

---

## Step 11 — Insert Order Items

```sql
INSERT INTO order_items
    (order_id, product_id, quantity, unit_price)
VALUES
    (1, 1, 2, 850.00),
    (1, 3, 1, 1200.00),
    (2, 4, 2, 800.00);
```

---

# 60. Query the Shop Database

## Get all products

```sql
SELECT *
FROM products;
```

---

## Products with category

```sql
SELECT
    p.id,
    p.name AS product,
    c.name AS category,
    p.price,
    p.stock
FROM products p
JOIN categories c
    ON p.category_id = c.id;
```

---

## Get customer orders

```sql
SELECT
    o.id AS order_id,
    c.name AS customer,
    o.order_date
FROM orders o
JOIN customers c
    ON o.customer_id = c.id;
```

---

## Calculate order totals

```sql
SELECT
    oi.order_id,
    SUM(oi.quantity * oi.unit_price) AS total
FROM order_items oi
GROUP BY oi.order_id;
```

---

## Full order report

```sql
SELECT
    o.id AS order_id,
    c.name AS customer,
    p.name AS product,
    oi.quantity,
    oi.unit_price,
    oi.quantity * oi.unit_price AS subtotal
FROM orders o
JOIN customers c
    ON o.customer_id = c.id
JOIN order_items oi
    ON o.id = oi.order_id
JOIN products p
    ON oi.product_id = p.id
ORDER BY o.id;
```

---

## Customer spending

```sql
SELECT
    c.id,
    c.name,
    COALESCE(
        SUM(oi.quantity * oi.unit_price),
        0
    ) AS total_spent
FROM customers c
LEFT JOIN orders o
    ON c.id = o.customer_id
LEFT JOIN order_items oi
    ON o.id = oi.order_id
GROUP BY c.id, c.name
ORDER BY total_spent DESC;
```

---

# 61. Best Practices

## 1. Use meaningful table names

Good:

```text
customers
products
orders
order_items
```

Avoid confusing names like:

```text
t1
data1
abc
```

---

## 2. Use consistent naming

Example:

```text
created_at
updated_at
customer_id
product_id
```

---

## 3. Always use primary keys

Good:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## 4. Use foreign keys for relationships

```sql
FOREIGN KEY (customer_id)
REFERENCES customers(id)
```

---

## 5. Avoid `SELECT *` in application queries

Instead of:

```sql
SELECT *
FROM users;
```

Prefer:

```sql
SELECT
    id,
    username,
    email
FROM users;
```

---

## 6. Use parameters in application code

Do not build SQL using unsafe string concatenation.

Bad concept:

```text
"SELECT * FROM users WHERE id = " + userInput
```

Use parameterized queries / prepared statements.

---

## 7. Index columns used for important lookups

Example:

```sql
CREATE INDEX idx_users_email
ON users(email);
```

But do not create indexes blindly.

---

## 8. Check query plans

```sql
EXPLAIN
SELECT *
FROM users
WHERE email = 'dara@example.com';
```

For supported MySQL versions:

```sql
EXPLAIN ANALYZE
SELECT *
FROM users
WHERE email = 'dara@example.com';
```

---

## 9. Use transactions for multi-step operations

```sql
START TRANSACTION;

-- operation 1
-- operation 2
-- operation 3

COMMIT;
```

If something fails:

```sql
ROLLBACK;
```

---

## 10. Don't store passwords as plain text

Never:

```text
password = "123456"
```

Applications should store passwords using a strong password-hashing algorithm and verify them through the application's authentication library.

---

# 62. SQL Command Categories

MySQL SQL can be thought of in several common categories.

## DDL — Data Definition Language

Used to define database objects.

```sql
CREATE
ALTER
DROP
TRUNCATE
```

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY
);
```

---

## DML — Data Manipulation Language

Used to modify data.

```sql
INSERT
UPDATE
DELETE
```

Example:

```sql
INSERT INTO users (id)
VALUES (1);
```

---

## DQL — Data Query Language

Commonly used to describe querying:

```sql
SELECT
```

Example:

```sql
SELECT *
FROM users;
```

---

## DCL — Data Control Language

Used for permissions.

```sql
GRANT
REVOKE
```

---

## TCL — Transaction Control Language

Used for transactions.

```sql
START TRANSACTION
COMMIT
ROLLBACK
SAVEPOINT
```

---

# 63. ALTER TABLE

Add column:

```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(30);
```

Modify column:

```sql
ALTER TABLE users
MODIFY COLUMN phone VARCHAR(50);
```

Rename column:

```sql
ALTER TABLE users
RENAME COLUMN phone TO phone_number;
```

Rename table:

```sql
RENAME TABLE users TO customers;
```

Drop column:

```sql
ALTER TABLE customers
DROP COLUMN phone_number;
```

---

# 64. TRUNCATE

Remove all rows:

```sql
TRUNCATE TABLE users;
```

Difference:

```text
DELETE
→ removes rows
→ can use WHERE

TRUNCATE
→ removes all rows
→ cannot use WHERE
```

Example:

```sql
DELETE FROM users
WHERE id = 1;
```

But:

```sql
TRUNCATE TABLE users;
```

removes all rows.

---

# 65. AUTO_INCREMENT

Example:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

Insert without ID:

```sql
INSERT INTO users (name)
VALUES ('Dara');
```

MySQL automatically generates the ID.

---

# 66. DEFAULT

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL,
    status VARCHAR(20) DEFAULT 'active'
);
```

Insert:

```sql
INSERT INTO users (username)
VALUES ('Dara');
```

The status becomes:

```text
active
```

---

# 67. CHECK

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    price DECIMAL(10,2),
    stock INT,

    CHECK (price >= 0),
    CHECK (stock >= 0)
);
```

Invalid data such as a negative price should be rejected when the constraint is enforced.

---

# 68. COALESCE

Return the first non-NULL value:

```sql
SELECT COALESCE(NULL, NULL, 'Hello');
```

Result:

```text
Hello
```

Example:

```sql
SELECT
    name,
    COALESCE(phone, 'No phone')
FROM customers;
```

---

# 69. NULLIF

```sql
SELECT NULLIF(10, 10);
```

Result:

```text
NULL
```

If values are different:

```sql
SELECT NULLIF(10, 20);
```

Result:

```text
10
```

---

# 70. Conditional Aggregation

Example:

```sql
SELECT
    COUNT(*) AS total_employees,

    SUM(
        CASE
            WHEN salary >= 1000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees;
```

Another example:

```sql
SELECT
    department_id,

    SUM(
        CASE
            WHEN salary >= 1000 THEN 1
            ELSE 0
        END
    ) AS high_salary,

    SUM(
        CASE
            WHEN salary < 1000 THEN 1
            ELSE 0
        END
    ) AS low_salary

FROM employees
GROUP BY department_id;
```

---

# 71. Pagination

Basic pagination:

```sql
SELECT
    id,
    name,
    email
FROM users
ORDER BY id
LIMIT 20 OFFSET 0;
```

Second page:

```sql
SELECT
    id,
    name,
    email
FROM users
ORDER BY id
LIMIT 20 OFFSET 20;
```

Third page:

```sql
SELECT
    id,
    name,
    email
FROM users
ORDER BY id
LIMIT 20 OFFSET 40;
```

For very large datasets, keyset/cursor pagination can be more efficient than large offsets.

Example:

```sql
SELECT
    id,
    name,
    email
FROM users
WHERE id > 1000
ORDER BY id
LIMIT 20;
```

---

# 72. EXISTS vs IN

Using `IN`:

```sql
SELECT *
FROM customers
WHERE id IN (
    SELECT customer_id
    FROM orders
);
```

Using `EXISTS`:

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

Which is faster depends on the query, indexes, data distribution, and optimizer plan.

Use:

```sql
EXPLAIN
```

to inspect the actual plan.

---

# 73. Correlated Subquery

Example:

```sql
SELECT
    e.name,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

This finds employees whose salary is above the average salary of their own department.

---

# 74. Advanced Window Function Example

```sql
SELECT
    id,
    name,
    department_id,
    salary,

    ROW_NUMBER() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS salary_rank,

    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average

FROM employees;
```

---

# 75. Running Total

Suppose:

```sql
CREATE TABLE sales (
    id INT PRIMARY KEY,
    sale_date DATE NOT NULL,
    amount DECIMAL(10,2) NOT NULL
);
```

Query:

```sql
SELECT
    id,
    sale_date,
    amount,

    SUM(amount) OVER (
        ORDER BY sale_date, id
    ) AS running_total

FROM sales;
```

---

# 76. LAG and LEAD

Previous value:

```sql
SELECT
    sale_date,
    amount,
    LAG(amount) OVER (
        ORDER BY sale_date
    ) AS previous_amount
FROM sales;
```

Next value:

```sql
SELECT
    sale_date,
    amount,
    LEAD(amount) OVER (
        ORDER BY sale_date
    ) AS next_amount
FROM sales;
```

---

# 77. Ranking Top Products

```sql
WITH product_sales AS (
    SELECT
        p.id,
        p.name,
        SUM(oi.quantity * oi.unit_price) AS revenue
    FROM products p
    JOIN order_items oi
        ON p.id = oi.product_id
    GROUP BY p.id, p.name
)
SELECT
    id,
    name,
    revenue,
    RANK() OVER (
        ORDER BY revenue DESC
    ) AS ranking
FROM product_sales;
```

---

# 78. Database Design Example

A typical e-commerce system:

```text
                    ┌──────────────┐
                    │  customers   │
                    └──────┬───────┘
                           │
                           │ 1:N
                           ↓
                    ┌──────────────┐
                    │    orders    │
                    └──────┬───────┘
                           │
                           │ 1:N
                           ↓
                  ┌─────────────────┐
                  │   order_items   │
                  └────────┬────────┘
                           │
                           │ N:1
                           ↓
                    ┌──────────────┐
                    │   products   │
                    └──────┬───────┘
                           │
                           │ N:1
                           ↓
                    ┌──────────────┐
                    │  categories  │
                    └──────────────┘
```

---

# 79. Production Database Architecture

A typical application:

```text
┌───────────────┐
│   Frontend    │
│ React / Vue   │
│ Angular / etc │
└───────┬───────┘
        │
        │ HTTP / HTTPS
        ↓
┌───────────────┐
│   Backend     │
│ Node / Java   │
│ Go / PHP      │
│ Python / etc  │
└───────┬───────┘
        │
        │ SQL
        ↓
┌───────────────┐
│     MySQL     │
│    Database   │
└───────────────┘
```

---

# 80. MySQL Learning Roadmap

## Beginner

Learn:

```text
1. Database
2. Table
3. Row
4. Column
5. Data Types
6. CREATE
7. INSERT
8. SELECT
9. WHERE
10. UPDATE
11. DELETE
12. ORDER BY
13. LIMIT
14. DISTINCT
```

---

## Intermediate

Learn:

```text
1. Primary Key
2. Foreign Key
3. Constraints
4. JOIN
5. GROUP BY
6. HAVING
7. Aggregate Functions
8. Subqueries
9. CASE
10. Views
11. Indexes
12. Transactions
13. Relationships
14. Normalization
```

---

## Advanced

Learn:

```text
1. CTE
2. Recursive CTE
3. Window Functions
4. Stored Procedures
5. Stored Functions
6. Triggers
7. JSON
8. Query Optimization
9. EXPLAIN
10. Locking
11. Transaction Isolation
12. User Privileges
13. Roles
14. Backup
15. Recovery
16. Database Architecture
```

---

# 81. MySQL Cheat Sheet

## Database

```sql
CREATE DATABASE database_name;

SHOW DATABASES;

USE database_name;

DROP DATABASE database_name;
```

## Table

```sql
CREATE TABLE table_name (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

SHOW TABLES;

DESCRIBE table_name;

DROP TABLE table_name;
```

## Insert

```sql
INSERT INTO table_name
    (id, name)
VALUES
    (1, 'Dara');
```

## Select

```sql
SELECT *
FROM table_name;
```

## Where

```sql
SELECT *
FROM table_name
WHERE id = 1;
```

## Update

```sql
UPDATE table_name
SET name = 'Sokha'
WHERE id = 1;
```

## Delete

```sql
DELETE FROM table_name
WHERE id = 1;
```

## Sort

```sql
SELECT *
FROM table_name
ORDER BY name ASC;
```

## Limit

```sql
SELECT *
FROM table_name
LIMIT 10;
```

## Count

```sql
SELECT COUNT(*)
FROM table_name;
```

## Group

```sql
SELECT name, COUNT(*)
FROM table_name
GROUP BY name;
```

## Join

```sql
SELECT *
FROM table1 t1
JOIN table2 t2
    ON t1.id = t2.table1_id;
```

## Transaction

```sql
START TRANSACTION;

-- SQL

COMMIT;
```

Rollback:

```sql
ROLLBACK;
```

## Index

```sql
CREATE INDEX index_name
ON table_name(column_name);
```

## View

```sql
CREATE VIEW view_name AS
SELECT *
FROM table_name;
```

## Procedure

```sql
CALL procedure_name();
```

## Explain

```sql
EXPLAIN
SELECT *
FROM table_name;
```

---

# 82. Important SQL Concepts

```text
Database
   ↓
Tables
   ↓
Rows + Columns
   ↓
Primary Keys
   ↓
Foreign Keys
   ↓
Relationships
   ↓
Queries
   ↓
JOIN
   ↓
Aggregation
   ↓
Indexes
   ↓
Transactions
   ↓
Optimization
   ↓
Security
   ↓
Backup & Recovery
```

---

# 83. Recommended Learning Order

### Level 1 — Beginner

```text
SQL
 ↓
Database
 ↓
Table
 ↓
CREATE
 ↓
INSERT
 ↓
SELECT
 ↓
WHERE
 ↓
UPDATE
 ↓
DELETE
```

### Level 2 — Intermediate

```text
Primary Key
 ↓
Foreign Key
 ↓
Constraints
 ↓
JOIN
 ↓
GROUP BY
 ↓
HAVING
 ↓
Subqueries
 ↓
Views
```

### Level 3 — Advanced

```text
Indexes
 ↓
Transactions
 ↓
Stored Procedures
 ↓
Triggers
 ↓
CTE
 ↓
Window Functions
 ↓
JSON
 ↓
EXPLAIN
 ↓
Optimization
```

### Level 4 — Professional

```text
Database Design
 ↓
Normalization
 ↓
Index Design
 ↓
Transaction Isolation
 ↓
Locking
 ↓
Security
 ↓
Backup
 ↓
Recovery
 ↓
Monitoring
 ↓
Performance Optimization
```

---

# 84. Final Example

A complete query using multiple advanced concepts:

```sql
WITH customer_sales AS (
    SELECT
        c.id,
        c.name,
        SUM(oi.quantity * oi.unit_price) AS total_spent
    FROM customers c
    JOIN orders o
        ON c.id = o.customer_id
    JOIN order_items oi
        ON o.id = oi.order_id
    GROUP BY c.id, c.name
),
ranked_customers AS (
    SELECT
        id,
        name,
        total_spent,
        RANK() OVER (
            ORDER BY total_spent DESC
        ) AS customer_rank
    FROM customer_sales
)
SELECT
    id,
    name,
    total_spent,
    customer_rank,
    CASE
        WHEN total_spent >= 5000 THEN 'VIP'
        WHEN total_spent >= 1000 THEN 'Premium'
        ELSE 'Regular'
    END AS customer_type
FROM ranked_customers
ORDER BY customer_rank;
```

This example combines:

```text
CTE
+
JOIN
+
SUM
+
GROUP BY
+
Window Function
+
RANK
+
CASE
+
ORDER BY
```

---

# 85. Summary

MySQL is much more than basic `SELECT` queries.

A strong MySQL developer should understand:

```text
                MySQL
                  │
       ┌──────────┴──────────┐
       │                     │
    SQL Basics          Database Design
       │                     │
   SELECT                  Keys
   INSERT                Relations
   UPDATE               Normalization
   DELETE                    │
       │                     │
       ├──────── JOIN ────────┤
       │                     │
   Aggregation            Indexes
       │                     │
   GROUP BY              EXPLAIN
   HAVING                Optimization
       │                     │
       └─────────┬───────────┘
                 │
            Transactions
                 │
       ┌─────────┴─────────┐
       │                   │
   Procedures            Triggers
       │                   │
       └─────────┬─────────┘
                 │
             Advanced
                 │
       CTE / Window / JSON
                 │
                 ↓
       Production MySQL
                 │
       Security / Backup
       Recovery / Monitoring
```

## 🇰🇭 សង្ខេបជាភាសាខ្មែរ

ដើម្បីក្លាយជា MySQL Developer ដែលមានមូលដ្ឋានរឹងមាំ គួររៀនតាមលំដាប់៖

```text
SQL Basics
   ↓
Database & Table
   ↓
CRUD
   ↓
Primary Key / Foreign Key
   ↓
JOIN
   ↓
GROUP BY / HAVING
   ↓
Subquery
   ↓
View
   ↓
Index
   ↓
Transaction
   ↓
Stored Procedure / Function
   ↓
Trigger
   ↓
CTE
   ↓
Window Function
   ↓
JSON
   ↓
Database Design
   ↓
Optimization
   ↓
Security
   ↓
Backup & Recovery
```

> **Practice is the most important part.** Build real projects such as a **Student Management System, Inventory System, POS System, E-Commerce System, Banking System, or Hospital Management System** to become comfortable with MySQL.
