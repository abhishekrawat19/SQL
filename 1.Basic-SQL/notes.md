# 1. SQL Basics and Data Types

This section covers the foundational concepts of SQL. Mastering these basics is essential before moving on to more complex topics.

## SQL Command Categories

SQL commands are divided into four main categories. Understanding this separation is a common starting point in interviews.

1.  **DDL (Data Definition Language):** Used to define or modify the database schema (the structure).
    * `CREATE`: Creates a new table, database, or index.
    * `ALTER`: Modifies the structure of an existing database object.
    * `DROP`: Deletes an entire table, database, or index.
2.  **DML (Data Manipulation Language):** Used for managing the data itself.
    * `SELECT`: Retrieves data from a table.
    * `INSERT`: Adds new rows of data into a table.
    * `UPDATE`: Modifies existing data in a table.
    * `DELETE`: Removes rows from a table.
3.  **DCL (Data Control Language):** Used to manage access and permissions.
    * `GRANT`: Gives a user access privileges.
    * `REVOKE`: Takes back access privileges.
4.  **TCL (Transaction Control Language):** Used to manage transactions.
    * `COMMIT`: Saves all the work done in a transaction.
    * `ROLLBACK`: Reverts the database to its state before the transaction began.

---

## The Core `SELECT` Statement

The `SELECT` statement is the most frequently used command for retrieving data.

* `SELECT column1, column2`: Specifies the columns you want. Use `*` to select all columns.
* `FROM table_name`: Specifies the table you're querying.
* `WHERE condition`: Filters records based on a specific condition (e.g., `age > 30`).
* `ORDER BY column`: Sorts the result set in ascending (`ASC`) or descending (`DESC`) order.
* `LIMIT n`: Restricts the number of rows returned, which is useful for pagination or finding top results.

---

## Common Data Types

Choosing the correct data type is crucial for data integrity and performance.

| Data Type | Description | Common Use Case |
| :--- | :--- | :--- |
| `INT` or `INTEGER` | Whole numbers. | For unique IDs, counts, or quantities. |
| `VARCHAR(n)` | A variable-length string with a max length of `n` characters. | Usernames, titles, or any text with a known max length. |
| `TEXT` | A variable-length string with a very large capacity. | Blog posts, product descriptions, or long comments. |
| `BOOLEAN` | Stores `TRUE` or `FALSE` values. | Flags like `is_active` or `has_paid`. |
| `DATE` | Stores a date (year, month, day). | Birthdays, hire dates. |
| `TIMESTAMP` | Stores both date and time information, often with a time zone. | Event logging like `created_at` or `last_updated`. |
| `DECIMAL(p, s)` | A fixed-precision number with `p` total digits and `s` decimal places. | 💰 Financial data where precision is critical (e.g., prices). |

### 💡 Key Interview Takeaways

* **DDL vs. DML:** This is a classic "hello world" question for SQL. **DDL** defines the *structure* (the blueprint of the house), while **DML** manages the *data* inside that structure (the furniture).
* **`VARCHAR` vs. `TEXT`:** Use `VARCHAR(n)` when you can enforce a reasonable limit. It can be more performant as the database knows the maximum space needed. Use `TEXT` when the length is unknown or could be very large.
* **`DELETE`, `TRUNCATE`, and `DROP`:** `DELETE` is DML, removes rows one by one, and can be rolled back. `TRUNCATE` is DDL, removes all rows at once (faster), and cannot be rolled back. `DROP` is DDL and removes the entire table structure and data permanently.

### Common Interview Questions

1.  **What is the difference between DDL and DML? Provide examples.**
    * *Answer:* DDL commands like `CREATE TABLE` define the database schema. DML commands like `SELECT` and `INSERT` are used to query and manipulate the data within that schema.
2.  **When would you use `TIMESTAMP` instead of `DATE`?**
    * *Answer:* You'd use `TIMESTAMP` when you need to know the exact time something happened, not just the day. It's essential for logging events, tracking updates, or scheduling tasks.
3.  **Explain the purpose of the `WHERE` and `ORDER BY` clauses.**
    * *Answer:* The `WHERE` clause filters rows to include only those that meet a specific condition. The `ORDER BY` clause sorts the final result set based on one or more columns, either ascending or descending.