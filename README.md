# 🐬 MySQL — Beginner to Advanced

> A complete MySQL learning guide from **Beginner → Intermediate → Advanced** with practical examples.
> មគ្គុទ្ទេសក៍ MySQL ពី **Beginner → Intermediate → Advanced** ជាមួយឧទាហរណ៍អនុវត្តជាក់ស្តែង។

---

## 📚 Table of Contents

* [1. What is MySQL?](#1-what-is-mysql)
* [2. Installation](#2-installation)
* [3. MySQL Basics](#3-mysql-basics)
* [4. Databases](#4-databases)
* [5. Tables](#5-tables)
* [6. Data Types](#6-data-types)
* [7. INSERT](#7-insert)
* [8. SELECT](#8-select)
* [9. WHERE](#9-where)
* [10. UPDATE](#10-update)
* [11. DELETE](#11-delete)
* [12. ORDER BY](#12-order-by)
* [13. LIMIT](#13-limit)
* [14. DISTINCT](#14-distinct)
* [15. Aggregate Functions](#15-aggregate-functions)
* [16. GROUP BY](#16-group-by)
* [17. HAVING](#17-having)
* [18. SQL Operators](#18-sql-operators)
* [19. LIKE](#19-like)
* [20. BETWEEN](#20-between)
* [21. IN](#21-in)
* [22. NULL](#22-null)
* [23. Constraints](#23-constraints)
* [24. Primary Key](#24-primary-key)
* [25. Foreign Key](#25-foreign-key)
* [26. Relationships](#26-relationships)
* [27. JOIN](#27-join)
* [28. Subqueries](#28-subqueries)
* [29. CASE](#29-case)
* [30. String Functions](#30-string-functions)
* [31. Date & Time Functions](#31-date--time-functions)
* [32. Numeric Functions](#32-numeric-functions)
* [33. Views](#33-views)
* [34. Indexes](#34-indexes)
* [35. Transactions](#35-transactions)
* [36. Stored Procedures](#36-stored-procedures)
* [37. Functions](#37-functions)
* [38. Triggers](#38-triggers)
* [39. CTE](#39-cte)
* [40. Window Functions](#40-window-functions)
* [41. Recursive CTE](#41-recursive-cte)
* [42. JSON](#42-json)
* [43. User Management](#43-user-management)
* [44. Permissions](#44-permissions)
* [45. Backup & Restore](#45-backup--restore)
* [46. EXPLAIN](#46-explain)
* [47. Query Optimization](#47-query-optimization)
* [48. Database Design](#48-database-design)
* [49. Normalization](#49-normalization)
* [50. Security](#50-security)
* [51. Complete Project](#51-complete-project)
* [52. Best Practices](#52-best-practices)
* [53. Cheat Sheet](#53-cheat-sheet)

---

# 1. What is MySQL?

**English**

MySQL is an open-source relational database management system (RDBMS).

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

**Khmer**

MySQL គឺជា Database Management System ប្រភេទ Relational Database ដែលប្រើ SQL ដើម្បីគ្រប់គ្រងទិន្នន័យ។

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

---

# 2. Installation

## Windows

Install MySQL Server and MySQL Workbench.

After installation, check:

```bash
mysql --version
```

Example:

```text
mysql  Ver 8.0.xx for Win64
```

## Linux

```bash
sudo apt update
sudo apt install mysql-server
```

Start MySQL:

```bash
sudo systemctl start mysql
```

Check status:

```bash
sudo systemctl status mysql
```

## Login

```bash
mysql -u root -p
```

Then enter your password.

---

# 3. MySQL Basics

## Start MySQL

```bash
mysql -u root -p
```

## Show MySQL version

```sql
SELECT VERSION();
```

## Show current database

```sql
SELECT DATABASE();
```

## Show current user

```sql
SELECT USER();
```

## Exit

```sql
EXIT;
```

or:

```sql
QUIT;
```

---

# 4. Databases

A database contains tables and other database objects.

## Create Database

```sql
CREATE DATABASE school;
```

**Khmer:** បង្កើត Database ឈ្មោះ `school`។

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

> ⚠️ `DROP DATABASE` permanently deletes the database and its data.

---

# 5. Tables

## Create Table

```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT,
    email VARCHAR(150),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Explanation

| Column       | Meaning           |
| ------------ | ----------------- |
| `id`         | Unique student ID |
| `name`       | Student name      |
| `age`        | Student age       |
| `email`      | Student email     |
| `created_at` | Creation time     |

**Khmer**

* `PRIMARY KEY` → កំណត់ ID ដែលមិនស្ទួន
* `AUTO_INCREMENT` → ID កើនដោយស្វ័យប្រវត្តិ
* `NOT NULL` → មិនអាចទទេ
* `DEFAULT` → តម្លៃលំនាំដើម

## Show Tables

```sql
SHOW TABLES;
```

## Describe Table

```sql
DESCRIBE students;
```

or:

```sql
DESC students;
```

## Delete Table

```sql
DROP TABLE students;
```

## Clear Table

```sql
TRUNCATE TABLE students;
```

---

# 6. Data Types

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
LONGTEXT
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
created_at TIMESTAMP
```

## Boolean

MySQL commonly represents Boolean values using:

```sql
BOOLEAN
```

which is effectively an alias for a numeric type.

Example:

```sql
is_active BOOLEAN DEFAULT TRUE
```

---

# 7. INSERT

Insert one row:

```sql
INSERT INTO students (name, age, email)
VALUES ('Dara', 20, 'dara@example.com');
```

Insert multiple rows:

```sql
INSERT INTO students (name, age, email)
VALUES
    ('Dara', 20, 'dara@example.com'),
    ('Sokha', 21, 'sokha@example.com'),
    ('Vanna', 19, 'vanna@example.com');
```

**Khmer**

`INSERT` ប្រើសម្រាប់បញ្ចូលទិន្នន័យថ្មីទៅក្នុង Table។

---

# 8. SELECT

Select everything:

```sql
SELECT *
FROM students;
```

Select specific columns:

```sql
SELECT id, name, email
FROM students;
```

Rename columns:

```sql
SELECT
    name AS student_name,
    email AS student_email
FROM students;
```

---

# 9. WHERE

Filter data.

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
WHERE age >= 18
  AND age <= 25;
```

**Khmer:** `WHERE` ប្រើសម្រាប់ Filter ទិន្នន័យ។

---

# 10. UPDATE

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

> ⚠️ Always be careful with `UPDATE` without `WHERE`.

Bad:

```sql
UPDATE students
SET age = 20;
```

This changes **every row**.

---

# 11. DELETE

Delete one row:

```sql
DELETE FROM students
WHERE id = 1;
```

Delete multiple rows:

```sql
DELETE FROM students
WHERE age < 18;
```

> ⚠️ Never run this casually:

```sql
DELETE FROM students;
```

It deletes every row.

---

# 12. ORDER BY

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

Multiple sorting columns:

```sql
SELECT *
FROM students
ORDER BY age DESC, name ASC;
```

---

# 13. LIMIT

Get first 5 records:

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
Take 10 rows
```

---

# 14. DISTINCT

Remove duplicate values.

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

# 15. Aggregate Functions

Common aggregate functions:

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

## COUNT

```sql
SELECT COUNT(*) AS total_students
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

# 16. GROUP BY

Group data.

Example:

```sql
SELECT
    age,
    COUNT(*) AS total
FROM students
GROUP BY age;
```

**Meaning:**

Students are grouped according to age.

**Khmer:** `GROUP BY` ប្រើសម្រាប់បែងចែកទិន្នន័យជាក្រុម។

---

# 17. HAVING

`HAVING` filters grouped results.

```sql
SELECT
    age,
    COUNT(*) AS total
FROM students
GROUP BY age
HAVING COUNT(*) > 1;
```

### WHERE vs HAVING

```text
WHERE
↓
Filters rows before grouping

GROUP BY
↓
Creates groups

HAVING
↓
Filters groups
```

---

# 18. SQL Operators

## Comparison

```sql
=
!=
<>
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

## Logical

```sql
AND
OR
NOT
```

Example:

```sql
SELECT *
FROM students
WHERE age >= 18
  AND age <= 30;
```

---

# 19. LIKE

Search by pattern.

Starts with:

```sql
SELECT *
FROM students
WHERE name LIKE 'D%';
```

Ends with:

```sql
SELECT *
FROM students
WHERE name LIKE '%a';
```

Contains:

```sql
SELECT *
FROM students
WHERE name LIKE '%ar%';
```

Single character:

```sql
SELECT *
FROM students
WHERE name LIKE '_a%';
```

### Wildcards

```text
%  → zero or more characters
_  → exactly one character
```

---

# 20. BETWEEN

```sql
SELECT *
FROM students
WHERE age BETWEEN 18 AND 25;
```

Date example:

```sql
SELECT *
FROM orders
WHERE order_date
BETWEEN '2026-01-01' AND '2026-12-31';
```

> For timestamp columns, be careful with inclusive end boundaries. For example, a half-open range can be safer:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
  AND order_date < '2027-01-01';
```

---

# 21. IN

Instead of:

```sql
WHERE age = 18
   OR age = 20
   OR age = 25
```

Use:

```sql
SELECT *
FROM students
WHERE age IN (18, 20, 25);
```

NOT IN:

```sql
SELECT *
FROM students
WHERE age NOT IN (18, 20, 25);
```

---

# 22. NULL

`NULL` means missing/unknown value.

Correct:

```sql
SELECT *
FROM students
WHERE email IS NULL;
```

Not:

```sql
WHERE email = NULL;
```

Find non-null:

```sql
SELECT *
FROM students
WHERE email IS NOT NULL;
```

---

# 23. Constraints

Constraints enforce rules.

Common constraints:

```sql
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
DEFAULT
CHECK
```

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    age INT CHECK (age >= 18),
    status VARCHAR(20) DEFAULT 'active'
);
```

---

# 24. Primary Key

A primary key uniquely identifies a row.

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);
```

Each row has a unique `id`.

---

# 25. Foreign Key

A foreign key connects tables.

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);
```

Orders:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT NOT NULL,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_customer
        FOREIGN KEY (customer_id)
        REFERENCES customers(id)
);
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

**Khmer:** Foreign Key ប្រើសម្រាប់ភ្ជាប់ Table មួយទៅ Table មួយទៀត។

---

# 26. Relationships

## One-to-One

```text
User
  |
  | 1
  |
Profile
```

## One-to-Many

```text
Customer
   |
   | 1
   |
   | N
 Orders
```

## Many-to-Many

Requires a junction table.

```text
Students
   |
   N
   |
student_courses
   |
   N
   |
Courses
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

# 27. JOIN

JOIN combines data from multiple tables.

## INNER JOIN

```sql
SELECT
    customers.id,
    customers.name,
    orders.id AS order_id
FROM customers
INNER JOIN orders
    ON customers.id = orders.customer_id;
```

Only matching records are returned.

---

## LEFT JOIN

```sql
SELECT
    customers.id,
    customers.name,
    orders.id AS order_id
FROM customers
LEFT JOIN orders
    ON customers.id = orders.customer_id;
```

Returns all customers, including customers without orders.

---

## RIGHT JOIN

```sql
SELECT
    customers.name,
    orders.id AS order_id
FROM customers
RIGHT JOIN orders
    ON customers.id = orders.customer_id;
```

Returns all rows from the right table.

---

## CROSS JOIN

```sql
SELECT
    customers.name,
    products.name
FROM customers
CROSS JOIN products;
```

Creates combinations between rows.

---

# 28. Subqueries

A subquery is a query inside another query.

Example:

```sql
SELECT *
FROM students
WHERE age > (
    SELECT AVG(age)
    FROM students
);
```

This finds students whose age is above the average.

---

# 29. CASE

`CASE` works like conditional logic.

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
    product_name,
    price,
    CASE
        WHEN price >= 1000 THEN 'Expensive'
        WHEN price >= 500 THEN 'Medium'
        ELSE 'Cheap'
    END AS price_category
FROM products;
```

---

# 30. String Functions

## CONCAT

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
SELECT TRIM(name)
FROM students;
```

## SUBSTRING

```sql
SELECT SUBSTRING(name, 1, 3)
FROM students;
```

---

# 31. Date & Time Functions

Current date:

```sql
SELECT CURRENT_DATE();
```

Current time:

```sql
SELECT CURRENT_TIME();
```

Current datetime:

```sql
SELECT CURRENT_TIMESTAMP();
```

Extract year:

```sql
SELECT YEAR(created_at)
FROM users;
```

Extract month:

```sql
SELECT MONTH(created_at)
FROM users;
```

Extract day:

```sql
SELECT DAY(created_at)
FROM users;
```

Add days:

```sql
SELECT DATE_ADD(CURRENT_DATE(), INTERVAL 7 DAY);
```

Subtract days:

```sql
SELECT DATE_SUB(CURRENT_DATE(), INTERVAL 7 DAY);
```

Difference:

```sql
SELECT DATEDIFF('2026-12-31', '2026-01-01');
```

---

# 32. Numeric Functions

## ROUND

```sql
SELECT ROUND(123.4567, 2);
```

Result:

```text
123.46
```

## CEIL

```sql
SELECT CEIL(10.2);
```

## FLOOR

```sql
SELECT FLOOR(10.9);
```

## ABS

```sql
SELECT ABS(-100);
```

## MOD

```sql
SELECT MOD(10, 3);
```

---

# 33. Views

A View is a saved query that behaves like a virtual table.

Create:

```sql
CREATE VIEW customer_orders AS
SELECT
    customers.id,
    customers.name,
    orders.id AS order_id,
    orders.order_date
FROM customers
JOIN orders
    ON customers.id = orders.customer_id;
```

Use:

```sql
SELECT *
FROM customer_orders;
```

Delete:

```sql
DROP VIEW customer_orders;
```

---

# 34. Indexes

Indexes improve lookup performance.

Create:

```sql
CREATE INDEX idx_students_email
ON students(email);
```

Multiple-column index:

```sql
CREATE INDEX idx_students_name_age
ON students(name, age);
```

Unique index:

```sql
CREATE UNIQUE INDEX idx_users_username
ON users(username);
```

Show indexes:

```sql
SHOW INDEX FROM students;
```

Delete index:

```sql
DROP INDEX idx_students_email
ON students;
```

### Important

Indexes can make reads faster, but they also consume storage and can make `INSERT`, `UPDATE`, and `DELETE` more expensive.

**Khmer:** កុំបង្កើត Index គ្រប់ Column ដោយគ្មានហេតុផល។

---

# 35. Transactions

Transactions allow multiple operations to behave as one logical unit.

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

### Example

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

-- If everything is correct:
COMMIT;

-- If something failed:
-- ROLLBACK;
```

**Khmer:** Transaction ជួយឱ្យការងារច្រើនត្រូវបានចាត់ទុកជាក្រុមតែមួយ។

---

# 36. Stored Procedures

Stored Procedure stores reusable SQL logic.

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

Delete:

```sql
DROP PROCEDURE GetStudentById;
```

---

# 37. Functions

Stored functions return a value.

```sql
DELIMITER //

CREATE FUNCTION CalculateTotal(
    price DECIMAL(10,2),
    quantity INT
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN price * quantity;
END //

DELIMITER ;
```

Use:

```sql
SELECT CalculateTotal(10.50, 3);
```

---

# 38. Triggers

A Trigger automatically executes when an event occurs.

Example:

```sql
CREATE TABLE product_logs (
    id INT PRIMARY KEY AUTO_INCREMENT,
    product_id INT NOT NULL,
    action VARCHAR(50) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Create trigger:

```sql
DELIMITER //

CREATE TRIGGER after_product_insert
AFTER INSERT ON products
FOR EACH ROW
BEGIN
    INSERT INTO product_logs (product_id, action)
    VALUES (NEW.id, 'INSERT');
END //

DELIMITER ;
```

Now:

```sql
INSERT INTO products (name, price)
VALUES ('Keyboard', 50.00);
```

The trigger automatically creates a log.

---

# 39. CTE

CTE means **Common Table Expression**.

Syntax:

```sql
WITH student_data AS (
    SELECT
        id,
        name,
        age
    FROM students
)
SELECT *
FROM student_data;
```

More useful example:

```sql
WITH average_age AS (
    SELECT AVG(age) AS avg_age
    FROM students
)
SELECT
    s.name,
    s.age
FROM students s
CROSS JOIN average_age a
WHERE s.age > a.avg_age;
```

CTEs make complex queries easier to read.

---

# 40. Window Functions

Window functions calculate values across related rows without collapsing them into one row.

## ROW_NUMBER

```sql
SELECT
    id,
    name,
    age,
    ROW_NUMBER() OVER (
        ORDER BY age DESC
    ) AS row_number
FROM students;
```

## RANK

```sql
SELECT
    name,
    age,
    RANK() OVER (
        ORDER BY age DESC
    ) AS ranking
FROM students;
```

## DENSE_RANK

```sql
SELECT
    name,
    age,
    DENSE_RANK() OVER (
        ORDER BY age DESC
    ) AS ranking
FROM students;
```

## PARTITION BY

```sql
SELECT
    department_id,
    name,
    salary,
    RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

**Khmer:** Window Function អាចគណនាទិន្នន័យតាមក្រុម ប៉ុន្តែមិនបង្រួម Row ដូច `GROUP BY` ទេ។

---

# 41. Recursive CTE

Recursive CTE is useful for hierarchical data.

Example:

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS number

    UNION ALL

    SELECT number + 1
    FROM numbers
    WHERE number < 10
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

# 42. JSON

MySQL supports JSON data.

Create table:

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    details JSON
);
```

Insert JSON:

```sql
INSERT INTO products (name, details)
VALUES (
    'Laptop',
    '{"brand": "Dell", "ram": 16, "storage": 512}'
);
```

Read JSON:

```sql
SELECT details
FROM products;
```

Extract property:

```sql
SELECT
    JSON_EXTRACT(details, '$.brand') AS brand
FROM products;
```

Using arrow syntax:

```sql
SELECT
    details->>'$.brand' AS brand
FROM products;
```

Search JSON:

```sql
SELECT *
FROM products
WHERE details->>'$.brand' = 'Dell';
```

---

# 43. User Management

Create user:

```sql
CREATE USER 'app_user'@'localhost'
IDENTIFIED BY 'StrongPassword123!';
```

Show users:

```sql
SELECT User, Host
FROM mysql.user;
```

Change password:

```sql
ALTER USER 'app_user'@'localhost'
IDENTIFIED BY 'NewStrongPassword123!';
```

Delete user:

```sql
DROP USER 'app_user'@'localhost';
```

> Never store database passwords directly in source code or GitHub repositories.

---

# 44. Permissions

Grant permissions:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON school.*
TO 'app_user'@'localhost';
```

Show grants:

```sql
SHOW GRANTS FOR 'app_user'@'localhost';
```

Remove permission:

```sql
REVOKE DELETE
ON school.*
FROM 'app_user'@'localhost';
```

For applications, give users only the permissions they actually need.

---

# 45. Backup & Restore

## Backup

Using `mysqldump`:

```bash
mysqldump -u root -p school > school_backup.sql
```

## Backup all databases

```bash
mysqldump -u root -p --all-databases > all_databases.sql
```

## Restore

```bash
mysql -u root -p school < school_backup.sql
```

Alternative:

```bash
mysql -u root -p < school_backup.sql
```

**Khmer:** Backup គឺសំខាន់សម្រាប់ការពារទិន្នន័យពីការបាត់បង់។

---

# 46. EXPLAIN

`EXPLAIN` helps understand how MySQL executes a query.

```sql
EXPLAIN
SELECT *
FROM students
WHERE email = 'dara@example.com';
```

For more detailed execution information:

```sql
EXPLAIN ANALYZE
SELECT *
FROM students
WHERE email = 'dara@example.com';
```

Use this when investigating slow queries.

---

# 47. Query Optimization

## Bad

```sql
SELECT *
FROM users;
```

If you only need two columns:

```sql
SELECT id, name
FROM users;
```

## Add useful indexes

```sql
CREATE INDEX idx_users_email
ON users(email);
```

Then:

```sql
SELECT id, name
FROM users
WHERE email = 'user@example.com';
```

## Avoid unnecessary functions on indexed columns

Instead of:

```sql
SELECT *
FROM users
WHERE YEAR(created_at) = 2026;
```

Prefer a range:

```sql
SELECT *
FROM users
WHERE created_at >= '2026-01-01'
  AND created_at < '2027-01-01';
```

## Check query plan

```sql
EXPLAIN
SELECT
    id,
    name
FROM users
WHERE email = 'user@example.com';
```

### Optimization checklist

```text
✓ Select only required columns
✓ Add appropriate indexes
✓ Use EXPLAIN
✓ Avoid unnecessary JOINs
✓ Avoid unnecessary subqueries
✓ Filter data early
✓ Use proper data types
✓ Keep transactions reasonably short
✓ Avoid N+1 queries in applications
✓ Monitor slow queries
```

---

# 48. Database Design

A good database should have clear entities and relationships.

Example e-commerce system:

```text
Users
  |
  | 1
  |
  | N
Orders
  |
  | 1
  |
  | N
Order_Items
  |
  | N
  |
  | 1
Products
```

Tables:

```text
users
products
orders
order_items
categories
payments
```

Example:

```sql
CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Products:

```sql
CREATE TABLE products (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(12,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Orders:

```sql
CREATE TABLE orders (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    status VARCHAR(30) NOT NULL DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
);
```

Order items:

```sql
CREATE TABLE order_items (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    order_id BIGINT UNSIGNED NOT NULL,
    product_id BIGINT UNSIGNED NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(12,2) NOT NULL,

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id),

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id)
);
```

---

# 49. Normalization

Normalization organizes data to reduce duplication and improve consistency.

## 1NF

Each column should contain atomic values.

Bad:

```text
id | name | phones
1  | Dara | 111,222,333
```

Better:

```text
users
-----
id
name
```

and:

```text
user_phones
-----------
id
user_id
phone
```

## 2NF

Must satisfy 1NF and remove partial dependencies from composite keys.

## 3NF

Must satisfy 2NF and remove transitive dependencies.

### Practical rule

Don't duplicate information unnecessarily.

Bad:

```text
orders
----------------------------------
id
customer_id
customer_name
customer_email
```

Better:

```text
customers
----------
id
name
email

orders
------
id
customer_id
```

Then use JOIN:

```sql
SELECT
    orders.id,
    customers.name,
    customers.email
FROM orders
JOIN customers
    ON customers.id = orders.customer_id;
```

---

# 50. Security

## Use Prepared Statements

Never build SQL by directly concatenating user input.

Bad application logic:

```text
"SELECT * FROM users WHERE email = '" + userInput + "'"
```

This can lead to SQL injection.

Use parameterized queries instead.

Example with Node.js:

```javascript
const [rows] = await connection.execute(
    'SELECT id, name, email FROM users WHERE email = ?',
    [email]
);
```

Example with Python:

```python
cursor.execute(
    "SELECT id, name, email FROM users WHERE email = %s",
    (email,)
)
```

## Strong Passwords

Use strong database passwords:

```text
✓ Long
✓ Unique
✓ Random
✓ Never committed to Git
```

## Environment Variables

Example `.env`:

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=school
DB_USER=app_user
DB_PASSWORD=your_password
```

Add `.env` to `.gitignore`:

```gitignore
.env
```

## Principle of Least Privilege

Do not use:

```text
root
```

for your normal application.

Create a dedicated application user.

---

# 51. Complete Project

Let's create a small **Student Management System**.

## Step 1 — Create Database

```sql
CREATE DATABASE school_db;

USE school_db;
```

## Step 2 — Create Students

```sql
CREATE TABLE students (
    id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    age INT UNSIGNED NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Step 3 — Insert Students

```sql
INSERT INTO students (name, email, age)
VALUES
    ('Dara', 'dara@example.com', 20),
    ('Sokha', 'sokha@example.com', 21),
    ('Vanna', 'vanna@example.com', 19),
    ('Sopheak', 'sopheak@example.com', 22);
```

## Step 4 — Read

```sql
SELECT *
FROM students;
```

## Step 5 — Find One

```sql
SELECT *
FROM students
WHERE id = 1;
```

## Step 6 — Search

```sql
SELECT *
FROM students
WHERE name LIKE '%Dara%';
```

## Step 7 — Update

```sql
UPDATE students
SET age = 21
WHERE id = 1;
```

## Step 8 — Delete

```sql
DELETE FROM students
WHERE id = 4;
```

## Step 9 — Count

```sql
SELECT COUNT(*) AS total_students
FROM students;
```

## Step 10 — Average Age

```sql
SELECT AVG(age) AS average_age
FROM students;
```

---

# 52. Complete E-Commerce Example

## Create Database

```sql
CREATE DATABASE ecommerce_db;

USE ecommerce_db;
```

## Users

```sql
CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Categories

```sql
CREATE TABLE categories (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE
);
```

## Products

```sql
CREATE TABLE products (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    category_id BIGINT UNSIGNED,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(12,2) NOT NULL,
    stock INT UNSIGNED NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_products_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id)
);
```

## Orders

```sql
CREATE TABLE orders (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    status VARCHAR(30) NOT NULL DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

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
    quantity INT UNSIGNED NOT NULL,
    price DECIMAL(12,2) NOT NULL,

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id),

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id)
);
```

## Insert Data

```sql
INSERT INTO users (name, email)
VALUES
    ('Dara', 'dara@example.com'),
    ('Sokha', 'sokha@example.com');
```

```sql
INSERT INTO categories (name)
VALUES
    ('Laptop'),
    ('Phone'),
    ('Accessory');
```

```sql
INSERT INTO products (category_id, name, price, stock)
VALUES
    (1, 'Dell Laptop', 850.00, 10),
    (1, 'HP Laptop', 750.00, 15),
    (2, 'iPhone', 1200.00, 5),
    (3, 'Keyboard', 50.00, 30);
```

## Create Order

```sql
INSERT INTO orders (user_id, status)
VALUES (1, 'pending');
```

## Add Order Items

```sql
INSERT INTO order_items (
    order_id,
    product_id,
    quantity,
    price
)
VALUES
    (1, 1, 1, 850.00),
    (1, 4, 2, 50.00);
```

## Calculate Order Total

```sql
SELECT
    order_id,
    SUM(quantity * price) AS total
FROM order_items
WHERE order_id = 1
GROUP BY order_id;
```

## Get Order Details

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
    ON u.id = o.user_id
JOIN order_items oi
    ON oi.order_id = o.id
JOIN products p
    ON p.id = oi.product_id
WHERE o.id = 1;
```

---

# 53. Advanced SQL Query Example

Find top customers by spending:

```sql
SELECT
    u.id,
    u.name,
    SUM(oi.quantity * oi.price) AS total_spent
FROM users u
JOIN orders o
    ON o.user_id = u.id
JOIN order_items oi
    ON oi.order_id = o.id
GROUP BY
    u.id,
    u.name
ORDER BY total_spent DESC;
```

Top 5:

```sql
SELECT
    u.id,
    u.name,
    SUM(oi.quantity * oi.price) AS total_spent
FROM users u
JOIN orders o
    ON o.user_id = u.id
JOIN order_items oi
    ON oi.order_id = o.id
GROUP BY
    u.id,
    u.name
ORDER BY total_spent DESC
LIMIT 5;
```

---

# 54. Pagination

For page 1:

```sql
SELECT *
FROM products
ORDER BY id
LIMIT 10 OFFSET 0;
```

Page 2:

```sql
SELECT *
FROM products
ORDER BY id
LIMIT 10 OFFSET 10;
```

Page 3:

```sql
SELECT *
FROM products
ORDER BY id
LIMIT 10 OFFSET 20;
```

Formula:

```text
OFFSET = (page - 1) × limit
```

For large datasets, consider keyset/cursor pagination rather than very large offsets.

Example:

```sql
SELECT *
FROM products
WHERE id > 1000
ORDER BY id
LIMIT 10;
```

---

# 55. Useful SQL Patterns

## Find duplicate emails

```sql
SELECT
    email,
    COUNT(*) AS total
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

If `email` is declared `UNIQUE`, duplicates should normally be prevented.

## Find products with low stock

```sql
SELECT *
FROM products
WHERE stock < 10;
```

## Find expensive products

```sql
SELECT *
FROM products
WHERE price > 1000;
```

## Find customers without orders

```sql
SELECT
    u.id,
    u.name
FROM users u
LEFT JOIN orders o
    ON o.user_id = u.id
WHERE o.id IS NULL;
```

## Count orders per customer

```sql
SELECT
    u.id,
    u.name,
    COUNT(o.id) AS total_orders
FROM users u
LEFT JOIN orders o
    ON o.user_id = u.id
GROUP BY
    u.id,
    u.name;
```

---

# 56. SQL Execution Order

Understanding SQL's logical processing order is important.

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
DISTINCT
  ↓
ORDER BY
  ↓
LIMIT
```

Example:

```sql
SELECT
    category_id,
    COUNT(*) AS total
FROM products
WHERE price > 100
GROUP BY category_id
HAVING COUNT(*) > 2
ORDER BY total DESC
LIMIT 10;
```

Conceptually:

```text
FROM products
↓
WHERE price > 100
↓
GROUP BY category_id
↓
HAVING COUNT(*) > 2
↓
SELECT
↓
ORDER BY
↓
LIMIT
```

---

# 57. NULL and COALESCE

`COALESCE()` returns the first non-NULL value.

```sql
SELECT
    name,
    COALESCE(email, 'No Email') AS email
FROM users;
```

Example:

```sql
SELECT
    product_name,
    COALESCE(stock, 0) AS stock
FROM products;
```

---

# 58. IF and IFNULL

## IF

```sql
SELECT
    name,
    IF(age >= 18, 'Adult', 'Minor') AS category
FROM students;
```

## IFNULL

```sql
SELECT
    name,
    IFNULL(email, 'No Email') AS email
FROM students;
```

---

# 59. UNION

Combine results from multiple queries.

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

The queries must have compatible numbers/types of columns.

---

# 60. EXISTS

Check whether a related record exists.

```sql
SELECT
    u.id,
    u.name
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.user_id = u.id
);
```

Find users without orders:

```sql
SELECT
    u.id,
    u.name
FROM users u
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.user_id = u.id
);
```

---

# 61. Foreign Key Actions

Example:

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,

    CONSTRAINT fk_orders_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

Common actions:

```text
CASCADE
SET NULL
RESTRICT
NO ACTION
```

Be careful with `ON DELETE CASCADE` because deleting a parent row can delete related rows automatically.

---

# 62. Composite Index

Example:

```sql
CREATE INDEX idx_orders_user_status
ON orders(user_id, status);
```

This can help queries such as:

```sql
SELECT *
FROM orders
WHERE user_id = 10
  AND status = 'pending';
```

Column order matters.

For example:

```sql
(user_id, status)
```

is not equivalent to:

```sql
(status, user_id)
```

for every workload.

Design indexes based on actual query patterns.

---

# 63. Unique Constraints

```sql
CREATE TABLE accounts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE
);
```

This prevents duplicate usernames and emails.

---

# 64. CHECK Constraints

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL,

    CHECK (price >= 0),
    CHECK (stock >= 0)
);
```

---

# 65. ALTER TABLE

Add column:

```sql
ALTER TABLE students
ADD COLUMN phone VARCHAR(30);
```

Modify column:

```sql
ALTER TABLE students
MODIFY COLUMN phone VARCHAR(50);
```

Rename column:

```sql
ALTER TABLE students
RENAME COLUMN phone TO phone_number;
```

Drop column:

```sql
ALTER TABLE students
DROP COLUMN phone_number;
```

Add index:

```sql
ALTER TABLE students
ADD INDEX idx_students_name (name);
```

---

# 66. Rename Table

```sql
RENAME TABLE students TO learners;
```

---

# 67. Database Metadata

Show tables:

```sql
SHOW TABLES;
```

Show table structure:

```sql
SHOW CREATE TABLE students;
```

Show indexes:

```sql
SHOW INDEX FROM students;
```

Show databases:

```sql
SHOW DATABASES;
```

---

# 68. SQL Comments

Single-line:

```sql
-- This is a comment
SELECT * FROM users;
```

Another style:

```sql
# This is also a comment
SELECT * FROM users;
```

Multi-line:

```sql
/*
    This is a
    multi-line comment
*/
SELECT * FROM users;
```

---

# 69. Naming Conventions

Recommended:

```text
snake_case
```

Good:

```text
user_id
created_at
order_items
product_categories
```

Avoid inconsistent naming:

```text
UserID
userId
USER_ID
```

A consistent convention is easier to maintain.

---

# 70. Recommended Project Structure

```text
mysql-project/
│
├── README.md
│
├── database/
│   ├── schema.sql
│   ├── seed.sql
│   ├── views.sql
│   ├── procedures.sql
│   ├── functions.sql
│   └── triggers.sql
│
├── migrations/
│   ├── 001_create_users.sql
│   ├── 002_create_products.sql
│   └── 003_create_orders.sql
│
├── backups/
│   └── .gitkeep
│
└── docs/
    └── database-design.md
```

---

# 71. Complete `schema.sql`

```sql
CREATE DATABASE IF NOT EXISTS ecommerce_db;

USE ecommerce_db;

CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE categories (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE products (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    category_id BIGINT UNSIGNED,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(12,2) NOT NULL,
    stock INT UNSIGNED NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_products_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id)
);

CREATE TABLE orders (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    status VARCHAR(30) NOT NULL DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
);

CREATE TABLE order_items (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    order_id BIGINT UNSIGNED NOT NULL,
    product_id BIGINT UNSIGNED NOT NULL,
    quantity INT UNSIGNED NOT NULL,
    price DECIMAL(12,2) NOT NULL,

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id),

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id)
);
```

---

# 72. Complete CRUD

CRUD means:

```text
C = Create
R = Read
U = Update
D = Delete
```

## CREATE

```sql
INSERT INTO users (name, email)
VALUES ('Dara', 'dara@example.com');
```

## READ

```sql
SELECT *
FROM users;
```

## UPDATE

```sql
UPDATE users
SET name = 'Dara Chan'
WHERE id = 1;
```

## DELETE

```sql
DELETE FROM users
WHERE id = 1;
```

---

# 73. Transaction-Based Order Creation

A real order operation can use a transaction.

```sql
START TRANSACTION;

INSERT INTO orders (user_id, status)
VALUES (1, 'pending');

SET @order_id = LAST_INSERT_ID();

INSERT INTO order_items (
    order_id,
    product_id,
    quantity,
    price
)
SELECT
    @order_id,
    id,
    2,
    price
FROM products
WHERE id = 1;

UPDATE products
SET stock = stock - 2
WHERE id = 1
  AND stock >= 2;

COMMIT;
```

In production code, you should also verify that the stock update affected the expected number of rows and roll back if the operation cannot be completed safely.

---

# 74. ACID

Transactions are commonly discussed using **ACID**.

```text
A = Atomicity
C = Consistency
I = Isolation
D = Durability
```

## Atomicity

Everything succeeds or the transaction is rolled back.

## Consistency

Database rules remain valid.

## Isolation

Concurrent transactions should not incorrectly interfere with each other.

## Durability

Committed data should survive normal system failures.

**Khmer**

ACID ជាគោលការណ៍សំខាន់សម្រាប់ Transaction ក្នុង Database។

---

# 75. Transaction Isolation

Common isolation levels include:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Check:

```sql
SELECT @@transaction_isolation;
```

Set for the current session:

```sql
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

Use isolation levels carefully because stronger isolation can reduce concurrency.

---

# 76. Locking

Example row lock:

```sql
START TRANSACTION;

SELECT *
FROM products
WHERE id = 1
FOR UPDATE;

UPDATE products
SET stock = stock - 1
WHERE id = 1;

COMMIT;
```

`FOR UPDATE` can lock selected rows during the transaction when supported by the storage engine and transaction context.

---

# 77. Deadlocks

A deadlock occurs when transactions wait for each other.

Example concept:

```text
Transaction A
    ↓
locks Row 1
    ↓
waits for Row 2

Transaction B
    ↓
locks Row 2
    ↓
waits for Row 1
```

Best practices:

```text
✓ Keep transactions short
✓ Access tables/rows in a consistent order
✓ Update only what is necessary
✓ Handle deadlock errors by retrying safely
```

---

# 78. Pagination with Search and Sorting

Example:

```sql
SELECT
    id,
    name,
    price
FROM products
WHERE name LIKE '%laptop%'
ORDER BY price DESC
LIMIT 20 OFFSET 0;
```

Important:

Do not allow arbitrary user input to become SQL identifiers such as:

```text
ORDER BY <user_input>
```

Whitelist allowed sort columns in application code.

---

# 79. Reporting Query

Monthly sales:

```sql
SELECT
    YEAR(o.created_at) AS year,
    MONTH(o.created_at) AS month,
    SUM(oi.quantity * oi.price) AS revenue
FROM orders o
JOIN order_items oi
    ON oi.order_id = o.id
WHERE o.status = 'completed'
GROUP BY
    YEAR(o.created_at),
    MONTH(o.created_at)
ORDER BY
    year,
    month;
```

---

# 80. Top Products

```sql
SELECT
    p.id,
    p.name,
    SUM(oi.quantity) AS total_sold,
    SUM(oi.quantity * oi.price) AS revenue
FROM products p
JOIN order_items oi
    ON oi.product_id = p.id
JOIN orders o
    ON o.id = oi.order_id
WHERE o.status = 'completed'
GROUP BY
    p.id,
    p.name
ORDER BY
    total_sold DESC
LIMIT 10;
```

---

# 81. Monthly Customer Ranking

```sql
WITH customer_sales AS (
    SELECT
        u.id,
        u.name,
        SUM(oi.quantity * oi.price) AS total_spent
    FROM users u
    JOIN orders o
        ON o.user_id = u.id
    JOIN order_items oi
        ON oi.order_id = o.id
    WHERE o.status = 'completed'
    GROUP BY
        u.id,
        u.name
)
SELECT
    id,
    name,
    total_spent,
    RANK() OVER (
        ORDER BY total_spent DESC
    ) AS customer_rank
FROM customer_sales;
```

---

# 82. Database Design Checklist

Before creating a database:

```text
□ Identify entities
□ Identify relationships
□ Define primary keys
□ Define foreign keys
□ Choose appropriate data types
□ Add required constraints
□ Normalize where appropriate
□ Identify common queries
□ Add indexes based on workload
□ Plan backup strategy
□ Plan security
□ Plan migrations
```

---

# 83. MySQL Best Practices

## Database

```text
✓ Use meaningful table names
✓ Use consistent naming conventions
✓ Use primary keys
✓ Use foreign keys
✓ Use appropriate data types
✓ Avoid unnecessary duplication
```

## Queries

```text
✓ Avoid SELECT *
✓ Use WHERE carefully
✓ Use parameterized queries
✓ Use indexes appropriately
✓ Check slow queries with EXPLAIN
✓ Avoid unnecessary JOINs
```

## Security

```text
✓ Never expose database passwords
✓ Never commit .env
✓ Do not use root in applications
✓ Use least privilege
✓ Use prepared statements
✓ Keep MySQL updated
```

## Production

```text
✓ Backups
✓ Monitoring
✓ Logging
✓ Disaster recovery
✓ Migration strategy
✓ Index review
✓ Query optimization
```

---

# 84. Common Mistakes

## Mistake 1 — Forgetting WHERE

Bad:

```sql
UPDATE users
SET name = 'Dara';
```

This updates every user.

Correct:

```sql
UPDATE users
SET name = 'Dara'
WHERE id = 1;
```

---

## Mistake 2 — Using `= NULL`

Bad:

```sql
SELECT *
FROM users
WHERE email = NULL;
```

Correct:

```sql
SELECT *
FROM users
WHERE email IS NULL;
```

---

## Mistake 3 — SQL Injection

Bad:

```text
SELECT * FROM users WHERE email = 'USER_INPUT';
```

when constructed unsafely through string concatenation.

Use parameterized queries.

---

## Mistake 4 — Too Many Indexes

More indexes do not automatically mean better performance.

Indexes have storage and write-maintenance costs.

---

## Mistake 5 — Using Wrong Data Type

For monetary values, prefer:

```sql
DECIMAL(12,2)
```

instead of relying on floating-point types for exact currency representation.

---

# 85. MySQL Cheat Sheet

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
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100)
);

SHOW TABLES;

DESCRIBE table_name;

DROP TABLE table_name;

TRUNCATE TABLE table_name;
```

## CRUD

```sql
INSERT INTO table_name (name)
VALUES ('Dara');
```

```sql
SELECT *
FROM table_name;
```

```sql
UPDATE table_name
SET name = 'Sokha'
WHERE id = 1;
```

```sql
DELETE FROM table_name
WHERE id = 1;
```

## Filtering

```sql
WHERE
AND
OR
NOT
IN
NOT IN
BETWEEN
LIKE
IS NULL
IS NOT NULL
```

## Sorting

```sql
ORDER BY column ASC;
```

```sql
ORDER BY column DESC;
```

## Aggregation

```sql
COUNT()
SUM()
AVG()
MIN()
MAX()
```

## Grouping

```sql
GROUP BY
HAVING
```

## Joins

```sql
INNER JOIN
LEFT JOIN
RIGHT JOIN
CROSS JOIN
```

## Advanced

```sql
WITH
WITH RECURSIVE
OVER()
PARTITION BY
ROW_NUMBER()
RANK()
DENSE_RANK()
CASE
EXISTS
UNION
UNION ALL
```

---

# 86. Beginner → Advanced Learning Path

## 🟢 Beginner

Learn:

```text
1. What is MySQL?
2. Database
3. Table
4. Rows
5. Columns
6. Data types
7. CREATE
8. INSERT
9. SELECT
10. WHERE
11. UPDATE
12. DELETE
```

---

## 🟡 Intermediate

Learn:

```text
13. ORDER BY
14. LIMIT
15. DISTINCT
16. LIKE
17. IN
18. BETWEEN
19. NULL
20. Aggregate functions
21. GROUP BY
22. HAVING
23. Constraints
24. Primary Keys
25. Foreign Keys
26. Relationships
27. JOIN
28. Subqueries
29. CASE
30. Functions
```

---

## 🔴 Advanced

Learn:

```text
31. Views
32. Indexes
33. Transactions
34. ACID
35. Isolation
36. Locks
37. Stored Procedures
38. Stored Functions
39. Triggers
40. CTE
41. Recursive CTE
42. Window Functions
43. JSON
44. User Management
45. Permissions
46. Backup
47. EXPLAIN
48. Query Optimization
49. Normalization
50. Database Architecture
51. Security
52. Production Database Design
```

---

# 87. Recommended MySQL Project Progression

Practice with projects in this order:

### Project 1 — Student Management

```text
students
teachers
courses
```

Practice:

```text
CRUD
WHERE
ORDER BY
GROUP BY
JOIN
```

### Project 2 — Library Management

```text
books
authors
members
borrowings
```

Practice:

```text
Relationships
Foreign Keys
JOIN
Transactions
```

### Project 3 — Inventory Management

```text
products
categories
suppliers
stock_movements
```

Practice:

```text
Indexes
Transactions
Reports
Views
```

### Project 4 — E-Commerce

```text
users
products
categories
orders
order_items
payments
```

Practice:

```text
Advanced JOIN
Transactions
Indexes
CTEs
Window Functions
Reporting
```

### Project 5 — Production System

Practice:

```text
Database design
Normalization
Migrations
Security
Backups
Monitoring
Optimization
High-volume queries
```

---

# 88. Final MySQL Architecture

A typical application architecture:

```text
                 ┌──────────────┐
                 │   Frontend   │
                 │ React / Vue  │
                 │ Angular      │
                 └──────┬───────┘
                        │
                        │ HTTP
                        ▼
                 ┌──────────────┐
                 │     API      │
                 │ Node / Java  │
                 │ Python / Go  │
                 └──────┬───────┘
                        │
                        │ SQL
                        ▼
                 ┌──────────────┐
                 │    MySQL     │
                 │              │
                 │ ┌──────────┐ │
                 │ │ Tables   │ │
                 │ │ Indexes  │ │
                 │ │ Views    │ │
                 │ │ Triggers │ │
                 │ └──────────┘ │
                 └──────────────┘
```

---

# 89. Final Summary

MySQL learning progression:

```text
SQL Basics
    ↓
CRUD
    ↓
Filtering
    ↓
Sorting
    ↓
Aggregation
    ↓
Relationships
    ↓
JOIN
    ↓
Subqueries
    ↓
Constraints
    ↓
Indexes
    ↓
Transactions
    ↓
Views
    ↓
Procedures
    ↓
Functions
    ↓
Triggers
    ↓
CTEs
    ↓
Window Functions
    ↓
JSON
    ↓
Security
    ↓
EXPLAIN
    ↓
Optimization
    ↓
Production Database Design
```

## The most important things to master

```text
1. SELECT
2. INSERT
3. UPDATE
4. DELETE
5. WHERE
6. JOIN
7. GROUP BY
8. HAVING
9. Subqueries
10. Constraints
11. Indexes
12. Transactions
13. CTE
14. Window Functions
15. Database Design
16. Security
17. Query Optimization
```

---

# ⭐ Quick Reference

```sql
-- Create database
CREATE DATABASE app_db;

-- Use database
USE app_db;

-- Create table
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE
);

-- Insert
INSERT INTO users (name, email)
VALUES ('Dara', 'dara@example.com');

-- Read
SELECT *
FROM users;

-- Filter
SELECT *
FROM users
WHERE id = 1;

-- Update
UPDATE users
SET name = 'Dara Chan'
WHERE id = 1;

-- Delete
DELETE FROM users
WHERE id = 1;

-- Join
SELECT
    u.name,
    o.id AS order_id
FROM users u
JOIN orders o
    ON o.user_id = u.id;

-- Group
SELECT
    user_id,
    COUNT(*) AS total
FROM orders
GROUP BY user_id;

-- Transaction
START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;

-- Explain
EXPLAIN
SELECT *
FROM users
WHERE email = 'dara@example.com';
```

---

# 📖 Conclusion

MySQL is much more than basic CRUD.

A professional MySQL developer should understand:

```text
SQL
+
Data Modeling
+
Relationships
+
Indexes
+
Transactions
+
Security
+
Optimization
+
Backup
+
Production Design
```

**English:** Learn the basics first, then practice by building real projects.

**Khmer:** រៀនពីមូលដ្ឋានជាមុន បន្ទាប់មកអនុវត្តដោយបង្កើត Project ពិតៗ។ កុំរៀន SQL ត្រឹមតែចាំ Syntax — ត្រូវយល់ពី **Database Design, Relationships, Transactions, Indexes, Security និង Performance** ផងដែរ។

---

## 🚀 Keep Learning

```text
Beginner
   ↓
CRUD
   ↓
JOIN
   ↓
Database Design
   ↓
Transactions
   ↓
Indexes
   ↓
Advanced SQL
   ↓
Optimization
   ↓
Production
```

**Happy Coding! 🐬💻**
