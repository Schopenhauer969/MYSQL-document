# MySQL — Writing Data, Beginner to Advanced

A complete, practical guide to **writing data in MySQL** — from your first `INSERT` to production-grade bulk loads, transactions, triggers, and error handling.

Examples use standard **MySQL SQL** (works in the `mysql` CLI, MySQL Workbench) plus a **Node.js (`mysql2`)** section for application-level writes.

```bash
npm install mysql2
```

---

## Table of Contents

1. [Setup & Connection](#1-setup--connection)
2. [Beginner: Creating a Table](#2-beginner-creating-a-table)
3. [Beginner: Inserting Rows](#3-beginner-inserting-rows)
4. [Beginner: Basic Updates](#4-beginner-basic-updates)
5. [Beginner: Deleting Rows](#5-beginner-deleting-rows)
6. [Intermediate: Upserts (ON DUPLICATE KEY UPDATE)](#6-intermediate-upserts-on-duplicate-key-update)
7. [Intermediate: Auto Increment & Generated Keys](#7-intermediate-auto-increment--generated-keys)
8. [Intermediate: INSERT ... SELECT & REPLACE](#8-intermediate-insert--select--replace)
9. [Intermediate: JSON Columns](#9-intermediate-json-columns)
10. [Advanced: Bulk Inserts & LOAD DATA](#10-advanced-bulk-inserts--load-data)
11. [Advanced: Transactions & Savepoints](#11-advanced-transactions--savepoints)
12. [Advanced: Triggers for Auditing](#12-advanced-triggers-for-auditing)
13. [Advanced: Constraints & Validation](#13-advanced-constraints--validation)
14. [Advanced: Node.js (mysql2) Application Writes](#14-advanced-nodejs-mysql2-application-writes)
15. [Advanced: Stored Procedures & Error Handling](#15-advanced-stored-procedures--error-handling)
16. [Best Practices Cheat Sheet](#16-best-practices-cheat-sheet)

---

## 1. Setup & Connection

### MySQL CLI

```bash
mysql -u username -p -h hostname -P 3306 database_name
```

### Node.js Connection Pool

```javascript
// db.js
const mysql = require("mysql2/promise");

const pool = mysql.createPool({
  host: process.env.DB_HOST || "localhost",
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});

module.exports = pool;
```

```javascript
// index.js
const pool = require("./db");

async function main() {
  const [rows] = await pool.query("SELECT 1 + 1 AS result");
  console.log(rows); // [{ result: 2 }]
}

main().catch(console.error);
```

---

## 2. Beginner: Creating a Table

```sql
CREATE TABLE users (
    user_id     INT AUTO_INCREMENT PRIMARY KEY,
    name        VARCHAR(100) NOT NULL,
    email       VARCHAR(150) NOT NULL UNIQUE,
    age         TINYINT UNSIGNED,
    status      VARCHAR(20) DEFAULT 'active',
    created_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB;
```

> ℹ️ Always use the **InnoDB** engine for tables that need transactions, foreign keys, and row-level locking (it's the default since MySQL 5.5, but explicit is safer).

---

## 3. Beginner: Inserting Rows

### 3.1 Insert a Single Row

```sql
INSERT INTO users (name, email, age)
VALUES ('Alice Johnson', 'alice@example.com', 28);
```

### 3.2 Insert Multiple Rows in One Statement

```sql
INSERT INTO users (name, email, age)
VALUES
    ('Bob Smith', 'bob@example.com', 34),
    ('Carla Diaz', 'carla@example.com', 22),
    ('David Lee', 'david@example.com', 41);
```

> ✅ A single multi-row `INSERT` is dramatically faster than multiple single-row `INSERT`s — fewer round trips and one transaction commit.

### 3.3 Insert with Explicit Column Defaults

```sql
INSERT INTO users (name, email, age, status)
VALUES ('Erin Walsh', 'erin@example.com', 31, DEFAULT);
```

---

## 4. Beginner: Basic Updates

```sql
-- Update a single row
UPDATE users
SET age = 29
WHERE email = 'alice@example.com';

-- Update many rows
UPDATE users
SET status = 'inactive'
WHERE created_at < '2024-01-01 00:00:00';

-- Update with a row limit (MySQL-specific)
UPDATE users
SET status = 'flagged'
WHERE status = 'active'
ORDER BY created_at ASC
LIMIT 10;
```

Check how many rows were affected (in the CLI, this is printed automatically):

```
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

---

## 5. Beginner: Deleting Rows

```sql
-- Delete a single matching row
DELETE FROM users WHERE email = 'bob@example.com';

-- Delete many rows
DELETE FROM users WHERE status = 'inactive';

-- Delete with a limit, useful for throttled cleanup jobs
DELETE FROM logs WHERE created_at < '2024-01-01' LIMIT 1000;

-- Delete ALL rows fast (DDL, resets AUTO_INCREMENT, cannot be rolled back)
TRUNCATE TABLE staging_logs;
```

| Command | Logged? | Can Rollback? | Resets AUTO_INCREMENT? | Fires Triggers? |
|---|---|---|---|---|
| `DELETE` | Yes (row-level) | Yes, until commit | No | Yes |
| `TRUNCATE` | Minimal | No (implicit commit) | Yes | No |

---

## 6. Intermediate: Upserts (ON DUPLICATE KEY UPDATE)

MySQL's native upsert — requires a `UNIQUE` or `PRIMARY KEY` on the conflicting column(s).

```sql
INSERT INTO user_preferences (user_id, theme, created_at)
VALUES (1042, 'dark', NOW())
ON DUPLICATE KEY UPDATE
    theme = VALUES(theme),
    updated_at = NOW();
```

### Upsert with a Counter (common pattern: view counts, tallies)

```sql
INSERT INTO page_views (page_slug, views)
VALUES ('home', 1)
ON DUPLICATE KEY UPDATE views = views + 1;
```

### Alternative: `REPLACE INTO` (deletes + reinserts — use with caution)

```sql
REPLACE INTO users (user_id, name, email)
VALUES (7, 'Alice Johnson', 'alice.j@example.com');
```

> ⚠️ `REPLACE INTO` **deletes the old row and inserts a new one** — this resets any columns not included in the statement to their defaults, and re-triggers `AUTO_INCREMENT`/triggers as a delete+insert, not an update. Prefer `ON DUPLICATE KEY UPDATE` unless you specifically want replace semantics.

---

## 7. Intermediate: Auto Increment & Generated Keys

```sql
INSERT INTO orders (order_code, total) VALUES ('ORD-0001', 129.99);

-- Get the ID just generated in this session
SELECT LAST_INSERT_ID();
```

```javascript
// Same thing from Node.js
const [result] = await pool.execute(
  "INSERT INTO orders (order_code, total) VALUES (?, ?)",
  ["ORD-0002", 59.5]
);
console.log(result.insertId); // auto-generated primary key
```

### Setting or Resetting AUTO_INCREMENT

```sql
ALTER TABLE orders AUTO_INCREMENT = 1000;
```

---

## 8. Intermediate: INSERT ... SELECT & REPLACE

### Copy Rows Between Tables

```sql
INSERT INTO archived_users (name, email, age)
SELECT name, email, age
FROM users
WHERE status = 'inactive';
```

### Insert with a Join

```sql
INSERT INTO order_summaries (order_id, customer_name, total)
SELECT o.order_id, c.name, o.total
FROM orders o
JOIN customers c ON c.customer_id = o.customer_id
WHERE o.status = 'completed';
```

### Ignore Duplicate-Key Errors on Insert

```sql
INSERT IGNORE INTO users (user_id, name, email)
VALUES (7, 'Alice Johnson', 'alice@example.com');
-- If user_id 7 already exists, MySQL silently skips this row instead of erroring
```

---

## 9. Intermediate: JSON Columns

```sql
CREATE TABLE products (
    product_id  INT AUTO_INCREMENT PRIMARY KEY,
    name        VARCHAR(150) NOT NULL,
    attributes  JSON
);

INSERT INTO products (name, attributes)
VALUES (
    'Wireless Mouse',
    JSON_OBJECT('color', 'black', 'wireless', TRUE, 'tags', JSON_ARRAY('electronics', 'accessories'))
);

-- Update a single key inside the JSON document without rewriting the whole thing
UPDATE products
SET attributes = JSON_SET(attributes, '$.color', 'silver')
WHERE product_id = 1;

-- Append to a JSON array field
UPDATE products
SET attributes = JSON_ARRAY_APPEND(attributes, '$.tags', 'best-seller')
WHERE product_id = 1;

-- Remove a key
UPDATE products
SET attributes = JSON_REMOVE(attributes, '$.wireless')
WHERE product_id = 1;
```

---

## 10. Advanced: Bulk Inserts & LOAD DATA

### 10.1 Batched Multi-Row Inserts (application-level chunking)

```javascript
async function insertUsersBatch(pool, users) {
  // users = [{ name, email, age }, ...]
  const values = users.map(u => [u.name, u.email, u.age]);

  const [result] = await pool.query(
    "INSERT INTO users (name, email, age) VALUES ?",
    [values]
  );

  console.log(`Inserted ${result.affectedRows} rows`);
}
```

> ✅ For very large datasets, chunk into batches of ~500–1000 rows per statement rather than one giant `INSERT` — this keeps transaction/undo size and lock duration manageable.

### 10.2 LOAD DATA INFILE (fastest way to bulk-load from a file)

```sql
LOAD DATA INFILE '/var/lib/mysql-files/users.csv'
INTO TABLE users
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS  -- skip header row
(name, email, age);
```

```sql
-- Client-side variant when the file isn't on the server (requires local_infile enabled)
LOAD DATA LOCAL INFILE '/home/user/users.csv'
INTO TABLE users
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(name, email, age);
```

### 10.3 Temporarily Disabling Checks for Faster Bulk Loads

```sql
SET UNIQUE_CHECKS = 0;
SET FOREIGN_KEY_CHECKS = 0;

-- ... run your large bulk INSERT / LOAD DATA here ...

SET UNIQUE_CHECKS = 1;
SET FOREIGN_KEY_CHECKS = 1;
```

> ⚠️ Only disable checks for trusted, pre-validated bulk loads — re-enable immediately after, and be aware invalid data can slip through while checks are off.

---

## 11. Advanced: Transactions & Savepoints

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1001 AND balance >= 500;

-- Check affected rows in application code; if 0, funds were insufficient

SAVEPOINT after_debit;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 1002;

INSERT INTO transfers (from_account, to_account, amount, created_at)
VALUES (1001, 1002, 500, NOW());

-- If something goes wrong after the debit, you can partially roll back:
-- ROLLBACK TO SAVEPOINT after_debit;

COMMIT;
```

**Key points:**
- `START TRANSACTION` (or `BEGIN`) opens an explicit transaction; MySQL is otherwise in `autocommit` mode by default.
- `InnoDB` is required for real ACID transactions — `MyISAM` does not support them.
- Default isolation level is `REPEATABLE READ`; use `SET TRANSACTION ISOLATION LEVEL READ COMMITTED` (or others) when needed.

---

## 12. Advanced: Triggers for Auditing

```sql
CREATE TABLE users_audit (
    audit_id    INT AUTO_INCREMENT PRIMARY KEY,
    user_id     INT,
    action      VARCHAR(10),
    old_email   VARCHAR(150),
    new_email   VARCHAR(150),
    changed_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    changed_by  VARCHAR(100)
);

DELIMITER $$

CREATE TRIGGER trg_users_after_update
AFTER UPDATE ON users
FOR EACH ROW
BEGIN
    INSERT INTO users_audit (user_id, action, old_email, new_email, changed_by)
    VALUES (OLD.user_id, 'UPDATE', OLD.email, NEW.email, CURRENT_USER());
END$$

CREATE TRIGGER trg_users_after_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO users_audit (user_id, action, new_email, changed_by)
    VALUES (NEW.user_id, 'INSERT', NEW.email, CURRENT_USER());
END$$

CREATE TRIGGER trg_users_after_delete
AFTER DELETE ON users
FOR EACH ROW
BEGIN
    INSERT INTO users_audit (user_id, action, old_email, changed_by)
    VALUES (OLD.user_id, 'DELETE', OLD.email, CURRENT_USER());
END$$

DELIMITER ;
```

---

## 13. Advanced: Constraints & Validation

```sql
CREATE TABLE orders (
    order_id     INT AUTO_INCREMENT PRIMARY KEY,
    customer_id  INT NOT NULL,
    total        DECIMAL(10,2) NOT NULL,
    status       VARCHAR(20) DEFAULT 'pending',

    CONSTRAINT chk_total_positive CHECK (total >= 0),
    CONSTRAINT chk_status_valid
        CHECK (status IN ('pending', 'shipped', 'delivered', 'cancelled')),
    CONSTRAINT fk_orders_customer
        FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
) ENGINE=InnoDB;
```

> ℹ️ `CHECK` constraints are enforced starting in **MySQL 8.0.16+**; in earlier versions they are parsed but silently ignored.

A write that violates a constraint raises an error immediately, before anything is committed:

| Error | Meaning |
|---|---|
| `1062 Duplicate entry` | Unique constraint / primary key violation |
| `1048 Column cannot be null` | `NOT NULL` violation |
| `3819 Check constraint violated` | `CHECK` constraint failed |
| `1452 Cannot add or update a child row` | Foreign key constraint violation |
| `1451 Cannot delete or update a parent row` | Foreign key violated on delete |

---

## 14. Advanced: Node.js (mysql2) Application Writes

### Single Insert with Prepared Statements (always use `?` placeholders)

```javascript
async function insertUser(pool, name, email, age) {
  const [result] = await pool.execute(
    "INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
    [name, email, age]
  );

  console.log(`Inserted user_id: ${result.insertId}`);
  return result.insertId;
}
```

### Upsert from the Application Layer

```javascript
async function upsertPreference(pool, userId, theme) {
  const [result] = await pool.execute(
    `INSERT INTO user_preferences (user_id, theme, created_at)
     VALUES (?, ?, NOW())
     ON DUPLICATE KEY UPDATE theme = VALUES(theme), updated_at = NOW()`,
    [userId, theme]
  );

  console.log(`Affected rows: ${result.affectedRows}`); // 1 = insert, 2 = update
}
```

### Transaction Across Multiple Statements

```javascript
async function transferFunds(pool, fromId, toId, amount) {
  const connection = await pool.getConnection();
  try {
    await connection.beginTransaction();

    const [debit] = await connection.execute(
      "UPDATE accounts SET balance = balance - ? WHERE account_id = ? AND balance >= ?",
      [amount, fromId, amount]
    );

    if (debit.affectedRows === 0) {
      throw new Error("Insufficient funds or account not found");
    }

    await connection.execute(
      "UPDATE accounts SET balance = balance + ? WHERE account_id = ?",
      [amount, toId]
    );

    await connection.execute(
      "INSERT INTO transfers (from_account, to_account, amount) VALUES (?, ?, ?)",
      [fromId, toId, amount]
    );

    await connection.commit();
    console.log("Transfer committed");
  } catch (error) {
    await connection.rollback();
    console.error("Transfer rolled back:", error.message);
    throw error;
  } finally {
    connection.release();
  }
}
```

---

## 15. Advanced: Stored Procedures & Error Handling

```sql
DELIMITER $$

CREATE PROCEDURE transfer_funds(
    IN p_from_id INT,
    IN p_to_id INT,
    IN p_amount DECIMAL(10,2)
)
BEGIN
    DECLARE v_balance DECIMAL(10,2);
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL; -- re-raise the original error to the caller
    END;

    START TRANSACTION;

    SELECT balance INTO v_balance
    FROM accounts
    WHERE account_id = p_from_id
    FOR UPDATE; -- row lock to prevent concurrent double-spend

    IF v_balance IS NULL THEN
        SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Source account not found';
    ELSEIF v_balance < p_amount THEN
        SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Insufficient funds';
    END IF;

    UPDATE accounts SET balance = balance - p_amount WHERE account_id = p_from_id;
    UPDATE accounts SET balance = balance + p_amount WHERE account_id = p_to_id;

    INSERT INTO transfers (from_account, to_account, amount, created_at)
    VALUES (p_from_id, p_to_id, p_amount, NOW());

    COMMIT;
END$$

DELIMITER ;
```

```sql
-- Call it
CALL transfer_funds(1001, 1002, 500.00);
```

**Common handled conditions:**

| Condition | Raised When |
|---|---|
| `SQLEXCEPTION` | Catch-all for any SQL error (recommended default handler) |
| `SQLWARNING` | Non-fatal warnings (e.g. data truncation) |
| `NOT FOUND` | A cursor `FETCH` has no more rows |
| `SIGNAL SQLSTATE '45000'` | Custom application-defined error |

---

## 16. Best Practices Cheat Sheet

- ✅ Always use **prepared statements / placeholders** (`?`) — never concatenate user input into SQL strings.
- ✅ Use multi-row `INSERT ... VALUES (...), (...), (...)` instead of looping single-row inserts.
- ✅ Use `ON DUPLICATE KEY UPDATE` for upserts; avoid `REPLACE INTO` unless you specifically want delete+insert semantics.
- ✅ Wrap multi-step writes in an explicit `START TRANSACTION ... COMMIT`, especially across multiple tables.
- ✅ Use `SELECT ... FOR UPDATE` inside a transaction to lock rows and prevent race conditions (e.g. balance transfers).
- ✅ Use `LOAD DATA INFILE` for large one-time imports — it's dramatically faster than row-by-row `INSERT`.
- ✅ Add `CHECK`, `NOT NULL`, and `FOREIGN KEY` constraints (MySQL 8.0.16+ for `CHECK`) to catch bad data at the database layer.
- ✅ Use `InnoDB` for any table needing transactions or foreign keys.
- ✅ Commit in batches during huge bulk loads to control lock and undo-log growth.
- ❌ Don't forget that `TRUNCATE` is DDL — it auto-commits immediately and can't be rolled back.
- ❌ Don't rely on `SELECT MAX(id)+1` for keys — use `AUTO_INCREMENT` to avoid race conditions.
- ❌ Don't leave `FOREIGN_KEY_CHECKS`/`UNIQUE_CHECKS` disabled longer than the bulk-load statement itself.

---

## License

Free to use in any project — copy, adapt, and drop straight into your own `README.md`.
