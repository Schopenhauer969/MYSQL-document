# MySQL — Beginner to Advanced

A complete **MySQL learning guide from beginner to advanced**, including SQL syntax, database design, relationships, joins, indexes, transactions, stored procedures, functions, triggers, views, CTEs, JSON, optimization, security, backup, and real-world projects.

> **Language:** English + Khmer
> **Level:** Beginner → Intermediate → Advanced
> **Database:** MySQL 8.x

---

## Table of Contents

1. [What is MySQL?](#1-what-is-mysql)
2. [Install MySQL](#2-install-mysql)
3. [Connect to MySQL](#3-connect-to-mysql)
4. [MySQL Concepts](#4-mysql-concepts)
5. [Create Database](#5-create-database)
6. [Create Table](#6-create-table)
7. [MySQL Data Types](#7-mysql-data-types)
8. [Insert Data](#8-insert-data)
9. [Select Data](#9-select-data)
10. [Where](#10-where)
11. [Order By](#11-order-by)
12. [Limit](#12-limit)
13. [Update](#13-update)
14. [Delete](#14-delete)
15. [NULL](#15-null)
16. [Constraints](#16-constraints)
17. [Primary Key](#17-primary-key)
18. [Foreign Key](#18-foreign-key)
19. [Relationships](#19-relationships)
20. [Joins](#20-joins)
21. [Aggregate Functions](#21-aggregate-functions)
22. [Group By](#22-group-by)
23. [Having](#23-having)
24. [String Functions](#24-string-functions)
25. [Date and Time](#25-date-and-time)
26. [CASE](#26-case)
27. [Subqueries](#27-subqueries)
28. [Common Table Expressions](#28-common-table-expressions)
29. [Views](#29-views)
30. [Indexes](#30-indexes)
31. [Transactions](#31-transactions)
32. [Stored Procedures](#32-stored-procedures)
33. [Stored Functions](#33-stored-functions)
34. [Triggers](#34-triggers)
35. [Events](#35-events)
36. [Window Functions](#36-window-functions)
37. [JSON](#37-json)
38. [Recursive CTE](#38-recursive-cte)
39. [Query Optimization](#39-query-optimization)
40. [EXPLAIN](#40-explain)
41. [Database Normalization](#41-database-normalization)
42. [Users and Privileges](#42-users-and-privileges)
43. [Security](#43-security)
44. [Backup and Restore](#44-backup-and-restore)
45. [Database Design](#45-database-design)
46. [Advanced Queries](#46-advanced-queries)
47. [Best Practices](#47-best-practices)
48. [SQL Cheat Sheet](#48-sql-cheat-sheet)
49. [Learning Path](#49-learning-path)
50. [MySQL Mental Model](#50-mysql-mental-model)
51. [Real-World Architecture](#51-real-world-architecture)
52. [Production Checklist](#52-production-checklist)
53. [Environment Variables](#53-environment-variables)
54. [Project Structure](#54-project-structure)
55. [Complete E-Commerce Example](#55-complete-e-commerce-example)
56. [Final Roadmap](#56-final-roadmap)
57. [Practice Projects](#57-practice-projects)
58. [Conclusion](#58-conclusion)

---

# 1. What is MySQL?

## English

**MySQL** is an open-source relational database management system.

It stores data inside tables using rows and columns and uses **SQL (Structured Query Language)** to manage that data.

## Khmer

**MySQL** គឺជា Database Management System ប្រភេទ Relational Database ដែលប្រើសម្រាប់រក្សាទុក និងគ្រប់គ្រងទិន្នន័យ។

MySQL ប្រើ **SQL** ដើម្បី:

* Create database
* Create tables
* Insert data
* Read data
* Update data
* Delete data
* Manage relationships
* Manage users
* Optimize queries

---

# 2. Install MySQL

## Windows

Download and install MySQL Server and MySQL Workbench.

After installation:

```bash
mysql --version
```

Example:

```text
mysql  Ver 8.0.xx for Win64
```

## Linux Ubuntu

```bash
sudo apt update
sudo apt install mysql-server
```

Start MySQL:

```bash
sudo systemctl start mysql
```

Enable MySQL:

```bash
sudo systemctl enable mysql
```

Check status:

```bash
sudo systemctl status mysql
```

## macOS

Using Homebrew:

```bash
brew install mysql
```

Start:

```bash
brew services start mysql
```

Check:

```bash
mysql --version
```

---

# 3. Connect to MySQL

```bash
mysql -u root -p
```

Enter your password.

You can also specify a host:

```bash
mysql -h localhost -u root -p
```

Specify a database:

```bash
mysql -u root -p my_database
```

Exit:

```sql
EXIT;
```

or:

```sql
QUIT;
```

---

# 4. MySQL Concepts

A relational database contains:

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
Database: shop

users
--------------------------------
id | name | email
--------------------------------
1  | John | john@gmail.com
2  | Anna | anna@gmail.com
```

## Khmer

* **Database** = កន្លែងផ្ទុក Tables
* **Table** = តារាងទិន្នន័យ
* **Row** = ទិន្នន័យមួយ record
* **Column** = Field / Attribute

---

# 5. Create Database

Create:

```sql
CREATE DATABASE shop;
```

Create only if it does not exist:

```sql
CREATE DATABASE IF NOT EXISTS shop;
```

Show databases:

```sql
SHOW DATABASES;
```

Use database:

```sql
USE shop;
```

Delete database:

```sql
DROP DATABASE shop;
```

> Be careful: `DROP DATABASE` permanently removes the database.

---

# 6. Create Table

Example:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Show tables:

```sql
SHOW TABLES;
```

Describe table:

```sql
DESCRIBE users;
```

Alternative:

```sql
DESC users;
```

---

# 7. MySQL Data Types

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
```

For money, prefer:

```sql
DECIMAL(10,2)
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
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
```

## Boolean

MySQL supports:

```sql
BOOLEAN
```

It is effectively stored as a numeric type:

```sql
is_active BOOLEAN DEFAULT TRUE
```

---

# 8. Insert Data

Insert one row:

```sql
INSERT INTO users (name, email, age)
VALUES ('John', 'john@gmail.com', 25);
```

Insert multiple rows:

```sql
INSERT INTO users (name, email, age)
VALUES
    ('John', 'john@gmail.com', 25),
    ('Anna', 'anna@gmail.com', 22),
    ('David', 'david@gmail.com', 30);
```

Insert without specifying the auto-increment ID:

```sql
INSERT INTO users (name, email)
VALUES ('Dara', 'dara@gmail.com');
```

---

# 9. Select Data

Select everything:

```sql
SELECT *
FROM users;
```

Select specific columns:

```sql
SELECT id, name, email
FROM users;
```

Alias:

```sql
SELECT
    name AS username,
    email AS user_email
FROM users;
```

Distinct:

```sql
SELECT DISTINCT age
FROM users;
```

---

# 10. WHERE

Find users older than 20:

```sql
SELECT *
FROM users
WHERE age > 20;
```

Equal:

```sql
SELECT *
FROM users
WHERE age = 25;
```

Not equal:

```sql
SELECT *
FROM users
WHERE age <> 25;
```

Multiple conditions:

```sql
SELECT *
FROM users
WHERE age >= 18
AND age <= 30;
```

OR:

```sql
SELECT *
FROM users
WHERE age = 20
OR age = 25;
```

IN:

```sql
SELECT *
FROM users
WHERE age IN (20, 25, 30);
```

BETWEEN:

```sql
SELECT *
FROM users
WHERE age BETWEEN 20 AND 30;
```

LIKE:

```sql
SELECT *
FROM users
WHERE name LIKE 'J%';
```

Starts with J:

```text
John
James
Jason
```

Ends with n:

```sql
SELECT *
FROM users
WHERE name LIKE '%n';
```

Contains "oh":

```sql
SELECT *
FROM users
WHERE name LIKE '%oh%';
```

---

# 11. ORDER BY

Ascending:

```sql
SELECT *
FROM users
ORDER BY age ASC;
```

Descending:

```sql
SELECT *
FROM users
ORDER BY age DESC;
```

Multiple columns:

```sql
SELECT *
FROM users
ORDER BY age DESC, name ASC;
```

---

# 12. LIMIT

Get first 10 records:

```sql
SELECT *
FROM users
LIMIT 10;
```

Pagination:

```sql
SELECT *
FROM users
LIMIT 10 OFFSET 20;
```

Equivalent:

```sql
SELECT *
FROM users
LIMIT 20, 10;
```

Meaning:

```text
Skip 20
Take 10
```

---

# 13. Update

Update one record:

```sql
UPDATE users
SET age = 26
WHERE id = 1;
```

Update multiple columns:

```sql
UPDATE users
SET
    name = 'John Doe',
    age = 27
WHERE id = 1;
```

Update multiple records:

```sql
UPDATE users
SET age = age + 1
WHERE age >= 18;
```

> Always be careful with `UPDATE` without `WHERE`.

---

# 14. Delete

Delete one record:

```sql
DELETE FROM users
WHERE id = 1;
```

Delete records:

```sql
DELETE FROM users
WHERE age < 18;
```

Delete all rows:

```sql
DELETE FROM users;
```

Remove table:

```sql
DROP TABLE users;
```

Remove all rows quickly:

```sql
TRUNCATE TABLE users;
```

### Difference

```text
DELETE
→ Removes rows
→ Can use WHERE

TRUNCATE
→ Removes all rows
→ Faster for clearing a table

DROP
→ Removes the entire table
```

---

# 15. NULL

Find NULL:

```sql
SELECT *
FROM users
WHERE age IS NULL;
```

Find NOT NULL:

```sql
SELECT *
FROM users
WHERE age IS NOT NULL;
```

Wrong:

```sql
WHERE age = NULL
```

Correct:

```sql
WHERE age IS NULL
```

Use `COALESCE`:

```sql
SELECT
    name,
    COALESCE(age, 0) AS age
FROM users;
```

---

# 16. Constraints

Constraints protect data integrity.

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
    id INT AUTO_INCREMENT PRIMARY KEY,

    username VARCHAR(50) NOT NULL UNIQUE,

    age INT CHECK (age >= 0),

    is_active BOOLEAN DEFAULT TRUE
);
```

---

# 17. Primary Key

A primary key uniquely identifies a row.

Example:

```sql
CREATE TABLE products (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(150) NOT NULL,
    price DECIMAL(10,2) NOT NULL
);
```

Primary key properties:

```text
Unique
Not NULL
Identifies one row
```

---

# 18. Foreign Key

A foreign key creates a relationship between tables.

Parent table:

```sql
CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

Child table:

```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    category_id INT,

    CONSTRAINT fk_product_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id)
);
```

Insert:

```sql
INSERT INTO categories (name)
VALUES
    ('Laptop'),
    ('Phone');
```

Insert product:

```sql
INSERT INTO products (name, category_id)
VALUES
    ('MacBook', 1),
    ('iPhone', 2);
```

---

# 19. Relationships

## One-to-One

```text
User
  |
  | 1
  |
  | 1
Profile
```

## One-to-Many

```text
Category
   |
   | 1
   |
   | N
Products
```

One category can have many products.

## Many-to-Many

Example:

```text
Students
   |
   |
student_courses
   |
   |
Courses
```

Junction table:

```sql
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

# 20. Joins

## INNER JOIN

Returns matching records.

```sql
SELECT
    products.id,
    products.name,
    categories.name AS category
FROM products
INNER JOIN categories
    ON products.category_id = categories.id;
```

## LEFT JOIN

Returns all rows from the left table.

```sql
SELECT
    categories.name,
    products.name
FROM categories
LEFT JOIN products
    ON products.category_id = categories.id;
```

## RIGHT JOIN

```sql
SELECT
    categories.name,
    products.name
FROM products
RIGHT JOIN categories
    ON products.category_id = categories.id;
```

## CROSS JOIN

Creates a Cartesian product.

```sql
SELECT
    users.name,
    categories.name
FROM users
CROSS JOIN categories;
```

## Self JOIN

Example employee hierarchy:

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    manager_id INT NULL,

    FOREIGN KEY (manager_id)
        REFERENCES employees(id)
);
```

Query:

```sql
SELECT
    employee.name AS employee,
    manager.name AS manager
FROM employees employee
LEFT JOIN employees manager
    ON employee.manager_id = manager.id;
```

---

# 21. Aggregate Functions

Common aggregate functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Count:

```sql
SELECT COUNT(*) AS total_users
FROM users;
```

Sum:

```sql
SELECT SUM(price) AS total_price
FROM products;
```

Average:

```sql
SELECT AVG(price) AS average_price
FROM products;
```

Minimum:

```sql
SELECT MIN(price)
FROM products;
```

Maximum:

```sql
SELECT MAX(price)
FROM products;
```

Multiple:

```sql
SELECT
    COUNT(*) AS total_products,
    SUM(price) AS total_price,
    AVG(price) AS average_price,
    MIN(price) AS cheapest,
    MAX(price) AS most_expensive
FROM products;
```

---

# 22. GROUP BY

Group products by category:

```sql
SELECT
    category_id,
    COUNT(*) AS total_products
FROM products
GROUP BY category_id;
```

With SUM:

```sql
SELECT
    category_id,
    SUM(price) AS total_price
FROM products
GROUP BY category_id;
```

With JOIN:

```sql
SELECT
    categories.name,
    COUNT(products.id) AS total_products
FROM categories
LEFT JOIN products
    ON products.category_id = categories.id
GROUP BY categories.id, categories.name;
```

---

# 23. HAVING

`WHERE` filters rows.

`HAVING` filters groups.

Example:

```sql
SELECT
    category_id,
    COUNT(*) AS total_products
FROM products
GROUP BY category_id
HAVING COUNT(*) > 5;
```

Combined:

```sql
SELECT
    category_id,
    AVG(price) AS average_price
FROM products
WHERE price > 10
GROUP BY category_id
HAVING AVG(price) > 100;
```

---

# 24. String Functions

Uppercase:

```sql
SELECT UPPER(name)
FROM users;
```

Lowercase:

```sql
SELECT LOWER(name)
FROM users;
```

Length:

```sql
SELECT
    name,
    LENGTH(name) AS name_length
FROM users;
```

Concatenate:

```sql
SELECT
    CONCAT(name, ' - ', email) AS user_info
FROM users;
```

Trim:

```sql
SELECT TRIM(name)
FROM users;
```

Replace:

```sql
SELECT REPLACE(name, 'John', 'Johnny')
FROM users;
```

Substring:

```sql
SELECT SUBSTRING(name, 1, 3)
FROM users;
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

Current date and time:

```sql
SELECT NOW();
```

Insert timestamp:

```sql
INSERT INTO users (
    name,
    email,
    created_at
)
VALUES (
    'John',
    'john@gmail.com',
    NOW()
);
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

Date difference:

```sql
SELECT
    DATEDIFF(CURDATE(), created_at) AS days_old
FROM users;
```

Add days:

```sql
SELECT DATE_ADD(NOW(), INTERVAL 7 DAY);
```

Subtract days:

```sql
SELECT DATE_SUB(NOW(), INTERVAL 7 DAY);
```

---

# 26. CASE

Simple CASE:

```sql
SELECT
    name,
    age,
    CASE
        WHEN age < 18 THEN 'Minor'
        WHEN age >= 18 AND age < 60 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM users;
```

Product price classification:

```sql
SELECT
    name,
    price,
    CASE
        WHEN price < 50 THEN 'Cheap'
        WHEN price < 500 THEN 'Medium'
        ELSE 'Expensive'
    END AS price_category
FROM products;
```

---

# 27. Subqueries

Find products more expensive than average:

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

Subquery with `IN`:

```sql
SELECT *
FROM products
WHERE category_id IN (
    SELECT id
    FROM categories
    WHERE name IN ('Laptop', 'Phone')
);
```

`EXISTS`:

```sql
SELECT *
FROM categories c
WHERE EXISTS (
    SELECT 1
    FROM products p
    WHERE p.category_id = c.id
);
```

---

# 28. Common Table Expressions

A CTE makes complex queries easier to read.

```sql
WITH expensive_products AS (
    SELECT *
    FROM products
    WHERE price > 500
)
SELECT *
FROM expensive_products;
```

Multiple CTEs:

```sql
WITH
product_stats AS (
    SELECT
        category_id,
        COUNT(*) AS total_products,
        AVG(price) AS average_price
    FROM products
    GROUP BY category_id
),
expensive_categories AS (
    SELECT *
    FROM product_stats
    WHERE average_price > 500
)
SELECT *
FROM expensive_categories;
```

---

# 29. Views

A view is a saved query.

Create:

```sql
CREATE VIEW product_category_view AS
SELECT
    products.id,
    products.name AS product_name,
    products.price,
    categories.name AS category_name
FROM products
INNER JOIN categories
    ON products.category_id = categories.id;
```

Use:

```sql
SELECT *
FROM product_category_view;
```

Drop:

```sql
DROP VIEW product_category_view;
```

---

# 30. Indexes

Indexes improve search performance.

Create:

```sql
CREATE INDEX idx_users_email
ON users(email);
```

Multiple-column index:

```sql
CREATE INDEX idx_products_category_price
ON products(category_id, price);
```

Unique index:

```sql
CREATE UNIQUE INDEX idx_users_username
ON users(username);
```

Show indexes:

```sql
SHOW INDEX FROM users;
```

Drop:

```sql
DROP INDEX idx_users_email
ON users;
```

## Important

Indexes improve reads but can increase:

```text
INSERT cost
UPDATE cost
DELETE cost
Storage usage
```

Do not create indexes on every column.

---

# 31. Transactions

Transactions allow multiple operations to behave as one unit.

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

Rollback:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

ROLLBACK;
```

## ACID

```text
A = Atomicity
C = Consistency
I = Isolation
D = Durability
```

---

# 32. Stored Procedures

Create:

```sql
DELIMITER //

CREATE PROCEDURE GetUsers()
BEGIN
    SELECT *
    FROM users;
END //

DELIMITER ;
```

Call:

```sql
CALL GetUsers();
```

Procedure with parameter:

```sql
DELIMITER //

CREATE PROCEDURE GetUserById(
    IN user_id INT
)
BEGIN
    SELECT *
    FROM users
    WHERE id = user_id;
END //

DELIMITER ;
```

Call:

```sql
CALL GetUserById(1);
```

Drop:

```sql
DROP PROCEDURE GetUsers;
```

---

# 33. Stored Functions

Create:

```sql
DELIMITER //

CREATE FUNCTION AddNumbers(
    a INT,
    b INT
)
RETURNS INT
DETERMINISTIC
BEGIN
    RETURN a + b;
END //

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

# 34. Triggers

Triggers execute automatically when an event occurs.

Example audit table:

```sql
CREATE TABLE user_logs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    action VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Create trigger:

```sql
DELIMITER //

CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO user_logs (
        user_id,
        action
    )
    VALUES (
        NEW.id,
        'INSERT'
    );
END //

DELIMITER ;
```

Insert:

```sql
INSERT INTO users (
    name,
    email,
    age
)
VALUES (
    'Test User',
    'test@gmail.com',
    25
);
```

Check:

```sql
SELECT *
FROM user_logs;
```

---

# 35. Events

Events allow scheduled SQL operations.

Enable scheduler:

```sql
SET GLOBAL event_scheduler = ON;
```

Create event:

```sql
CREATE EVENT delete_old_logs
ON SCHEDULE EVERY 1 DAY
DO
    DELETE FROM user_logs
    WHERE created_at < NOW() - INTERVAL 30 DAY;
```

Show events:

```sql
SHOW EVENTS;
```

Drop:

```sql
DROP EVENT delete_old_logs;
```

---

# 36. Window Functions

Window functions calculate values across related rows without grouping them into one row.

Example:

```sql
SELECT
    id,
    name,
    price,
    AVG(price) OVER () AS average_price
FROM products;
```

Ranking:

```sql
SELECT
    id,
    name,
    price,
    RANK() OVER (
        ORDER BY price DESC
    ) AS price_rank
FROM products;
```

Row number:

```sql
SELECT
    id,
    name,
    price,
    ROW_NUMBER() OVER (
        ORDER BY price DESC
    ) AS row_number
FROM products;
```

Partition:

```sql
SELECT
    id,
    name,
    category_id,
    price,
    RANK() OVER (
        PARTITION BY category_id
        ORDER BY price DESC
    ) AS category_rank
FROM products;
```

---

# 37. JSON

Create JSON column:

```sql
CREATE TABLE products_json (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    attributes JSON
);
```

Insert:

```sql
INSERT INTO products_json (
    name,
    attributes
)
VALUES (
    'Laptop',
    '{"brand":"Apple","ram":16,"storage":512}'
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
    attributes->>'$.brand' AS brand
FROM products_json;
```

Extract RAM:

```sql
SELECT
    attributes->>'$.ram' AS ram
FROM products_json;
```

Search JSON:

```sql
SELECT *
FROM products_json
WHERE JSON_EXTRACT(attributes, '$.ram') = 16;
```

---

# 38. Recursive CTE

Recursive CTEs are useful for hierarchical data.

Example:

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    manager_id INT NULL,

    FOREIGN KEY (manager_id)
        REFERENCES employees(id)
);
```

Insert:

```sql
INSERT INTO employees (name, manager_id)
VALUES
    ('CEO', NULL),
    ('Manager A', 1),
    ('Manager B', 1),
    ('Developer A', 2),
    ('Developer B', 2),
    ('Developer C', 3);
```

Recursive query:

```sql
WITH RECURSIVE employee_tree AS (

    SELECT
        id,
        name,
        manager_id,
        0 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT
        e.id,
        e.name,
        e.manager_id,
        et.level + 1
    FROM employees e
    INNER JOIN employee_tree et
        ON e.manager_id = et.id
)

SELECT *
FROM employee_tree
ORDER BY level, id;
```

---

# 39. Query Optimization

Bad:

```sql
SELECT *
FROM users;
```

Better:

```sql
SELECT id, name, email
FROM users;
```

Bad:

```sql
SELECT *
FROM users
WHERE LOWER(email) = 'john@gmail.com';
```

Better:

```sql
SELECT id, name, email
FROM users
WHERE email = 'john@gmail.com';
```

Create an index:

```sql
CREATE INDEX idx_users_email
ON users(email);
```

## Avoid unnecessary operations

Avoid:

```sql
SELECT *
```

Prefer:

```sql
SELECT id, name, email
```

Use pagination:

```sql
SELECT id, name
FROM users
ORDER BY id
LIMIT 20 OFFSET 0;
```

For large datasets, keyset pagination can be better:

```sql
SELECT id, name
FROM users
WHERE id > 1000
ORDER BY id
LIMIT 20;
```

---

# 40. EXPLAIN

Use `EXPLAIN` to understand query execution.

```sql
EXPLAIN
SELECT *
FROM users
WHERE email = 'john@gmail.com';
```

For actual execution analysis:

```sql
EXPLAIN ANALYZE
SELECT *
FROM users
WHERE email = 'john@gmail.com';
```

Check:

```text
type
possible_keys
key
rows
Extra
```

A good index can change a query from scanning many rows to finding matching rows efficiently.

---

# 41. Database Normalization

Normalization reduces duplicated data.

## First Normal Form — 1NF

Each column should contain atomic values.

Bad:

```text
id | name | phones
1  | John | 123,456,789
```

Better:

```text
users
id | name

user_phones
id | user_id | phone
```

## Second Normal Form — 2NF

Every non-key column should depend on the whole primary key.

## Third Normal Form — 3NF

Non-key columns should not depend on other non-key columns.

Example:

Bad:

```text
user_id
user_name
department_id
department_name
```

Better:

```text
users
departments
```

---

# 42. Users and Privileges

Create user:

```sql
CREATE USER 'app_user'@'localhost'
IDENTIFIED BY 'StrongPassword_123!';
```

Grant privileges:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON shop.*
TO 'app_user'@'localhost';
```

Show grants:

```sql
SHOW GRANTS
FOR 'app_user'@'localhost';
```

Remove privilege:

```sql
REVOKE DELETE
ON shop.*
FROM 'app_user'@'localhost';
```

Drop user:

```sql
DROP USER 'app_user'@'localhost';
```

---

# 43. Security

## Never store passwords as plain text

Bad:

```text
password = "123456"
```

Application passwords should be hashed using a password hashing algorithm such as:

```text
Argon2id
bcrypt
scrypt
```

## Use prepared statements

Bad:

```text
SELECT * FROM users WHERE email = '" + email + "'
```

This can lead to SQL injection.

Better:

```sql
SELECT *
FROM users
WHERE email = ?;
```

Application code should bind the value separately.

## Principle of Least Privilege

Do not give application users:

```text
ALL PRIVILEGES
```

unless there is a real reason.

Prefer:

```sql
GRANT SELECT, INSERT, UPDATE, DELETE
ON shop.*
TO 'app_user'@'localhost';
```

---

# 44. Backup and Restore

## Backup

Using `mysqldump`:

```bash
mysqldump -u root -p shop > shop_backup.sql
```

Backup all databases:

```bash
mysqldump -u root -p --all-databases > all_databases.sql
```

## Restore

```bash
mysql -u root -p shop < shop_backup.sql
```

If the database does not exist:

```bash
mysql -u root -p < shop_backup.sql
```

## Important

Production databases should have:

```text
Regular backups
Off-site backups
Backup testing
Retention policy
Recovery procedure
```

A backup that has never been restored/tested should not be assumed reliable.

---

# 45. Database Design

A good database design usually starts with requirements.

Example e-commerce system:

```text
Users
  |
  └── Orders
        |
        └── Order Items
                |
                └── Products
                        |
                        └── Categories
```

Possible tables:

```text
users
categories
products
orders
order_items
payments
addresses
```

---

# 46. Advanced Queries

## Top 5 Products

```sql
SELECT
    id,
    name,
    price
FROM products
ORDER BY price DESC
LIMIT 5;
```

## Products Above Average

```sql
SELECT *
FROM products
WHERE price > (
    SELECT AVG(price)
    FROM products
);
```

## Count Products Per Category

```sql
SELECT
    c.name,
    COUNT(p.id) AS total_products
FROM categories c
LEFT JOIN products p
    ON p.category_id = c.id
GROUP BY c.id, c.name;
```

## Highest Product Per Category

```sql
WITH ranked_products AS (
    SELECT
        p.*,
        RANK() OVER (
            PARTITION BY category_id
            ORDER BY price DESC
        ) AS product_rank
    FROM products p
)
SELECT *
FROM ranked_products
WHERE product_rank = 1;
```

## Duplicate Emails

```sql
SELECT
    email,
    COUNT(*) AS total
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

## Remove Duplicate Data Carefully

First identify duplicates:

```sql
SELECT
    email,
    COUNT(*) AS total
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

Never blindly delete duplicate rows in production. First determine which record should remain and whether related tables reference those rows.

---

# 47. Best Practices

## Naming

Use consistent names:

```text
users
products
orders
order_items
created_at
updated_at
```

Avoid:

```text
tblUser
tblProducts
Data1
TestTable
```

## Always use Primary Keys

```sql
id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY
```

## Use Foreign Keys

```sql
FOREIGN KEY (category_id)
REFERENCES categories(id)
```

## Use Transactions

For important multi-step operations:

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

## Index Carefully

Index columns frequently used in:

```text
WHERE
JOIN
ORDER BY
GROUP BY
```

But validate with real query workloads.

## Avoid SELECT *

Prefer:

```sql
SELECT
    id,
    name,
    email
FROM users;
```

---

# 48. SQL Cheat Sheet

## Database

```sql
CREATE DATABASE shop;

SHOW DATABASES;

USE shop;

DROP DATABASE shop;
```

## Table

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

SHOW TABLES;

DESCRIBE users;

DROP TABLE users;
```

## Insert

```sql
INSERT INTO users (name)
VALUES ('John');
```

## Select

```sql
SELECT *
FROM users;
```

## Filter

```sql
SELECT *
FROM users
WHERE id = 1;
```

## Update

```sql
UPDATE users
SET name = 'John Doe'
WHERE id = 1;
```

## Delete

```sql
DELETE FROM users
WHERE id = 1;
```

## Sort

```sql
SELECT *
FROM users
ORDER BY name ASC;
```

## Pagination

```sql
SELECT *
FROM users
ORDER BY id
LIMIT 20 OFFSET 0;
```

## Count

```sql
SELECT COUNT(*)
FROM users;
```

## Group

```sql
SELECT
    age,
    COUNT(*)
FROM users
GROUP BY age;
```

## Join

```sql
SELECT *
FROM users u
JOIN orders o
    ON o.user_id = u.id;
```

---

# 49. Learning Path

Recommended order:

```text
1. SQL Basics
       ↓
2. Database / Tables
       ↓
3. SELECT
       ↓
4. WHERE
       ↓
5. INSERT / UPDATE / DELETE
       ↓
6. Constraints
       ↓
7. Relationships
       ↓
8. JOIN
       ↓
9. GROUP BY / HAVING
       ↓
10. Subqueries
       ↓
11. CTE
       ↓
12. Views
       ↓
13. Indexes
       ↓
14. Transactions
       ↓
15. Stored Procedures
       ↓
16. Functions
       ↓
17. Triggers
       ↓
18. Window Functions
       ↓
19. JSON
       ↓
20. Optimization
       ↓
21. Security
       ↓
22. Production
```

---

# 50. MySQL Mental Model

Think about MySQL like this:

```text
Application
     |
     | SQL Query
     ↓
MySQL Server
     |
     ↓
Database
     |
     ↓
Tables
     |
     ↓
Rows + Columns
     |
     ↓
Indexes
     |
     ↓
Storage Engine
```

Example:

```text
Node.js / Java / Python / PHP
              |
              ↓
          SQL Query
              |
              ↓
          MySQL Server
              |
              ↓
          users table
```

---

# 51. Real-World Architecture

Typical web application:

```text
                Client
                  |
                  ↓
              Frontend
                  |
                  ↓
              REST API
                  |
                  ↓
             Backend App
                  |
                  ↓
              MySQL
                  |
                  ↓
              Storage
```

Example stack:

```text
React
   ↓
Node.js
   ↓
Express
   ↓
MySQL
```

Another:

```text
Flutter
   ↓
REST API
   ↓
Spring Boot
   ↓
MySQL
```

Another:

```text
Next.js
   ↓
API
   ↓
MySQL
```

---

# 52. Production Checklist

Before production:

```text
[ ] Primary keys
[ ] Foreign keys
[ ] Proper indexes
[ ] Constraints
[ ] Transactions
[ ] Backup strategy
[ ] Restore testing
[ ] Least-privilege users
[ ] Strong authentication
[ ] Prepared statements
[ ] Input validation
[ ] Query optimization
[ ] Monitoring
[ ] Error logging
[ ] Migration strategy
[ ] Connection pooling
```

---

# 53. Environment Variables

Never hard-code production credentials.

Bad:

```javascript
const password = "mySecretPassword";
```

Better:

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=shop
DB_USER=app_user
DB_PASSWORD=your_password
```

Example Node.js configuration:

```javascript
const mysql = require("mysql2/promise");

const pool = mysql.createPool({
    host: process.env.DB_HOST,
    port: Number(process.env.DB_PORT || 3306),
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME
});

module.exports = pool;
```

Never commit:

```text
.env
```

Add it to `.gitignore`:

```gitignore
.env
.env.*
!.env.example
```

Example:

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=shop
DB_USER=app_user
DB_PASSWORD=
```

---

# 54. Project Structure

Example backend project:

```text
my-project/
│
├── src/
│   ├── config/
│   │   └── database.js
│   │
│   ├── controllers/
│   │   └── user.controller.js
│   │
│   ├── services/
│   │   └── user.service.js
│   │
│   ├── repositories/
│   │   └── user.repository.js
│   │
│   ├── routes/
│   │   └── user.routes.js
│   │
│   └── app.js
│
├── database/
│   ├── migrations/
│   ├── seeds/
│   └── schema.sql
│
├── .env
├── .env.example
├── .gitignore
└── README.md
```

---

# 55. Complete E-Commerce Example

This section creates a small but realistic e-commerce database.

## Step 1 — Database

```sql
CREATE DATABASE IF NOT EXISTS ecommerce;

USE ecommerce;
```

---

## Step 2 — Users

```sql
CREATE TABLE users (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Insert:

```sql
INSERT INTO users (name, email)
VALUES
    ('John Doe', 'john@example.com'),
    ('Anna Smith', 'anna@example.com'),
    ('Dara Kim', 'dara@example.com');
```

---

## Step 3 — Categories

```sql
CREATE TABLE categories (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
```

Insert:

```sql
INSERT INTO categories (name)
VALUES
    ('Laptop'),
    ('Phone'),
    ('Accessory');
```

---

## Step 4 — Products

```sql
CREATE TABLE products (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    category_id BIGINT UNSIGNED NULL,
    name VARCHAR(150) NOT NULL,
    description TEXT,
    price DECIMAL(12,2) NOT NULL,
    stock INT UNSIGNED NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_products_category
        FOREIGN KEY (category_id)
        REFERENCES categories(id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

Insert:

```sql
INSERT INTO products (
    category_id,
    name,
    description,
    price,
    stock
)
VALUES
    (1, 'MacBook Pro', 'Apple laptop', 1999.99, 10),
    (1, 'Dell XPS', 'Dell laptop', 1499.99, 15),
    (2, 'iPhone', 'Apple smartphone', 999.99, 20),
    (2, 'Samsung Galaxy', 'Samsung smartphone', 899.99, 25),
    (3, 'Wireless Mouse', 'Bluetooth mouse', 49.99, 50);
```

---

## Step 5 — Orders

```sql
CREATE TABLE orders (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id BIGINT UNSIGNED NOT NULL,
    status ENUM(
        'pending',
        'paid',
        'shipped',
        'completed',
        'cancelled'
    ) NOT NULL DEFAULT 'pending',
    total_amount DECIMAL(12,2) NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_orders_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);
```

---

## Step 6 — Order Items

```sql
CREATE TABLE order_items (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    order_id BIGINT UNSIGNED NOT NULL,
    product_id BIGINT UNSIGNED NOT NULL,
    quantity INT UNSIGNED NOT NULL,
    price DECIMAL(12,2) NOT NULL,

    CONSTRAINT fk_order_items_order
        FOREIGN KEY (order_id)
        REFERENCES orders(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE,

    CONSTRAINT fk_order_items_product
        FOREIGN KEY (product_id)
        REFERENCES products(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);
```

Notice that `price` is stored in `order_items`.

This is useful because product prices can change later while historical orders should keep the price paid at the time of purchase.

---

## Step 7 — Create an Order

```sql
START TRANSACTION;

INSERT INTO orders (
    user_id,
    status,
    total_amount
)
VALUES (
    1,
    'pending',
    2049.98
);

SET @order_id = LAST_INSERT_ID();

INSERT INTO order_items (
    order_id,
    product_id,
    quantity,
    price
)
VALUES
    (@order_id, 1, 1, 1999.99),
    (@order_id, 5, 1, 49.99);

UPDATE products
SET stock = stock - 1
WHERE id = 1
  AND stock >= 1;

UPDATE products
SET stock = stock - 1
WHERE id = 5
  AND stock >= 1;

COMMIT;
```

In production application code, stock updates should also be checked carefully so an order cannot succeed if the requested quantity is unavailable.

---

## Step 8 — Get Orders

```sql
SELECT
    o.id AS order_id,
    u.name AS customer,
    o.status,
    o.total_amount,
    o.created_at
FROM orders o
INNER JOIN users u
    ON o.user_id = u.id
ORDER BY o.created_at DESC;
```

---

## Step 9 — Order Details

```sql
SELECT
    o.id AS order_id,
    u.name AS customer,
    p.name AS product,
    oi.quantity,
    oi.price,
    oi.quantity * oi.price AS subtotal
FROM orders o
INNER JOIN users u
    ON o.user_id = u.id
INNER JOIN order_items oi
    ON oi.order_id = o.id
INNER JOIN products p
    ON p.id = oi.product_id
ORDER BY o.id DESC;
```

---

## Step 10 — Customer Spending

```sql
SELECT
    u.id,
    u.name,
    COUNT(o.id) AS total_orders,
    COALESCE(SUM(o.total_amount), 0) AS total_spent
FROM users u
LEFT JOIN orders o
    ON o.user_id = u.id
GROUP BY u.id, u.name
ORDER BY total_spent DESC;
```

---

## Step 11 — Best-Selling Products

```sql
SELECT
    p.id,
    p.name,
    SUM(oi.quantity) AS total_quantity_sold,
    SUM(oi.quantity * oi.price) AS revenue
FROM order_items oi
INNER JOIN products p
    ON p.id = oi.product_id
INNER JOIN orders o
    ON o.id = oi.order_id
WHERE o.status IN ('paid', 'shipped', 'completed')
GROUP BY p.id, p.name
ORDER BY total_quantity_sold DESC;
```

---

## Step 12 — Products With Low Stock

```sql
SELECT
    id,
    name,
    stock
FROM products
WHERE stock < 10
ORDER BY stock ASC;
```

---

# 56. Final Roadmap

```text
BEGINNER
│
├── Database
├── Tables
├── Data Types
├── INSERT
├── SELECT
├── WHERE
├── ORDER BY
├── LIMIT
├── UPDATE
├── DELETE
│
INTERMEDIATE
│
├── Constraints
├── Primary Keys
├── Foreign Keys
├── Relationships
├── JOIN
├── GROUP BY
├── HAVING
├── Aggregate Functions
├── Subqueries
├── Views
├── CTE
├── Transactions
├── Indexes
│
ADVANCED
│
├── Stored Procedures
├── Stored Functions
├── Triggers
├── Events
├── Window Functions
├── JSON
├── Recursive CTE
├── Query Optimization
├── EXPLAIN
├── Normalization
├── Security
├── Backup
└── Production Architecture
```

---

# 57. Practice Projects

## Beginner

Build:

```text
1. Student Database
2. Employee Database
3. Library Database
4. School Database
```

Practice:

```text
CREATE
INSERT
SELECT
WHERE
UPDATE
DELETE
ORDER BY
LIMIT
```

---

## Intermediate

Build:

```text
1. Inventory System
2. Restaurant System
3. Hospital System
4. Course Management System
5. Banking Database
```

Practice:

```text
JOIN
FOREIGN KEY
GROUP BY
HAVING
SUBQUERY
CTE
VIEW
INDEX
TRANSACTION
```

---

## Advanced

Build:

```text
1. E-Commerce
2. Banking Platform
3. Hotel Booking System
4. Food Delivery System
5. Social Media Database
6. Learning Management System
7. Warehouse Management System
```

Practice:

```text
Transactions
Indexes
Window Functions
JSON
Stored Procedures
Triggers
Query Optimization
Security
Backup
Database Architecture
```

---

# 58. Conclusion

MySQL is one of the most important relational databases for backend and full-stack development.

The most important concepts to master are:

```text
SQL
│
├── SELECT
├── INSERT
├── UPDATE
├── DELETE
│
├── WHERE
├── ORDER BY
├── GROUP BY
├── HAVING
│
├── JOIN
├── Subqueries
├── CTE
│
├── Constraints
├── Relationships
├── Indexes
│
├── Transactions
├── Views
├── Procedures
├── Functions
├── Triggers
│
├── Window Functions
├── JSON
├── Recursive CTE
│
├── Optimization
├── EXPLAIN
├── Security
└── Backup
```

## Final Advice

Do not try to memorize every SQL command.

Instead, understand:

```text
How data is modeled
        ↓
How tables are related
        ↓
How data is queried
        ↓
How queries are optimized
        ↓
How transactions work
        ↓
How data is protected
        ↓
How databases operate in production
```

Once you understand these concepts, you can work with MySQL in:

```text
Node.js
Java
Spring Boot
Python
Django
PHP
Laravel
C#
.NET
Go
Ruby
Ruby on Rails
Kotlin
Android
Flutter
React
Next.js
```

---

## MySQL Quick Reference

```sql
-- Database
CREATE DATABASE shop;
USE shop;
SHOW DATABASES;

-- Table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE
);

-- Insert
INSERT INTO users (name, email)
VALUES ('John', 'john@example.com');

-- Read
SELECT *
FROM users;

-- Filter
SELECT *
FROM users
WHERE id = 1;

-- Update
UPDATE users
SET name = 'John Doe'
WHERE id = 1;

-- Delete
DELETE FROM users
WHERE id = 1;

-- Sort
SELECT *
FROM users
ORDER BY name ASC;

-- Count
SELECT COUNT(*)
FROM users;

-- Group
SELECT
    name,
    COUNT(*)
FROM users
GROUP BY name;

-- Join
SELECT *
FROM users u
JOIN orders o
    ON o.user_id = u.id;

-- Index
CREATE INDEX idx_users_email
ON users(email);

-- Transaction
START TRANSACTION;

-- SQL operations...

COMMIT;

-- Rollback
ROLLBACK;
```

---

## MySQL Mastery Checklist

```text
[ ] I understand databases
[ ] I understand tables
[ ] I understand rows and columns
[ ] I understand data types
[ ] I can create databases
[ ] I can create tables
[ ] I can insert data
[ ] I can query data
[ ] I can filter data
[ ] I can update data
[ ] I can delete data
[ ] I understand primary keys
[ ] I understand foreign keys
[ ] I understand relationships
[ ] I understand JOIN
[ ] I understand GROUP BY
[ ] I understand HAVING
[ ] I understand subqueries
[ ] I understand CTE
[ ] I understand views
[ ] I understand indexes
[ ] I understand transactions
[ ] I understand stored procedures
[ ] I understand functions
[ ] I understand triggers
[ ] I understand events
[ ] I understand window functions
[ ] I understand JSON
[ ] I understand recursive CTE
[ ] I can use EXPLAIN
[ ] I understand normalization
[ ] I understand database security
[ ] I can create backups
[ ] I can restore backups
[ ] I can design production databases
[ ] I can optimize SQL queries
```

---

## License

This documentation can be used for learning, personal projects, and GitHub documentation.

---

## Author

Created as a **MySQL Beginner → Advanced learning reference** with English + Khmer explanations.

⭐ If this guide helps you, consider starring the repository.
