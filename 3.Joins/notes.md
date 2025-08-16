# 3. Joins

`JOIN` clauses are used to combine rows from two or more tables based on a related column between them. Mastering joins is arguably the most important practical SQL skill for working with relational data.

---

## Types of Joins

The most common types of joins can be visualized using Venn diagrams. Imagine the left circle is `Table A` and the right circle is `Table B`. The shaded area represents the data that is returned.



### `INNER JOIN`
Returns records that have matching values in **both** tables. It's the intersection of the two tables.

### `LEFT JOIN` (or `LEFT OUTER JOIN`)
Returns **all** records from the left table (`Table A`), and the matched records from the right table (`Table B`). If there is no match, the columns from the right table will be `NULL`.

### `RIGHT JOIN` (or `RIGHT OUTER JOIN`)
Returns **all** records from the right table (`Table B`), and the matched records from the left table (`Table A`). It's the opposite of a `LEFT JOIN`.

### `FULL OUTER JOIN`
Returns all records when there is a match in **either** the left or the right table. It essentially combines the results of `LEFT JOIN` and `RIGHT JOIN`.

### `SELF JOIN`
This isn't a different type of join, but a regular join where a table is joined with itself. It's used to query hierarchical data or compare rows within the same table.

### `CROSS JOIN`
Returns the Cartesian product of the two tables—every row from the first table is combined with every row from the second. This is rarely used and can produce massive result sets.

---

## Practical SQL Example

We will use the `employees` and `departments` tables from the previous section. First, let's add some data to better illustrate the joins.

```sql
-- Add a new department that has no employees yet
INSERT INTO departments (dept_id, dept_name) VALUES (4, 'Marketing');

-- Add a new employee who is not yet assigned to a department
INSERT INTO employees (emp_id, first_name, last_name, email, salary, dept_id) VALUES
(104, 'Diana', 'Miller', 'diana.m@example.com', 72000, NULL);
```

### 1. INNER JOIN Example
Returns only employees who are assigned to a department. `Diana` (no department) and `Marketing` (no employees) are excluded.

```sql
SELECT
    e.first_name,
    d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

### 2. LEFT JOIN Example
Returns **all employees**, even if they don't have a department. `Diana` is included, but her `dept_name` is `NULL`.

```sql
SELECT
    e.first_name,
    d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```

### 3. RIGHT JOIN Example
Returns **all departments**, even if they have no employees. `Marketing` is included, but its `first_name` is `NULL`.

```sql
SELECT
    e.first_name,
    d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

### 4. FULL OUTER JOIN Example
Returns **all employees and all departments**. Both `Diana` and `Marketing` are included in the result set with `NULL`s where there is no match.

```sql
SELECT
    e.first_name,
    d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;
```

### 5. SELF JOIN Example
To show this, we need a manager for each employee. Let's add a `manager_id` column that refers back to the `emp_id`.

```sql
-- First, add the column
ALTER TABLE employees ADD COLUMN manager_id INT;

-- Now, assign managers
UPDATE employees SET manager_id = 101 WHERE emp_id = 102; -- Alice manages Bob
UPDATE employees SET manager_id = 101 WHERE emp_id = 103; -- Alice manages Charlie

-- This query finds the manager's name for each employee
SELECT
    e.first_name AS employee_name,
    m.first_name AS manager_name
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.emp_id; -- Join the table to itself
```

---

### 💡 Key Interview Takeaways

* **`INNER JOIN` vs. `LEFT JOIN`:** This is the most common question about joins.
    * **`INNER JOIN`** is for when you only want records where a relationship **exists**.
    * **`LEFT JOIN`** is for when you want all records from the primary (left) table, regardless of whether a relationship exists. A key use case is finding things that *haven't* happened (e.g., find all customers who have **never** placed an order by using a `LEFT JOIN` from `customers` to `orders` and filtering `WHERE orders.id IS NULL`).
* **Hierarchical Data:** When you hear about querying hierarchical data (like org charts, categories and sub-categories), your first thought should be **`SELF JOIN`**.

### Common Interview Questions

1.  **Explain the difference between an `INNER JOIN` and a `LEFT JOIN`.**
    * *Answer:* An `INNER JOIN` returns only the rows where the join condition is met in both tables. A `LEFT JOIN` returns all rows from the left table, and for rows that have no match in the right table, it returns `NULL` for the right table's columns.
2.  **When would you use a `SELF JOIN`? Provide a practical example.**
    * *Answer:* You use a `SELF JOIN` for querying hierarchical data within the same table. A classic example is an `employees` table where each employee has a `manager_id` that points to another employee's `id`. You would self-join to get the employee's name and their manager's name in the same row.