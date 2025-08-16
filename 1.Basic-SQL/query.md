-- DDL: Create a table for users
-- This command defines the structure (schema) of our 'users' table.
CREATE TABLE users (
    user_id INT,
    username VARCHAR(50),
    email VARCHAR(100),
    is_active BOOLEAN,
    join_date DATE
);

-- DML: Insert sample data into the users table
-- These commands add new rows of data into the table.
INSERT INTO users (user_id, username, email, is_active, join_date) VALUES
(1, 'john_doe', 'john.doe@example.com', TRUE, '2025-01-15'),
(2, 'jane_smith', 'jane.smith@example.com', TRUE, '2025-02-20'),
(3, 'alice_jones', 'alice.jones@example.com', FALSE, '2025-03-10'),
(4, 'bob_brown', 'bob.brown@example.com', TRUE, '2025-02-22');

-- DML: Select queries to retrieve data

-- 1. Select all users and all columns
-- The '*' is a wildcard that means "all columns".
SELECT * FROM users;

-- 2. Select specific columns for active users only
-- The WHERE clause filters the rows to only include those where 'is_active' is TRUE.
SELECT username, email
FROM users
WHERE is_active = TRUE;

-- 3. Select users who joined in February, sorted by most recent first
-- The LIKE operator is used for pattern matching. '2025-02-%' matches any string starting with '2025-02-'.
-- ORDER BY sorts the results, and DESC specifies descending order.
SELECT username, join_date
FROM users
WHERE join_date::text LIKE '2025-02-%'
ORDER BY join_date DESC;

-- 4. Select the top 2 most recently joined users
-- LIMIT restricts the output to a specified number of rows after sorting.
SELECT user_id, username, join_date
FROM users
ORDER BY join_date DESC
LIMIT 2;

-- DDL: Altering an existing table
-- These commands modify the table's structure.

-- 1. Add a new column to the table
-- We are adding a column to store the last time a user logged in.
ALTER TABLE users ADD COLUMN last_login TIMESTAMP;

-- 2. Rename an existing column
-- 'join_date' is renamed to 'creation_date' for better clarity.
ALTER TABLE users RENAME COLUMN join_date TO creation_date;

-- 3. Drop a column from the table
-- We are removing the 'email' column completely.
ALTER TABLE users DROP COLUMN email;