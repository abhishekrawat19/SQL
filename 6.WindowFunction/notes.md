# 6. Window Functions

**Window functions** perform a calculation across a set of table rows that are somehow related to the current row. This is powerful because it lets you use aggregate-like functions without collapsing the result set with `GROUP BY`. Each row retains its unique identity.

---

## Syntax and Key Concepts

The magic of window functions lies in the `OVER()` clause.

`FUNCTION_NAME() OVER (PARTITION BY ... ORDER BY ...)`

* `FUNCTION_NAME()`: The window function to use (e.g., `SUM()`, `RANK()`).
* `PARTITION BY column_name`: This divides the rows into partitions (groups). The function is then applied independently to each partition. It's like a `GROUP BY` for window functions.
* `ORDER BY column_name`: This orders rows within each partition. It is essential for ranking and sequence functions like `RANK()` and `LAG()`.

---

## Common Window Functions

### Ranking Functions
These are classic interview questions.
* **`ROW_NUMBER()`**: Assigns a unique, sequential integer to each row (1, 2, 3, 4).
* **`RANK()`**: Assigns a rank to each row, with gaps in the ranking for ties (1, 2, 2, 4).
* **`DENSE_RANK()`**: Assigns a rank without gaps for ties (1, 2, 2, 3).

### Positional Functions
* **`LEAD()`**: Accesses data from a subsequent row in the same result set.
* **`LAG()`**: Accesses data from a previous row in the same result set.

### Aggregate Functions as Window Functions
Standard aggregate functions can be used as window functions to create running totals, moving averages, or compare a row's value to the partition's total.

---

## Practical SQL Example

Let's use a new table to demonstrate these functions effectively.

```sql
CREATE TABLE employees_adv (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    department VARCHAR(50),
    hire_date DATE,
    salary DECIMAL(10, 2)
);

INSERT INTO employees_adv (emp_id, first_name, department, hire_date, salary) VALUES
(101, 'Alice', 'Engineering', '2022-01-10', 95000),
(102, 'Bob', 'Engineering', '2021-03-15', 110000),
(103, 'Charlie', 'Engineering', '2022-05-20', 95000), -- Tie with Alice
(104, 'Diana', 'Sales', '2020-08-01', 80000),
(105, 'Eve', 'Sales', '2021-11-12', 85000),
(106, 'Frank', 'HR', '2023-01-05', 60000);
```

### 1. Ranking Functions Example
Rank employees in each department based on their salary (highest first). Notice the different outputs for the tied salaries.

```sql
SELECT
    first_name,
    department,
    salary,
    ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) as row_num,
    RANK()       OVER(PARTITION BY department ORDER BY salary DESC) as rank_num,
    DENSE_RANK() OVER(PARTITION BY department ORDER BY salary DESC) as dense_rank_num
FROM employees_adv;
```

### 2. Positional Function (`LAG`) Example
Show each employee's salary and the salary of the person hired just before them in the same department.

```sql
SELECT
    first_name,
    department,
    hire_date,
    salary,
    LAG(salary, 1, 0) OVER(PARTITION BY department ORDER BY hire_date) as previous_hire_salary
FROM employees_adv;
```

### 3. Aggregate as a Window Function Example
Show each employee's salary compared to their department's average, and calculate a running total of salaries within the department (ordered by hire date).

```sql
SELECT
    first_name,
    department,
    hire_date,
    salary,
    AVG(salary) OVER(PARTITION BY department) as avg_dept_salary,
    SUM(salary) OVER(PARTITION BY department ORDER BY hire_date) as running_total_salary
FROM employees_adv;
```

---

### 💡 Key Interview Takeaways

* **Window vs. `GROUP BY`:** This is the most critical concept. A `GROUP BY` aggregation collapses multiple rows into a single summary row. A window function operates on a set of rows (the "window") but **preserves the original number of rows**, returning a value for each one.
* **`RANK()` vs. `DENSE_RANK()`:** This is the most common direct question. Use the race analogy:
    * `RANK()`: Olympic medals with ties (1st, 2nd, 2nd, **4th**). Ranks skip after a tie.
    * `DENSE_RANK()`: A dense ranking with ties (1st, 2nd, 2nd, **3rd**). Ranks do not skip.

### Common Interview Questions

1.  **What is a window function and how does it differ from a `GROUP BY` aggregation?**
    * *Answer:* A window function computes a value for each row based on a related set of rows, but it preserves the individual rows. A `GROUP BY` aggregation collapses multiple rows into a single summary row, losing the individual row detail.
2.  **Explain the difference between `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()`.**
    * *Answer:* All three assign a rank within a partition. `ROW_NUMBER` gives a unique number regardless of ties. `RANK` gives the same rank to ties but leaves a gap before the next rank. `DENSE_RANK` also gives the same rank to ties but does not leave a gap.
3.  **Provide a practical business use case for `LAG()` or `LEAD()`.**
    * *Answer:* `LAG()` is perfect for calculating period-over-period growth. For example, you can use `LAG(monthly_sales, 1) OVER (ORDER BY month)` to get the previous month's sales on the current month's row, making it easy to calculate the month-over-month sales difference.