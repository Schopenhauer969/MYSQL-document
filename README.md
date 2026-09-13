# MySQL — Beginner to Advanced

> A complete MySQL learning guide from **Beginner → Intermediate → Advanced**, with English + Khmer explanations and practical SQL examples.

---

## 📚 Table of Contents

* [1. What is MySQL?](#1-what-is-mysql)
* [2. Installation](#2-installation)
* [3. MySQL Concepts](#3-mysql-concepts)
* [4. Connect to MySQL](#4-connect-to-mysql)
* [5. Create Database](#5-create-database)
* [6. Create Table](#6-create-table)
* [7. Data Types](#7-data-types)
* [8. INSERT](#8-insert)
* [9. SELECT](#9-select)
* [10. WHERE](#10-where)
* [11. ORDER BY](#11-order-by)
* [12. LIMIT](#12-limit)
* [13. UPDATE](#13-update)
* [14. DELETE](#14-delete)
* [15. NULL](#15-null)
* [16. Constraints](#16-constraints)
* [17. Primary Key](#17-primary-key)
* [18. Foreign Key](#18-foreign-key)
* [19. Relationships](#19-relationships)
* [20. JOIN](#20-join)
* [21. Aggregate Functions](#21-aggregate-functions)
* [22. GROUP BY](#22-group-by)
* [23. HAVING](#23-having)
* [24. String Functions](#24-string-functions)
* [25. Date and Time](#25-date-and-time)
* [26. CASE](#26-case)
* [27. Subqueries](#27-subqueries)
* [28. CTE](#28-cte)
* [29. Views](#29-views)
* [30. Indexes](#30-indexes)
* [31. Transactions](#31-transactions)
* [32. Stored Procedures](#32-stored-procedures)
* [33. Functions](#33-functions)
* [34. Triggers](#34-triggers)
* [35. Events](#35-events)
* [36. Window Functions](#36-window-functions)
* [37. JSON](#37-json)
* [38. Common Table Expressions](#38-common-table-expressions)
* [39. Recursive CTE](#39-recursive-cte)
* [40. Query Optimization](#40-query-optimization)
* [41. EXPLAIN](#41-explain)
* [42. Normalization](#42-normalization)
* [43. Security](#43-security)
* [44. Users and Privileges](#44-users-and-privileges)
* [45. Backup and Restore](#45-backup-and-restore)
* [46. Database Design](#46-database-design)
* [47. Advanced Project](#47-advanced-project)
* [48. Best Practices](#48-best-practices)
* [49. SQL Cheat Sheet](#49-sql-cheat-sheet)

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

Example:

```text
Database: school

students
--------------------------------
id | name       | age | gender
--------------------------------
1  | Dara       | 20  | Male
2  | Sreyneang  | 21  | Female
```

## Khmer

**MySQL** គឺជា Database Management System ដែលប្រើសម្រាប់រក្សាទុក និងគ្រប់គ្រងទិន្នន័យ។

ទិន្នន័យត្រូវបានរៀបចំជា៖

```text
Database
   ↓
Table
   ↓
Row
   ↓
Column
```

ឧទាហរណ៍៖ Database `school` មាន Table `students`។

---

# 2. Installation

You can install MySQL Server and MySQL client tools.

Common tools:

* MySQL Server
* MySQL Workbench
* MySQL Shell
* phpMyAdmin
* DBeaver

After installation, check:

```bash
mysql --version
```

Example:

```text
mysql  Ver 8.0.x
```

## Khmer

បន្ទាប់ពី Install MySQL រួច អាចពិនិត្យ Version ដោយ៖

```bash
mysql --version
```

---

# 3. MySQL Concepts

The most important concepts:

| Concept     | Meaning                      |
| ----------- | ---------------------------- |
| Database    | Container for tables         |
| Table       | Stores structured data       |
| Row         | One record                   |
| Column      | One attribute                |
| Primary Key | Unique identifier            |
| Foreign Key | Connects tables              |
| Index       | Improves searching           |
| Query       | SQL command                  |
| Transaction | Group of database operations |

## Khmer

* **Database** = កន្លែងផ្ទុក Tables
* **Table** = កន្លែងផ្ទុកទិន្នន័យ
* **Row** = ទិន្នន័យមួយ Record
* **Column** = ប្រភេទព័ត៌មានមួយ
* **Primary Key** = ID មិនស្ទួន
* **Foreign Key** = ភ្ជាប់ Tables
* **Index** = ជួយឲ្យ Search លឿន
* **Transaction** = ក្រុមការងារ Database ដែលត្រូវធ្វើជាមួយគ្នា

---

# 4. Connect to MySQL

Open terminal:

```bash
mysql -u root -p
```

Then enter your password.

Connect to a specific host:

```bash
mysql -h localhost -u root -p
```

Connect to a database:

```bash
mysql -u root -p database_name
```

## Khmer

```bash
mysql -u root -p
```

មានន័យថា៖

* `-u` = username
* `root` = MySQL user
* `-p` = password

---

# 5. Create Database

## Create

```sql
CREATE DATABASE school;
```

## Create safely

```sql
CREATE DATABASE IF NOT EXISTS school;
```

## Show databases

```sql
SHOW DATABASES;
```

## Select database

```sql
USE school;
```

## Delete database

```sql
DROP DATABASE school;
```

## Khmer

បង្កើត Database៖

```sql
CREATE DATABASE school;
```

ប្រើ Database៖

```sql
USE school;
```

មើល Database ទាំងអស់៖

```sql
SHOW DATABASES;
```

> ⚠️ `DROP DATABASE` នឹងលុប Database ទាំងមូល។

---

# 6. Create Table

Create a simple table:

```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    gender VARCHAR(20)
);
```

Check tables:

```sql
SHOW TABLES;
```

Check table structure:

```sql
DESCRIBE students;
```

Alternative:

```sql
SHOW CREATE TABLE students;
```

## Khmer

Table `students` មាន៖

```text
id      → លេខសម្គាល់
name    → ឈ្មោះ
age     → អាយុ
gender  → ភេទ
```

---

# 7. Data Types

## Numeric

```sql
INT
BIGINT
DECIMAL(10,2)
FLOAT
DOUBLE
```

Example:

```sql
price DECIMAL(10,2)
quantity INT
```

## String

```sql
CHAR(10)
VARCHAR(255)
TEXT
```

Example:

```sql
name VARCHAR(100)
description TEXT
```

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
birth_date DATE
created_at DATETIME
```

## Boolean

MySQL commonly represents Boolean values using `BOOLEAN` / `BOOL`, which behave as numeric types:

```sql
is_active BOOLEAN
```

Typically:

```text
0 = FALSE
1 = TRUE
```

## Khmer

Data Type គឺកំណត់ថា Column មួយអាចរក្សាទុកទិន្នន័យប្រភេទអ្វី។

ឧទាហរណ៍៖

```sql
name VARCHAR(100)
age INT
price DECIMAL(10,2)
birth_date DATE
```

---

# 8. INSERT

Insert one record:

```sql
INSERT INTO students (name, age, gender)
VALUES ('Dara', 20, 'Male');
```

Insert multiple records:

```sql
INSERT INTO students (name, age, gender)
VALUES
    ('Dara', 20, 'Male'),
    ('Sokha', 21, 'Male'),
    ('Sreyneang', 22, 'Female'),
    ('Bopha', 19, 'Female');
```

Check:

```sql
SELECT * FROM students;
```

## Khmer

`INSERT` ប្រើសម្រាប់បញ្ចូលទិន្នន័យថ្មី។

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

Rename column:

```sql
SELECT
    name AS student_name,
    age AS student_age
FROM students;
```

## Khmer

`SELECT` ប្រើសម្រាប់យកទិន្នន័យចេញពី Database។

---

# 10. WHERE

Find students older than 20:

```sql
SELECT *
FROM students
WHERE age > 20;
```

Equal:

```sql
SELECT *
FROM students
WHERE gender = 'Male';
```

Multiple conditions:

```sql
SELECT *
FROM students
WHERE age >= 20
  AND gender = 'Male';
```

OR:

```sql
SELECT *
FROM students
WHERE age >= 20
   OR gender = 'Female';
```

NOT:

```sql
SELECT *
FROM students
WHERE NOT gender = 'Male';
```

BETWEEN:

```sql
SELECT *
FROM students
WHERE age BETWEEN 20 AND 25;
```

IN:

```sql
SELECT *
FROM students
WHERE gender IN ('Male', 'Female');
```

LIKE:

```sql
SELECT *
FROM students
WHERE name LIKE 'D%';
```

Meaning:

```text
D%   → starts with D
%D   → ends with D
%D%  → contains D
```

## Khmer

`WHERE` ប្រើសម្រាប់ Filter ទិន្នន័យ។

---

# 11. ORDER BY

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

## Khmer

`ORDER BY` ប្រើសម្រាប់តម្រៀបទិន្នន័យ។

```text
ASC  = តូច → ធំ
DESC = ធំ → តូច
```

---

# 12. LIMIT

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
Get 10 rows
```

## Khmer

`LIMIT` ប្រើសម្រាប់កំណត់ចំនួន Row ដែលចង់បាន។

---

# 13. UPDATE

Update one student:

```sql
UPDATE students
SET age = 21
WHERE id = 1;
```

Update multiple columns:

```sql
UPDATE students
SET
    age = 22,
    gender = 'Male'
WHERE id = 1;
```

> ⚠️ Always use `WHERE` when updating specific records.

Dangerous:

```sql
UPDATE students
SET age = 25;
```

This updates **every row**.

## Khmer

`UPDATE` ប្រើសម្រាប់កែប្រែទិន្នន័យ។

ត្រូវប្រយ័ត្ន៖

```sql
UPDATE students
SET age = 25;
```

នឹងកែ `age` របស់ Student ទាំងអស់។

---

# 14. DELETE

Delete one record:

```sql
DELETE FROM students
WHERE id = 1;
```

Delete records matching condition:

```sql
DELETE FROM students
WHERE age < 18;
```

Delete all rows:

```sql
DELETE FROM students;
```

> ⚠️ `DELETE FROM students;` deletes all rows.

## Khmer

`DELETE` ប្រើសម្រាប់លុបទិន្នន័យ។

ត្រូវប្រយ័ត្ន `DELETE` ដោយគ្មាន `WHERE`។

---

# 15. NULL

Find NULL:

```sql
SELECT *
FROM students
WHERE age IS NULL;
```

Find NOT NULL:

```sql
SELECT *
FROM students
WHERE age IS NOT NULL;
```

Do not use:

```sql
WHERE age = NULL;
```

Correct:

```sql
WHERE age IS NULL;
```

## COALESCE

```sql
SELECT
    name,
    COALESCE(age, 0) AS age
FROM students;
```

## Khmer

`NULL` មានន័យថា **គ្មានតម្លៃ / Unknown value**។

---

# 16. Constraints

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
    id INT PRIMARY KEY AUTO_INCREMENT,

    username VARCHAR(100) NOT NULL UNIQUE,

    email VARCHAR(255) NOT NULL UNIQUE,

    age INT CHECK (age >= 18),

    status VARCHAR(20) DEFAULT 'active'
);
```

## Khmer

Constraint ជាច្បាប់ដែលកំណត់លើ Data ដើម្បីការពារ Data មិនឲ្យខុស។

---

# 17. Primary Key

Example:

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);
```

Primary Key must be:

* Unique
* Not NULL
* Used to identify a row

## Khmer

`PRIMARY KEY` គឺជា ID សម្រាប់សម្គាល់ Record មួយៗ។

ឧទាហរណ៍៖

```text
id = 1
id = 2
id = 3
```

មិនអាចស្ទួនគ្នា។

---

# 18. Foreign Key

Create parent table:

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);
```

Create child table:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(id)
);
```

Insert:

```sql
INSERT INTO departments (name)
VALUES
    ('IT'),
    ('HR'),
    ('Finance');
```

```sql
INSERT INTO employees (name, department_id)
VALUES
    ('Dara', 1),
    ('Sokha', 1),
    ('Bopha', 2);
```

## Khmer

`FOREIGN KEY` ប្រើសម្រាប់ភ្ជាប់ Table មួយទៅ Table មួយ។

```text
departments
     ↑
     |
department_id
     |
employees
```

---

# 19. Relationships

## One-to-One

One user has one profile.

```text
users
  1
  |
  1
profiles
```

## One-to-Many

One department has many employees.

```text
departments
     1
     |
     |
     N
employees
```

## Many-to-Many

Students can take many courses, and courses can have many students.

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

Example:

```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE courses (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE student_courses (
    student_id INT NOT NULL,
    course_id INT NOT NULL,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(id),

    FOREIGN KEY (course_id)
        REFERENCES courses(id)
);
```

---

# 20. JOIN

Create example data:

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT NOT NULL,
    total DECIMAL(10,2) NOT NULL,

    FOREIGN KEY (customer_id)
        REFERENCES customers(id)
);
```

Insert:

```sql
INSERT INTO customers (name)
VALUES
    ('Dara'),
    ('Sokha'),
    ('Bopha');
```

```sql
INSERT INTO orders (customer_id, total)
VALUES
    (1, 100.00),
    (1, 250.00),
    (2, 75.00);
```

## INNER JOIN

```sql
SELECT
    customers.name,
    orders.total
FROM customers
INNER JOIN orders
    ON customers.id = orders.customer_id;
```

Returns only matching records.

## LEFT JOIN

```sql
SELECT
    customers.name,
    orders.total
FROM customers
LEFT JOIN orders
    ON customers.id = orders.customer_id;
```

Returns all customers, including customers without orders.

## RIGHT JOIN

```sql
SELECT
    customers.name,
    orders.total
FROM customers
RIGHT JOIN orders
    ON customers.id = orders.customer_id;
```

## CROSS JOIN

```sql
SELECT
    customers.name,
    orders.total
FROM customers
CROSS JOIN orders;
```

## Khmer

JOIN ប្រើសម្រាប់យក Data ពី Table ច្រើនមកភ្ជាប់គ្នា។

សំខាន់បំផុត៖

```text
INNER JOIN → តែ Data ដែល Match
LEFT JOIN  → Data ខាងឆ្វេងទាំងអស់
RIGHT JOIN → Data ខាងស្តាំទាំងអស់
```

---

# 21. Aggregate Functions

Common functions:

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Count:

```sql
SELECT COUNT(*) AS total_students
FROM students;
```

Sum:

```sql
SELECT SUM(total) AS total_sales
FROM orders;
```

Average:

```sql
SELECT AVG(total) AS average_order
FROM orders;
```

Minimum:

```sql
SELECT MIN(total) AS minimum_order
FROM orders;
```

Maximum:

```sql
SELECT MAX(total) AS maximum_order
FROM orders;
```

## Khmer

Aggregate Functions ប្រើសម្រាប់គណនា Data ច្រើន Row។

---

# 22. GROUP BY

Total orders by customer:

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count,
    SUM(total) AS total_spent
FROM orders
GROUP BY customer_id;
```

Join with customer name:

```sql
SELECT
    c.name,
    COUNT(o.id) AS order_count,
    COALESCE(SUM(o.total), 0) AS total_spent
FROM customers c
LEFT JOIN orders o
    ON c.id = o.customer_id
GROUP BY c.id, c.name;
```

## Khmer

`GROUP BY` ប្រើសម្រាប់បែងចែក Data ជាក្រុម។

---

# 23. HAVING

Find customers whose total spending is greater than 200:

```sql
SELECT
    customer_id,
    SUM(total) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(total) > 200;
```

Difference:

```text
WHERE  → filters rows before grouping
HAVING → filters groups after grouping
```

---

# 24. String Functions

## CONCAT

```sql
SELECT CONCAT('Hello ', 'World') AS message;
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
SELECT
    name,
    LENGTH(name) AS name_length
FROM students;
```

## TRIM

```sql
SELECT TRIM('   Hello   ');
```

## SUBSTRING

```sql
SELECT SUBSTRING('Database', 1, 4);
```

Result:

```text
Data
```

## REPLACE

```sql
SELECT REPLACE('Hello World', 'World', 'MySQL');
```

Result:

```text
Hello MySQL
```

---

# 25. Date and Time

Current date:

```sql
SELECT CURDATE();
```

Current time:

```sql
SELECT CURTIME();
```

Current datetime:

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

Add days:

```sql
SELECT DATE_ADD(CURDATE(), INTERVAL 7 DAY);
```

Subtract days:

```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 7 DAY);
```

Date difference:

```sql
SELECT DATEDIFF('2026-12-31', '2026-01-01');
```

Example:

```sql
SELECT *
FROM orders
WHERE created_at >= CURDATE() - INTERVAL 7 DAY;
```

## Khmer

MySQL មាន Function ជាច្រើនសម្រាប់គ្រប់គ្រង Date និង Time។

---

# 26. CASE

Example:

```sql
SELECT
    name,
    age,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 59 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM students;
```

Another example:

```sql
SELECT
    id,
    total,
    CASE
        WHEN total >= 500 THEN 'High'
        WHEN total >= 200 THEN 'Medium'
        ELSE 'Low'
    END AS order_level
FROM orders;
```

## Khmer

`CASE` មានអារម្មណ៍ដូចជា `if / else if / else`។

---

# 27. Subqueries

Find orders greater than the average order:

```sql
SELECT *
FROM orders
WHERE total > (
    SELECT AVG(total)
    FROM orders
);
```

Subquery with IN:

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE name = 'IT'
);
```

## Khmer

Subquery គឺ Query មួយនៅក្នុង Query មួយទៀត។

---

# 28. CTE

CTE means **Common Table Expression**.

Example:

```sql
WITH customer_totals AS (
    SELECT
        customer_id,
        SUM(total) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM customer_totals
WHERE total_spent > 200;
```

Multiple CTEs:

```sql
WITH
customer_totals AS (
    SELECT
        customer_id,
        SUM(total) AS total_spent
    FROM orders
    GROUP BY customer_id
),
large_customers AS (
    SELECT *
    FROM customer_totals
    WHERE total_spent > 200
)
SELECT *
FROM large_customers;
```

## Khmer

CTE ធ្វើឲ្យ Query ធំៗ អានងាយ និងរៀបចំ Logic បានល្អ។

---

# 29. Views

Create:

```sql
CREATE VIEW customer_order_summary AS
SELECT
    c.id,
    c.name,
    COUNT(o.id) AS order_count,
    COALESCE(SUM(o.total), 0) AS total_spent
FROM customers c
LEFT JOIN orders o
    ON c.id = o.customer_id
GROUP BY c.id, c.name;
```

Use:

```sql
SELECT *
FROM customer_order_summary;
```

Delete:

```sql
DROP VIEW customer_order_summary;
```

## Khmer

`VIEW` គឺជា Virtual Table ដែលផ្អែកលើ Query។

វាមានប្រយោជន៍ពេល Query ដដែលត្រូវប្រើញឹកញាប់។

---

# 30. Indexes

Indexes improve data lookup performance.

Create:

```sql
CREATE INDEX idx_students_name
ON students(name);
```

Multiple columns:

```sql
CREATE INDEX idx_students_gender_age
ON students(gender, age);
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

## Important

Do not create indexes on every column.

Indexes can:

```text
SELECT faster
```

but can make:

```text
INSERT
UPDATE
DELETE
```

more expensive because indexes also need maintenance.

## Khmer

Index ដូចជា Index ក្នុងសៀវភៅ។

វាជួយឲ្យ Search លឿន ប៉ុន្តែ Index ច្រើនពេកអាចធ្វើឲ្យ Insert/Update/Delete យឺត។

---

# 31. Transactions

Transactions are used when multiple operations must succeed or fail together.

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

Full example:

```sql
CREATE TABLE accounts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    balance DECIMAL(12,2) NOT NULL
);

INSERT INTO accounts (name, balance)
VALUES
    ('Dara', 1000.00),
    ('Sokha', 500.00);
```

Transfer:

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

## Khmer

Transaction សំខាន់សម្រាប់ Operation ដែលត្រូវជោគជ័យទាំងអស់ ឬបរាជ័យទាំងអស់។

ឧទាហរណ៍ Transfer Money៖

```text
Account A - $100
Account B + $100
```

បើ Operation មួយបរាជ័យ → `ROLLBACK`។

---

# 32. Stored Procedures

Create:

```sql
DELIMITER //

CREATE PROCEDURE GetAllStudents()
BEGIN
    SELECT *
    FROM students;
END //

DELIMITER ;
```

Call:

```sql
CALL GetAllStudents();
```

Procedure with parameter:

```sql
DELIMITER //

CREATE PROCEDURE GetStudentById(IN student_id INT)
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
DROP PROCEDURE GetAllStudents;
```

## Khmer

Stored Procedure គឺជា SQL Logic ដែលរក្សាទុកក្នុង Database ហើយអាចហៅប្រើឡើងវិញ។

---

# 33. Functions

Create a function:

```sql
DELIMITER //

CREATE FUNCTION AddTax(
    amount DECIMAL(10,2),
    tax_rate DECIMAL(5,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN amount + (amount * tax_rate / 100);
END //

DELIMITER ;
```

Use:

```sql
SELECT AddTax(100, 10);
```

Result:

```text
110.00
```

Drop:

```sql
DROP FUNCTION AddTax;
```

## Khmer

Function បង្កើត Logic ដែល Return តម្លៃមួយ។

---

# 34. Triggers

A trigger automatically runs when an event happens.

Example audit table:

```sql
CREATE TABLE student_audit (
    id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT NOT NULL,
    action VARCHAR(50) NOT NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

Create trigger:

```sql
DELIMITER //

CREATE TRIGGER after_student_insert
AFTER INSERT ON students
FOR EACH ROW
BEGIN
    INSERT INTO student_audit (student_id, action)
    VALUES (NEW.id, 'INSERT');
END //

DELIMITER ;
```

Insert:

```sql
INSERT INTO students (name, age, gender)
VALUES ('Kanha', 20, 'Female');
```

Check:

```sql
SELECT *
FROM student_audit;
```

## Khmer

Trigger គឺ Logic ដែល Database ដំណើរការដោយស្វ័យប្រវត្តិ ពេលមាន Event ដូចជា:

```text
INSERT
UPDATE
DELETE
```

---

# 35. Events

Events allow MySQL to run scheduled SQL.

Enable event scheduler:

```sql
SET GLOBAL event_scheduler = ON;
```

Example:

```sql
CREATE EVENT delete_old_audit
ON SCHEDULE EVERY 1 DAY
DO
    DELETE FROM student_audit
    WHERE created_at < NOW() - INTERVAL 30 DAY;
```

Show events:

```sql
SHOW EVENTS;
```

Drop:

```sql
DROP EVENT delete_old_audit;
```

## Khmer

Event ប្រើសម្រាប់ការងារដែលត្រូវ Run តាមពេលវេលា ដោយស្វ័យប្រវត្តិ។

---

# 36. Window Functions

Window functions calculate values across related rows without collapsing them.

Example:

```sql
SELECT
    id,
    customer_id,
    total,
    SUM(total) OVER (
        PARTITION BY customer_id
    ) AS customer_total
FROM orders;
```

Ranking:

```sql
SELECT
    id,
    customer_id,
    total,
    ROW_NUMBER() OVER (
        PARTITION BY customer_id
        ORDER BY total DESC
    ) AS row_number
FROM orders;
```

Rank:

```sql
SELECT
    id,
    total,
    RANK() OVER (
        ORDER BY total DESC
    ) AS sales_rank
FROM orders;
```

Dense rank:

```sql
SELECT
    id,
    total,
    DENSE_RANK() OVER (
        ORDER BY total DESC
    ) AS sales_rank
FROM orders;
```

## Khmer

Window Function អាចគណនា Data តាម Group ដោយមិនបាត់ Row ដើម។

---

# 37. JSON

MySQL supports JSON data.

Create table:

```sql
CREATE TABLE products_json (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    attributes JSON
);
```

Insert JSON:

```sql
INSERT INTO products_json (name, attributes)
VALUES (
    'Laptop',
    JSON_OBJECT(
        'brand', 'Dell',
        'ram', 16,
        'storage', 512
    )
);
```

Read:

```sql
SELECT
    name,
    attributes
FROM products_json;
```

Extract:

```sql
SELECT
    name,
    attributes->>'$.brand' AS brand,
    attributes->>'$.ram' AS ram
FROM products_json;
```

Search:

```sql
SELECT *
FROM products_json
WHERE attributes->>'$.brand' = 'Dell';
```

## Khmer

JSON មានប្រយោជន៍ពេល Data មាន Structure ដែលអាចផ្លាស់ប្តូរ។

ប៉ុន្តែសម្រាប់ Data ដែលមាន Structure ច្បាស់ គួរពិចារណាប្រើ Columns ធម្មតា។

---

# 38. Common Table Expressions

Basic:

```sql
WITH totals AS (
    SELECT
        customer_id,
        SUM(total) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM totals;
```

CTE + JOIN:

```sql
WITH totals AS (
    SELECT
        customer_id,
        SUM(total) AS total_spent
    FROM orders
    GROUP BY customer_id
)
SELECT
    c.name,
    t.total_spent
FROM customers c
JOIN totals t
    ON c.id = t.customer_id;
```

## Khmer

CTE ជួយបំបែក Query ធំៗទៅជាផ្នែកតូចៗដែលអានងាយ។

---

# 39. Recursive CTE

Useful for hierarchical data.

Create categories:

```sql
CREATE TABLE categories (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    parent_id INT NULL,

    FOREIGN KEY (parent_id)
        REFERENCES categories(id)
);
```

Insert:

```sql
INSERT INTO categories (name, parent_id)
VALUES
    ('Electronics', NULL),
    ('Computers', 1),
    ('Laptops', 2),
    ('Gaming Laptops', 3);
```

Recursive query:

```sql
WITH RECURSIVE category_tree AS (
    SELECT
        id,
        name,
        parent_id,
        0 AS level
    FROM categories
    WHERE parent_id IS NULL

    UNION ALL

    SELECT
        c.id,
        c.name,
        c.parent_id,
        ct.level + 1
    FROM categories c
    JOIN category_tree ct
        ON c.parent_id = ct.id
)
SELECT *
FROM category_tree
ORDER BY level, id;
```

## Khmer

Recursive CTE ប្រើសម្រាប់ Data មានទម្រង់ Tree ដូចជា៖

```text
Electronics
└── Computers
    └── Laptops
        └── Gaming Laptops
```

---

# 40. Query Optimization

Bad:

```sql
SELECT *
FROM orders;
```

Better:

```sql
SELECT
    id,
    customer_id,
    total
FROM orders;
```

Instead of:

```sql
WHERE YEAR(created_at) = 2026
```

Prefer a range:

```sql
WHERE created_at >= '2026-01-01'
  AND created_at < '2027-01-01';
```

Why?

Applying functions to an indexed column can make index usage less effective.

## Avoid unnecessary operations

Avoid:

```sql
SELECT DISTINCT *
FROM huge_table;
```

unless you actually need `DISTINCT`.

Avoid unnecessary joins.

Use appropriate indexes.

Return only required columns.

Use pagination for large datasets.

## Khmer

Optimization មានន័យថា ធ្វើឲ្យ Query:

```text
លឿន
ប្រើ RAM តិច
ប្រើ CPU តិច
ប្រើ Disk I/O តិច
```

---

# 41. EXPLAIN

Use:

```sql
EXPLAIN
SELECT *
FROM students
WHERE name = 'Dara';
```

For more detailed execution information:

```sql
EXPLAIN ANALYZE
SELECT *
FROM students
WHERE name = 'Dara';
```

Look for information such as:

```text
access type
possible keys
chosen key
estimated rows
execution details
```

## Khmer

`EXPLAIN` ជួយយើងយល់ថា MySQL ដំណើរការ Query ដោយរបៀបណា។

ប្រើវាពេល Query យឺត។

---

# 42. Normalization

Normalization helps reduce duplicated data and improve data consistency.

## Bad design

```text
orders

id
customer_name
customer_email
product_name
product_price
```

If the same customer makes 100 orders, customer information is duplicated.

## Better design

```text
customers
---------
id
name
email

products
--------
id
name
price

orders
------
id
customer_id
created_at

order_items
-----------
order_id
product_id
quantity
price
```

## First Normal Form — 1NF

Each column should contain atomic values.

Bad:

```text
phone = "012345678,098765432"
```

Better:

```text
customer_phones
---------------
customer_id
phone
```

## Second Normal Form — 2NF

Remove partial dependencies from composite keys.

## Third Normal Form — 3NF

Remove dependencies where non-key columns depend on other non-key columns.

## Khmer

Normalization គឺការរៀបចំ Database ដើម្បីកាត់បន្ថយ Data ស្ទួន និងធ្វើឲ្យ Data មានភាពត្រឹមត្រូវ។

---

# 43. Security

Never build SQL like this:

```text
"SELECT * FROM users WHERE username = '" + username + "'"
```

This can lead to SQL Injection.

## Use prepared statements

Example concept:

```sql
SELECT *
FROM users
WHERE email = ?;
```

Application code supplies the value separately.

For example in Node.js:

```javascript
const [rows] = await connection.execute(
    'SELECT * FROM users WHERE email = ?',
    [email]
);
```

## Passwords

Never store plain-text passwords.

Bad:

```text
password = "mypassword123"
```

Use a password hashing algorithm from your application framework/library, such as:

```text
Argon2id
bcrypt
```

Store the resulting hash, not the original password.

## Khmer

កុំរក្សាទុក Password ជា Plain Text។

កុំបង្កើត SQL ដោយបញ្ចូល User Input ដោយផ្ទាល់។

ត្រូវប្រើ:

```text
Prepared Statements
Password Hashing
Least Privilege
```

---

# 44. Users and Privileges

Create user:

```sql
CREATE USER 'app_user'@'localhost'
IDENTIFIED BY 'StrongPasswordHere';
```

Create database:

```sql
CREATE DATABASE shop;
```

Grant permissions:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON shop.*
TO 'app_user'@'localhost';
```

Show grants:

```sql
SHOW GRANTS FOR 'app_user'@'localhost';
```

Remove privileges:

```sql
REVOKE DELETE
ON shop.*
FROM 'app_user'@'localhost';
```

Drop user:

```sql
DROP USER 'app_user'@'localhost';
```

## Best Practice

Do not use:

```text
root
```

for an application.

Create a dedicated application user with only the permissions it needs.

## Khmer

Application មិនគួរប្រើ `root` User ទេ។

គួរបង្កើត User ផ្ទាល់ខ្លួន ហើយផ្តល់ Permission ត្រឹមតែអ្វីដែល Application ត្រូវការ។

---

# 45. Backup and Restore

## Backup with mysqldump

```bash
mysqldump -u root -p school > school.sql
```

## Backup a specific database

```bash
mysqldump -u root -p school > school_backup.sql
```

## Restore

Create database:

```sql
CREATE DATABASE school;
```

Then:

```bash
mysql -u root -p school < school.sql
```

## Backup multiple databases

```bash
mysqldump -u root -p --databases school shop > databases.sql
```

## Backup all databases

```bash
mysqldump -u root -p --all-databases > all_databases.sql
```

## Khmer

Backup គឺសំខាន់ណាស់សម្រាប់ Production Database។

គួរមាន:

```text
Regular backup
Off-site backup
Backup testing
Recovery plan
```

Backup ដែលមិនធ្លាប់ Test Restore មិនគួរចាត់ទុកថា Reliable ទេ។

---

# 46. Database Design

A typical e-commerce database:

```text
users
-----
id
name
email
password_hash

products
--------
id
name
description
price
stock

categories
----------
id
name

product_categories
------------------
product_id
category_id

orders
------
id
user_id
status
created_at

order_items
-----------
id
order_id
product_id
quantity
price

payments
--------
id
order_id
amount
status
paid_at
```

Relationship:

```text
users
  |
  | 1
  |
  | N
orders
  |
  | 1
  |
  | N
order_items
  |
  | N
  |
  | 1
products
```

---

# 47. Advanced Project

## E-Commerce Database

Create database:

```sql
CREATE DATABASE ecommerce;

USE ecommerce;
```

## Users

```sql
CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
        ON UPDATE CURRENT_TIMESTAMP
);
```

## Categories

```sql
CREATE TABLE categories (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

## Products

```sql
CREATE TABLE products (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    category_id BIGINT UNSIGNED NULL,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(12,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0,
    is_active BOOLEAN NOT NULL DEFAULT TRUE,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
        ON UPDATE CURRENT_TIMESTAMP,

    CONSTRAINT fk_products_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id)
        ON DELETE SET NULL,

    CONSTRAINT chk_products_price
        CHECK (price >= 0),

    CONSTRAINT chk_products_stock
        CHECK (stock >= 0)
);
```

## Orders

```sql
CREATE TABLE orders (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    status VARCHAR(30) NOT NULL DEFAULT 'pending',
    total_amount DECIMAL(12,2) NOT NULL DEFAULT 0,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
        ON UPDATE CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
);
```

## Order Items

```sql
CREATE TABLE order_items (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    order_id BIGINT UNSIGNED NOT NULL,
    product_id BIGINT UNSIGNED NOT NULL,
    quantity INT NOT NULL,
    unit_price DECIMAL(12,2) NOT NULL,

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id)
        ON DELETE CASCADE,

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id),

    CONSTRAINT chk_order_items_quantity
        CHECK (quantity > 0),

    CONSTRAINT chk_order_items_price
        CHECK (unit_price >= 0)
);
```

## Payments

```sql
CREATE TABLE payments (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    order_id BIGINT UNSIGNED NOT NULL,
    amount DECIMAL(12,2) NOT NULL,
    status VARCHAR(30) NOT NULL DEFAULT 'pending',
    paid_at DATETIME NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_payments_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id)
        ON DELETE CASCADE,

    CONSTRAINT chk_payments_amount
        CHECK (amount >= 0)
);
```

---

# 48. Advanced Queries

## Get all products with category

```sql
SELECT
    p.id,
    p.name,
    p.price,
    p.stock,
    c.name AS category_name
FROM products p
LEFT JOIN categories c
    ON p.category_id = c.id;
```

## Get order summary

```sql
SELECT
    o.id AS order_id,
    u.name AS customer_name,
    o.status,
    o.total_amount,
    o.created_at
FROM orders o
JOIN users u
    ON o.user_id = u.id
ORDER BY o.created_at DESC;
```

## Calculate order total

```sql
SELECT
    oi.order_id,
    SUM(oi.quantity * oi.unit_price) AS calculated_total
FROM order_items oi
GROUP BY oi.order_id;
```

## Top-selling products

```sql
SELECT
    p.id,
    p.name,
    SUM(oi.quantity) AS total_quantity
FROM order_items oi
JOIN products p
    ON oi.product_id = p.id
GROUP BY p.id, p.name
ORDER BY total_quantity DESC
LIMIT 10;
```

## Revenue by month

```sql
SELECT
    YEAR(o.created_at) AS year,
    MONTH(o.created_at) AS month,
    SUM(o.total_amount) AS revenue
FROM orders o
WHERE o.status = 'completed'
GROUP BY
    YEAR(o.created_at),
    MONTH(o.created_at)
ORDER BY year, month;
```

## Customer lifetime value

```sql
SELECT
    u.id,
    u.name,
    COALESCE(SUM(
        CASE
            WHEN o.status = 'completed'
            THEN o.total_amount
            ELSE 0
        END
    ), 0) AS lifetime_value
FROM users u
LEFT JOIN orders o
    ON u.id = o.user_id
GROUP BY u.id, u.name
ORDER BY lifetime_value DESC;
```

---

# 49. Best Practices

## Naming

Use consistent names:

```text
snake_case
```

Good:

```sql
created_at
updated_at
user_id
order_items
```

Avoid mixing:

```text
createdAt
created_at
CreatedAt
```

within the same project.

---

## Always define Primary Keys

Good:

```sql
CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT
);
```

---

## Use Foreign Keys

Good:

```sql
FOREIGN KEY (user_id)
REFERENCES users(id)
```

This protects referential integrity.

---

## Use DECIMAL for Money

Good:

```sql
price DECIMAL(12,2)
```

Avoid using floating-point types for exact monetary values when exact decimal arithmetic is required.

---

## Use UTC consistently for timestamps

For distributed applications, keeping timestamps in UTC and converting them to the user's local timezone at the application/UI layer is usually easier to manage.

Example:

```sql
created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
```

---

## Avoid SELECT *

Instead of:

```sql
SELECT *
FROM users;
```

Prefer:

```sql
SELECT
    id,
    name,
    email
FROM users;
```

---

## Always use WHERE for targeted UPDATE/DELETE

Good:

```sql
UPDATE users
SET name = 'Dara'
WHERE id = 1;
```

Good:

```sql
DELETE FROM users
WHERE id = 1;
```

Be extremely careful with:

```sql
UPDATE users
SET name = 'Dara';
```

and:

```sql
DELETE FROM users;
```

---

# 50. SQL Cheat Sheet

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
    id INT PRIMARY KEY AUTO_INCREMENT
);

SHOW TABLES;

DESCRIBE table_name;

DROP TABLE table_name;
```

## Insert

```sql
INSERT INTO table_name (column1, column2)
VALUES ('value1', 'value2');
```

## Select

```sql
SELECT *
FROM table_name;
```

## Filter

```sql
SELECT *
FROM table_name
WHERE column1 = 'value';
```

## Sort

```sql
SELECT *
FROM table_name
ORDER BY column1 DESC;
```

## Limit

```sql
SELECT *
FROM table_name
LIMIT 10;
```

## Update

```sql
UPDATE table_name
SET column1 = 'new_value'
WHERE id = 1;
```

## Delete

```sql
DELETE FROM table_name
WHERE id = 1;
```

## Count

```sql
SELECT COUNT(*)
FROM table_name;
```

## Sum

```sql
SELECT SUM(amount)
FROM payments;
```

## Average

```sql
SELECT AVG(amount)
FROM payments;
```

## Group

```sql
SELECT
    category_id,
    COUNT(*) AS total
FROM products
GROUP BY category_id;
```

## Having

```sql
SELECT
    category_id,
    COUNT(*) AS total
FROM products
GROUP BY category_id
HAVING COUNT(*) > 5;
```

## Join

```sql
SELECT
    a.name,
    b.total
FROM customers a
JOIN orders b
    ON a.id = b.customer_id;
```

## Transaction

```sql
START TRANSACTION;

-- SQL operations

COMMIT;
```

Rollback:

```sql
ROLLBACK;
```

---

# 51. Recommended Learning Path

## Beginner

Learn these first:

```text
1. Database
2. Table
3. Data Types
4. CREATE
5. INSERT
6. SELECT
7. WHERE
8. ORDER BY
9. LIMIT
10. UPDATE
11. DELETE
12. NULL
```

## Intermediate

Then learn:

```text
1. Primary Keys
2. Foreign Keys
3. Relationships
4. JOIN
5. GROUP BY
6. HAVING
7. Aggregate Functions
8. String Functions
9. Date Functions
10. CASE
11. Subqueries
12. Views
13. Indexes
14. Transactions
```

## Advanced

Finally learn:

```text
1. CTE
2. Recursive CTE
3. Window Functions
4. JSON
5. Stored Procedures
6. Functions
7. Triggers
8. Events
9. EXPLAIN
10. Query Optimization
11. Normalization
12. Security
13. Permissions
14. Backup & Restore
15. Production Database Design
```

---

# 52. MySQL Mental Model

When writing SQL, think in this order:

```text
FROM
  ↓
JOIN
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
  ↓
LIMIT
```

Example:

```sql
SELECT
    c.name,
    COUNT(o.id) AS order_count,
    SUM(o.total) AS total_spent
FROM customers c
LEFT JOIN orders o
    ON c.id = o.customer_id
WHERE o.total > 0
GROUP BY c.id, c.name
HAVING SUM(o.total) > 100
ORDER BY total_spent DESC
LIMIT 10;
```

---

# 53. Real-World MySQL Architecture

A typical application can look like:

```text
                    ┌───────────────┐
                    │   Frontend    │
                    │ React / Vue   │
                    │ Angular / etc │
                    └───────┬───────┘
                            │
                            │ HTTP/HTTPS
                            ▼
                    ┌───────────────┐
                    │      API      │
                    │ Node / Java   │
                    │ Go / C# / PHP │
                    └───────┬───────┘
                            │
                            │ SQL
                            ▼
                    ┌───────────────┐
                    │     MySQL     │
                    │   Database    │
                    └───────────────┘
```

## Khmer

Architecture ទូទៅ៖

```text
Frontend
   ↓
Backend / API
   ↓
MySQL
```

Frontend មិនគួរភ្ជាប់ MySQL ដោយផ្ទាល់ទេ។

ត្រូវប្រើ Backend/API ជាអ្នកគ្រប់គ្រង Database។

---

# 54. Production Checklist

Before deploying MySQL to production:

```text
[ ] Use strong database passwords
[ ] Do not use root for application
[ ] Use least-privilege accounts
[ ] Use prepared statements
[ ] Validate user input
[ ] Add appropriate indexes
[ ] Review slow queries
[ ] Use transactions where necessary
[ ] Configure backups
[ ] Test restoring backups
[ ] Monitor database performance
[ ] Monitor disk usage
[ ] Monitor connections
[ ] Use SSL/TLS where appropriate
[ ] Protect database credentials
[ ] Never commit passwords to Git
```

---

# 55. Environment Variables

Never put database passwords directly in source code.

Bad:

```javascript
const password = "MySecretPassword";
```

Better:

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=ecommerce
DB_USER=app_user
DB_PASSWORD=your_password
```

Then your application reads environment variables.

Never commit:

```text
.env
```

Add to `.gitignore`:

```gitignore
.env
.env.*
!.env.example
```

Create:

```text
.env.example
```

Example:

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=ecommerce
DB_USER=app_user
DB_PASSWORD=
```

---

# 56. Example Project Structure

```text
my-mysql-project/
│
├── README.md
├── .gitignore
├── .env.example
│
├── database/
│   ├── migrations/
│   │   ├── 001_create_users.sql
│   │   ├── 002_create_products.sql
│   │   └── 003_create_orders.sql
│   │
│   ├── seeds/
│   │   └── development.sql
│   │
│   └── queries/
│       ├── users.sql
│       ├── products.sql
│       └── orders.sql
│
└── docs/
    ├── database-design.md
    └── api-database.md
```

## Khmer

ការរៀបចំ Folder ឲ្យច្បាស់ជួយឲ្យ Project ងាយ Maintenance និងធ្វើការជាមួយ Team។

---

# 57. Complete Example

Here is a small complete MySQL project.

## Step 1 — Database

```sql
CREATE DATABASE shop;

USE shop;
```

## Step 2 — Users

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Step 3 — Products

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0
);
```

## Step 4 — Orders

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (user_id)
        REFERENCES users(id)
);
```

## Step 5 — Order Items

```sql
CREATE TABLE order_items (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,

    FOREIGN KEY (order_id)
        REFERENCES orders(id)
        ON DELETE CASCADE,

    FOREIGN KEY (product_id)
        REFERENCES products(id)
);
```

## Step 6 — Insert Users

```sql
INSERT INTO users (name, email)
VALUES
    ('Dara', 'dara@example.com'),
    ('Sokha', 'sokha@example.com'),
    ('Bopha', 'bopha@example.com');
```

## Step 7 — Insert Products

```sql
INSERT INTO products (name, price, stock)
VALUES
    ('Laptop', 1200.00, 10),
    ('Mouse', 25.00, 50),
    ('Keyboard', 45.00, 30);
```

## Step 8 — Create Order

```sql
INSERT INTO orders (user_id)
VALUES (1);
```

## Step 9 — Add Order Items

```sql
INSERT INTO order_items (
    order_id,
    product_id,
    quantity,
    price
)
VALUES
    (1, 1, 1, 1200.00),
    (1, 2, 2, 25.00);
```

## Step 10 — Calculate Order Total

```sql
SELECT
    order_id,
    SUM(quantity * price) AS total
FROM order_items
WHERE order_id = 1
GROUP BY order_id;
```

Result:

```text
order_id | total
---------|-------
1        | 1250.00
```

## Step 11 — Show Order

```sql
SELECT
    o.id AS order_id,
    u.name AS customer,
    p.name AS product,
    oi.quantity,
    oi.price,
    oi.quantity * oi.price AS subtotal
FROM orders o
JOIN users u
    ON o.user_id = u.id
JOIN order_items oi
    ON o.id = oi.order_id
JOIN products p
    ON oi.product_id = p.id
WHERE o.id = 1;
```

---

# 58. Most Important SQL Commands

Memorize these:

```sql
CREATE DATABASE
DROP DATABASE

CREATE TABLE
ALTER TABLE
DROP TABLE

INSERT INTO
SELECT
UPDATE
DELETE

WHERE
AND
OR
IN
BETWEEN
LIKE
IS NULL

ORDER BY
GROUP BY
HAVING
LIMIT

INNER JOIN
LEFT JOIN
RIGHT JOIN

COUNT
SUM
AVG
MIN
MAX

CASE
COALESCE

CREATE INDEX
DROP INDEX

CREATE VIEW
DROP VIEW

START TRANSACTION
COMMIT
ROLLBACK

CREATE USER
GRANT
REVOKE
DROP USER

EXPLAIN
EXPLAIN ANALYZE
```

---

# 59. Final MySQL Roadmap

```text
                         MYSQL
                           │
          ┌────────────────┴────────────────┐
          │                                 │
       BEGINNER                         INTERMEDIATE
          │                                 │
     Database                         Relationships
     Tables                           JOIN
     Data Types                       GROUP BY
     INSERT                           HAVING
     SELECT                           Functions
     WHERE                            Subqueries
     UPDATE                           Views
     DELETE                           Indexes
     LIMIT                            Transactions
          │                                 │
          └────────────────┬────────────────┘
                           │
                        ADVANCED
                           │
              ┌────────────┼────────────┐
              │            │            │
             CTE       Window Func     JSON
              │            │            │
          Recursive     Ranking      Documents
              │            │            │
              └────────────┼────────────┘
                           │
                     PERFORMANCE
                           │
                    EXPLAIN
                    Indexing
                    Optimization
                           │
                       SECURITY
                           │
                  Users / Privileges
                  Prepared Statements
                  Backups
                           │
                      PRODUCTION
                           │
                  Database Architecture
                  Monitoring
                  Recovery
                  Scaling
```

---

# 60. Conclusion

MySQL is much more than simply writing:

```sql
SELECT * FROM users;
```

A professional MySQL developer should understand:

```text
SQL
    ↓
Database Design
    ↓
Relationships
    ↓
Indexes
    ↓
Transactions
    ↓
Security
    ↓
Optimization
    ↓
Backup & Recovery
    ↓
Production Architecture
```

## Khmer Summary

បើចង់រៀន MySQL ពី Beginner ទៅ Advanced គួររៀនតាមលំដាប់៖

```text
1. Database
2. Table
3. CRUD
4. WHERE
5. JOIN
6. GROUP BY
7. Relationships
8. Constraints
9. Index
10. Transaction
11. Subquery
12. CTE
13. Window Function
14. JSON
15. Stored Procedure
16. Trigger
17. Security
18. EXPLAIN
19. Optimization
20. Backup
21. Production Database Design
```

---

# 🚀 Practice Projects

After learning this README, build these projects:

### Beginner

```text
1. Student Management System
2. Library Management System
3. Employee Management System
```

### Intermediate

```text
1. Inventory Management System
2. Restaurant Management System
3. School Management System
4. Hospital Management System
```

### Advanced

```text
1. E-Commerce System
2. Banking System
3. Food Delivery System
4. Hotel Booking System
5. Learning Management System
6. Point of Sale System
7. Multi-vendor Marketplace
```

---

# ⭐ Recommended Skill Order

```text
SQL Basics
   ↓
CRUD
   ↓
Constraints
   ↓
Relationships
   ↓
JOIN
   ↓
Aggregation
   ↓
Subqueries
   ↓
CTE
   ↓
Indexes
   ↓
Transactions
   ↓
Views
   ↓
Window Functions
   ↓
Stored Procedures
   ↓
Triggers
   ↓
JSON
   ↓
EXPLAIN
   ↓
Optimization
   ↓
Security
   ↓
Backup / Recovery
   ↓
Production Database Architecture
```

---

## License

This documentation can be used for learning, personal projects, and GitHub documentation.

---

## Author

**MySQL Beginner → Advanced Learning Guide**

Made for developers who want to learn MySQL step by step.

**English + Khmer 🇰🇭**

Happy Learning! 🚀
