# 4. GroupBy and Aggregations

Aggregation allows you to perform a calculation on a set of rows and return a single summary row. The `GROUP BY` clause is used with aggregate functions to group rows that have the same values into summary rows, like "find the total sales for each product."

---

## Common Aggregate Functions

These functions operate on a set of rows to compute a single value.

* `COUNT()`: Counts the number of rows.
* `SUM()`: Calculates the sum of a set of values.
* `AVG()`: Calculates the average value.
* `MIN()`: Gets the minimum value in a set.
* `MAX()`: Gets the maximum value in a set.

---

## `GROUP BY` and `HAVING` Clauses

### `GROUP BY` Clause
The `GROUP BY` statement groups rows that have the same values into summary rows. It is almost always used with one of the aggregate functions above.

### `HAVING` Clause
The `HAVING` clause was added to SQL because the `WHERE` keyword could not be used with aggregate functions.

* **`WHERE`** filters rows **before** any groupings are made.
* **`HAVING`** filters groups **after** the aggregations have been computed.

This distinction is a critical interview topic.

---

## Practical SQL Example

Let's create a `sales` table to see these concepts in action.

```sql
CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    sale_amount DECIMAL(10, 2)
);

INSERT INTO sales (sale_id, product_name, category, sale_amount) VALUES
(1, 'Laptop', 'Electronics', 1200.00),
(2, 'Mouse', 'Electronics', 25.00),
(3, 'Desk Chair', 'Furniture', 150.00),
(4, 'Laptop', 'Electronics', 1150.00),
(5, 'SQL Book', 'Books', 45.00),
(6, 'Mouse', 'Electronics', 30.00),
(7, 'Desk Chair', 'Furniture', 140.00),
(8, 'SQL Book', 'Books', 48.00);
```

### 1. Basic Aggregations (No `GROUP BY`)
Calculates aggregates over the entire table.

```sql
SELECT
    SUM(sale_amount) AS total_revenue,
    COUNT(*) AS number_of_sales,
    AVG(sale_amount) AS average_sale_value
FROM sales;
```

### 2. `GROUP BY` Example
Calculates the total sales and number of items sold for each product category.

```sql
SELECT
    category,
    SUM(sale_amount) AS total_sales,
    COUNT(*) as items_sold
FROM sales
GROUP BY category;
```

### 3. `HAVING` Clause Example
Finds product categories with total sales greater than $200.

```sql
SELECT
    category,
    SUM(sale_amount) AS total_sales
FROM sales
GROUP BY category
HAVING SUM(sale_amount) > 200;
```

### 4. `WHERE`, `GROUP BY`, and `HAVING` together
Finds products (not categories) that have been sold more than once and have a name other than 'Laptop'.

```sql
SELECT
    product_name,
    COUNT(*) as times_sold
FROM sales
WHERE product_name != 'Laptop' -- Filter rows BEFORE grouping
GROUP BY product_name
HAVING COUNT(*) > 1; -- Filter groups AFTER grouping
```

---

### 💡 Key Interview Takeaways

* **`WHERE` vs. `HAVING`:** This is almost guaranteed to be asked. The simplest way to remember is: **`WHERE` filters rows, `HAVING` filters groups**. You cannot use an aggregate function like `SUM()` in a `WHERE` clause because `WHERE` is processed before the aggregation happens.
* **Order of Operations:** Conceptually, the database executes clauses in this order: `FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `SELECT` -> `ORDER BY`. This mental model helps you understand what's possible in each clause.

### Common Interview Questions

1.  **What is the fundamental difference between the `WHERE` and `HAVING` clauses?**
    * *Answer:* `WHERE` filters individual rows before they are grouped or aggregated. `HAVING` filters entire groups of rows after they have been aggregated based on the result of an aggregate function.
2.  **What is the purpose of the `GROUP BY` clause?**
    * *Answer:* It groups rows that have the same values into summary rows. This allows aggregate functions like `COUNT()` or `SUM()` to operate on each group independently, rather than on the entire table.
3.  **Can you use an aggregate function like `AVG()` in a `WHERE` clause? Why or why not?**
    * *Answer:* No. The `WHERE` clause is evaluated before the `GROUP BY` clause and any aggregations are computed. Therefore, the result of the `AVG()` function doesn't exist at the time `WHERE` is being processed. You would use the `HAVING` clause for that.