# 2. Constraints and Keys

This file covers **constraints** and **keys**, which are the rules that protect data integrity in a database. Understanding them is critical for designing reliable and robust table structures.

---

## What are Constraints?

**Constraints** are rules enforced on data columns in a table. They are used to limit the type of data that can go into a table, ensuring accuracy and reliability. If you try to perform an action that violates a constraint, the action is aborted.

Common constraints include:
* `NOT NULL`: Ensures that a column cannot have a `NULL` value.
* `UNIQUE`: Ensures that all values in a column are different.
* `DEFAULT`: Provides a default value for a column when none is specified.
* `CHECK`: Ensures that the values in a column satisfy a specific condition (e.g., `CHECK (salary > 0)`).

---

## What are Keys?

**Keys** are a special type of constraint used to uniquely identify rows and create relationships between tables. They are the backbone of a relational database.

### `PRIMARY KEY`
A **primary key** is a constraint that uniquely identifies each record in a table.
* It must contain **`UNIQUE`** values.
* It **cannot** contain **`NULL`** values.
* A table can have only **one** primary key. This key can consist of a single column or multiple columns (a **composite key**).

### `FOREIGN KEY`
A **foreign key** is a key used to link two tables together. It is a column (or a collection of columns) in one table that refers to the `PRIMARY KEY` in another table. This enforces **referential integrity**, meaning you can't add a record to the child table (the one with the foreign key) unless the corresponding record exists in the parent table.



---

## Practical SQL Example

Let's see this in action. We'll create two tables, `departments` and `employees`, where each employee belongs to one department.

### 1. Table Creation
Here, we define the tables and apply the constraints directly in the schema.

```sql
-- Create a 'departments' table first (the "parent" table)
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(100) NOT NULL UNIQUE
);

-- Create an 'employees' table (the "child" table)
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10, 2) CHECK (salary > 0),
    dept_id INT,

    -- This line establishes the link between employees and departments
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

### 2. Inserting Valid Data
This data follows all the rules we defined.

```sql
-- Insert data into the parent table first
INSERT INTO departments (dept_id, dept_name) VALUES
(1, 'Engineering'),
(2, 'Human Resources'),
(3, 'Sales');

-- Now insert data into the child table, referencing valid dept_id's
INSERT INTO employees (emp_id, first_name, last_name, email, salary, dept_id) VALUES
(101, 'Alice', 'Williams', 'alice.w@example.com', 90000, 1),
(102, 'Bob', 'Johnson', 'bob.j@example.com', 80000, 1),
(103, 'Charlie', 'Davis', 'charlie.d@example.com', 65000, 2);
```

### 3. Constraint Violation Examples
These `INSERT` statements will **fail** because they violate the constraints we set.

```sql
-- This will FAIL because the primary key '101' already exists.
-- VIOLATION: PRIMARY KEY constraint
-- INSERT INTO employees (emp_id, first_name, last_name, email, salary, dept_id) VALUES
-- (101, 'Eve', 'Smith', 'eve.s@example.com', 50000, 1);

-- This will FAIL because the dept_id '4' does not exist in the 'departments' table.
-- VIOLATION: FOREIGN KEY constraint
-- INSERT INTO employees (emp_id, first_name, last_name, email, salary, dept_id) VALUES
-- (105, 'Frank', 'White', 'frank.w@example.com', 55000, 4);

-- This will FAIL because the salary is not greater than 0.
-- VIOLATION: CHECK constraint
-- INSERT INTO employees (emp_id, first_name, last_name, email, salary, dept_id) VALUES
-- (106, 'Grace', 'Lee', 'grace.l@example.com', -5000, 3);
```

---

### 💡 Key Interview Takeaways

* **`PRIMARY KEY` vs. `UNIQUE` Constraint:** This is a very common interview question. The differences are simple but crucial.

| Feature | `PRIMARY KEY` | `UNIQUE` Constraint |
| :--- | :--- | :--- |
| **Purpose** | Main identifier for a row in a table. | Ensures values in a column are unique (e.g., email). |
| **NULLs** | **Cannot** accept `NULL` values. | **Can** accept one `NULL` value (in most DB systems). |
| **Quantity** | Only **one** per table. | Can have **multiple** per table. |

* **Referential Integrity:** The main purpose of a **foreign key** is to maintain referential integrity. This means it prevents "orphan" records—for example, it stops you from having an employee assigned to a department that doesn't exist.

### Common Interview Questions

1.  **What is a `PRIMARY KEY` and what are its core properties?**
    * *Answer:* It's a unique, non-null identifier for each row in a table. Every table should have one, and it can only have one.
2.  **Explain the difference between a `PRIMARY KEY` and a `UNIQUE` constraint.**
    * *Answer:* A `PRIMARY KEY` is a table's main identifier, cannot be null, and is limited to one per table. A `UNIQUE` constraint also ensures uniqueness but allows one `NULL` value, and a table can have many `UNIQUE` constraints.
3.  **What is a `FOREIGN KEY`'s main purpose?**
    * *Answer:* Its main purpose is to link two tables and enforce referential integrity, which ensures that a relationship between tables remains consistent.