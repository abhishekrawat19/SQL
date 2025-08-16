# 5. Subqueries and CTEs

Subqueries and Common Table Expressions (CTEs) are powerful constructs for breaking down complex problems into logical, manageable steps. While they can often achieve the same results, CTEs are generally preferred for readability.

---

## Subqueries (or Inner Queries)

A **subquery** is a SQL query nested inside a larger query. It can be used in various places, such as the `SELECT`, `FROM`, or `WHERE` clause.

* **Scalar Subquery:** A subquery that returns a single value (one row, one column).
* **Multi-row Subquery:** A subquery that returns multiple rows, often used with operators like `IN`.
* **Correlated Subquery:** A subquery that depends on the outer query for its values. It is executed once for every row processed by the outer query and can be inefficient.

## Common Table Expressions (CTEs)

A **CTE** allows you to define a temporary, named result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. They are defined using the `WITH` clause, which greatly improves the readability of complex queries.

### Subqueries vs. CTEs

| Feature | Subquery | CTE (Common Table Expression) |
| :--- | :--- | :--- |
| **Readability** | Can become hard to read when nested deeply. | Much cleaner and easier to read, like defining variables. |
| **Reusability** | Must be re-written if needed multiple times. | Can be referenced multiple times in the main query. |
| **Recursion** | Not possible. | Can be recursive (able to reference themselves). |

**Shortcut:** For any multi-step query, prefer CTEs. They make your code more maintainable and easier to debug.

---

## Practical SQL Example

We will use the `employees` and `departments` tables.

### 1. Subquery Example
Find all employees who work in the 'Engineering' department by using a subquery to find the `dept_id`.

```sql
SELECT emp_id, first_name
FROM employees
WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE dept_name = 'Engineering'
);
```

###