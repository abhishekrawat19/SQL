# 9. Common Interview Queries 🧑‍💻

This section contains hands-on, practical SQL problems that frequently appear in technical interviews. Being able to solve these efficiently is a strong signal of your SQL proficiency. The key is to understand the underlying **pattern**, not just memorize the answer.

---

## Common Problem Patterns

### 1. N-th Highest Value
This is the most classic SQL interview question. The most common variant is "Find the second-highest salary."

* **The Challenge:** You need to handle duplicates and ties gracefully. What if three people share the second-highest salary?
* **Best Approach:** Use the `DENSE_RANK()` window function. It's robust, handles ties perfectly, and is easily adapted to find the N-th value by just changing a number in the final `WHERE` clause.

### 2. Finding Duplicates
The task is to find values that appear more than once in a column, such as duplicate emails in a `Users` table.

* **The Challenge:** You need to group by the column in question and then filter those groups.
* **Best Approach:** Use `GROUP BY` on the column you're checking for duplicates, then use `HAVING COUNT(*) > 1` to filter for the groups that contain more than one entry.

### 3. Employees Earning More Than Their Managers
This question tests your understanding of `SELF JOIN`. You need to compare rows within the same table.

* **The Challenge:** The core task is to get an employee's salary and their manager's salary on the same row for comparison.
* **Best Approach:** A `SELF JOIN` on the employees table, linking an employee's `manager_id` to their manager's `employee_id`.

---

## Practical SQL Examples

### Problem 1: N-th Highest Salary

**Task:** Find the second highest salary from the `salaries` table.

```sql
CREATE TABLE salaries ( id INT, name VARCHAR(50), salary INT );
INSERT INTO salaries (id, name, salary) VALUES
(1, 'Alice', 90000), (2, 'Bob', 85000), (3, 'Charlie', 85000), (4, 'Diana', 80000), (5, 'Eve', 90000);
```

**Solution 1: Using `DENSE_RANK()` (Best & Most Scalable)**
```sql
WITH SalaryRanks AS (
    SELECT
        salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) as salary_rank
    FROM salaries
)
SELECT salary FROM SalaryRanks WHERE salary_rank = 2;
```

**Solution 2: Using a Subquery (Traditional)**
```sql
SELECT MAX(salary)
FROM salaries
WHERE salary < (SELECT MAX(salary) FROM salaries);
```

---

### Problem 2: Finding Duplicates

**Task:** Find all duplicate emails in the `contacts` table.

```sql
CREATE TABLE contacts ( id INT, email VARCHAR(100) );
INSERT INTO contacts (id, email) VALUES
(1, 'alice@example.com'),(2, 'bob@example.com'),(3, 'charlie@example.com'),
(4, 'alice@example.com'),(5, 'diana@example.com'),(6, 'bob@example.com');
```

**Solution: Using `GROUP BY` and `HAVING`**
```sql
SELECT
    email,
    COUNT(email) AS occurrences
FROM contacts
GROUP BY email
HAVING COUNT(email) > 1;
```

---

### Problem 3: Employees Earning More Than Their Managers

**Task:** Find all employees who earn more than their managers.

```sql
CREATE TABLE staff ( id INT, name VARCHAR(50), salary INT, manager_id INT );
INSERT INTO staff (id, name, salary, manager_id) VALUES
(1, 'John', 70000, 3), (2, 'Mike', 80000, 4), (3, 'Sarah', 90000, NULL),
(4, 'Tom', 85000, 3), (5, 'Linda', 92000, 4); -- Linda earns more than her manager Tom
```

**Solution: Using a `SELF JOIN`**
```sql
SELECT
    e.name AS employee_name,
    e.salary AS employee_salary,
    m.name AS manager_name,
    m.salary AS manager_salary
FROM
    staff e
INNER JOIN
    staff m ON e.manager_id = m.id
WHERE
    e.salary > m.salary;
```

---

### 💡 Key Interview Takeaways

* **Think Aloud:** Before you start writing code, explain your approach to the interviewer. For example: "To find the second highest salary, I'll first rank all salaries using `DENSE_RANK()`, then filter where the rank is 2."
* **Know Multiple Solutions:** For a classic question like "N-th highest salary," being able to provide and discuss the trade-offs of multiple solutions (e.g., CTE vs. subquery) demonstrates a deeper level of understanding.