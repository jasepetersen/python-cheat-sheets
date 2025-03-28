# PostgreSQL Cheat Sheet

## Connect to PostgreSQL

```bash
psql -U username -d dbname
```

## Common Commands

```sql
-- Connect to a database
\c dbname

-- List databases, tables, users
\l          -- databases
\dt         -- tables
\du         -- roles

-- Describe a table
\d tablename

-- Quit psql
\q
```

## Create and Drop

```sql
CREATE DATABASE mydb;
DROP DATABASE mydb;

CREATE USER myuser WITH PASSWORD 'secret';
DROP USER myuser;
```

## Grant Privileges

```sql
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;
GRANT SELECT, INSERT ON tablename TO myuser;
```

## Create Table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Insert Data

```sql
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
```

## Update Data

```sql
UPDATE users SET email = 'alice@new.com' WHERE name = 'Alice';
```

## Delete Data

```sql
DELETE FROM users WHERE id = 1;
```

## Query Data

```sql
SELECT * FROM users;
SELECT name FROM users WHERE email LIKE '%@example.com';
```

## Filtering and Sorting

```sql
SELECT * FROM users WHERE name = 'Alice' ORDER BY created_at DESC LIMIT 10;
```

## Aggregate Functions

```sql
SELECT COUNT(*) FROM users;
SELECT AVG(age) FROM users;
SELECT MAX(created_at) FROM users;
```

## Joins

```sql
SELECT o.id, u.name
FROM orders o
JOIN users u ON o.user_id = u.id;
```

## Indexes

```sql
CREATE INDEX idx_users_email ON users(email);
```

## Alter Table

```sql
ALTER TABLE users ADD COLUMN age INT;
ALTER TABLE users DROP COLUMN age;
```

## Transactions

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- Or ROLLBACK if something fails
```

## JSON Support

```sql
-- Insert JSON
INSERT INTO data (info) VALUES ('{"key": "value"}');

-- Query JSON field
SELECT info->>'key' FROM data;
```

## Useful psql Options

```bash
psql -U user -d dbname -h host -p port
psql -f script.sql              # Run SQL file
```
