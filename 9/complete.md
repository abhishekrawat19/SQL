# Complete SQL Notes for Interviews

This document contains a comprehensive set of notes covering fundamental to advanced SQL concepts. It is designed for interview preparation for roles such as Full-Stack Developer, Data Analyst, and Machine Learning Engineer. The topics range from basic DDL and DML commands to advanced concepts like joins, subqueries, window functions, and normalization.

---

### Table of Contents
* [DAY 1: Introduction to SQL and Databases](#day-1-introduction-to-sql-and-databases)
* [DAY 2: Relational Model and Datatypes](#day-2-relational-model-and-datatypes)
* [DAY 3: Numeric and Date Datatypes](#day-3-numeric-and-date-datatypes)
* [DAY 4: Constraints](#day-4-constraints)
* [DAY 5: Data Query Language (DQL)](#day-5-data-query-language-dql)
* [DAY 6: Expressions, Aliases, and Selection](#day-6-expressions-aliases-and-selection)
* [DAY 7: SQL Operators](#day-7-sql-operators)
* [DAY 8: Special Operators](#day-8-special-operators)
* [DAY 9: Functions](#day-9-functions)
* [DAY 10: Grouping and Filtering](#day-10-grouping-and-filtering)
* [DAY 11: Subqueries](#day-11-subqueries)
* [DAY 12: Advanced Subqueries](#day-12-advanced-subqueries)
* [DAY 13: Types of Subqueries](#day-13-types-of-subqueries)
* [DAY 14: Employee and Manager Relations](#day-14-employee-and-manager-relations)
* [DAY 15-16: Joins](#day-15-16-joins)
* [DAY 17: Correlated Subqueries](#day-17-correlated-subqueries)
* [DAY 18-19: Single-Row Functions](#day-18-19-single-row-functions)
* [DAY 20-21: DDL, DML, & TCL](#day-20-21-ddl-dml--tcl)
* [DAY 22: Normalization](#day-22-normalization)

---

## DAY 1: Introduction to SQL and Databases
_Thursday, July 16, 2020_

### SQL (Structured Query Language)
SQL is the standard language used to communicate and interact with a relational database management system (RDBMS).

### What is Data?
> "Data is a raw fact which describes the attributes of an Entity."

An **Entity** is any real-world object, and **Attributes** are its properties.
* **Entity: A Person**
    * **Attributes:** First name, Surname, Phone number, DOB
* **Entity: A Laptop**
    * **Attributes:** Brand, RAM, Touch screen

### Database
> "A Database is a place or a medium in which we store data in a systematic and organized manner."

The basic operations that can be performed on a database are referred to as **"CRUD" Operations**:
* **C**reate / **I**nsert
* **R**ead / **R**etrieve
* **U**pdate / **M**odify
* **D**elete / **D**rop

### Database Management System (DBMS)
> "It is a software which is used to maintain and manage the database."

A DBMS provides important features like **security** and **authorization**.

### Relational Database Management System (RDBMS)
> "It is a type of DBMS software in which we store the data in the form of Tables (rows & columns)."

An RDBMS that follows the **Relational Model** (designed by E.F. Codd) stores all data, including metadata, in tables.

---

## DAY 2: Relational Model and Datatypes
_Friday, July 17, 2020_

### Table
> "A Table is a logical organization of data which consists of Columns & Rows."

| Columns / Attributes / Fields | | |
| :--- | :--- | :--- |
| **EID** | **ENAME** | **SALARY** |
| 1 | SMITH | 1000 |
| **Rows / Records / Tuples** | | |

### Rules of E.F. Codd (for Relational Model)
1.  **Data in a cell must be single-valued (atomic).** You cannot store multiple values in a single cell.
2.  **Data can be stored in multiple tables.** A connection can be established between tables using a **Key Attribute**.
3.  **Everything is stored in tables, including Metadata** (data about data).
4.  **Data is validated in two steps:** by assigning **Datatypes** (Mandatory) and **Constraints** (Optional).

### SQL Datatypes
A datatype specifies the type of data that a column can hold.
* **`CHAR(size)`**: Fixed-length string. Can waste memory.
* **`VARCHAR(size)` / `VARCHAR2(size)`**: Variable-length string. More memory efficient.

| Feature | `CHAR` | `VARCHAR` / `VARCHAR2` |
| :--- | :--- | :--- |
| **Memory Allocation**| Fixed-Length | Variable-Length |
| **Memory Usage** | Can waste memory | Efficient memory usage |
| **Use Case**| Fixed-size data (e.g., PAN card) | Variable-size data (e.g., names) |

---

## DAY 3: Numeric and Date Datatypes
_Monday, July 20, 2020_

### `NUMBER(precision, scale)`
Used to store numeric values.
* **Precision:** The total number of digits.
* **Scale:** The number of digits to the right of the decimal point.

### `DATE`
Used to store dates. In Oracle, the default format is `'DD-MON-YY'`.

### Large Objects (LOBs)
* **`CLOB` (Character Large Object):** Used to store large blocks of text (up to 4GB).
* **`BLOB` (Binary Large Object):** Used to store binary files like images or videos (up to 4GB).

---

## DAY 4: Constraints
_Tuesday, July 21, 2020_

### Constraints
> "A constraint is a rule given to a column for validation."
1.  **`UNIQUE`**: Prevents duplicate values.
2.  **`NOT NULL`**: Ensures a column cannot have an empty (`NULL`) value.
3.  **`CHECK`**: Provides validation with a condition (e.g., `CHECK (Salary > 0)`).
4.  **`PRIMARY KEY`**: Uniquely identifies each record. It is a combination of `UNIQUE` and `NOT NULL`.
5.  **`FOREIGN KEY`**: Establishes a connection between two tables.

### Primary Key vs. Foreign Key

| Feature | `PRIMARY KEY` (PK) | `FOREIGN KEY` (FK) |
| :--- | :--- | :--- |
| **Purpose** | Uniquely identify a record in its table. | Establish a link between two tables. |
| **NULL Values** | Cannot accept `NULL`. | Can accept `NULL`. |
| **Quantity per Table** | Only **one** PK per table. | Can have **multiple** FKs in a table. |

### The `NULL` Keyword
`NULL` is a keyword used to represent a missing or empty value. It is not the same as 0 or a blank space.

---

## DAY 5: Data Query Language (DQL)
_Wednesday, July 22, 2020_

### Overview of SQL Statements
1.  **DDL** (Data Definition Language)
2.  **DML** (Data Manipulation Language)
3.  **TCL** (Transaction Control Language)
4.  **DCL** (Data Control Language)
5.  **DQL** (Data Query Language)

### DQL Concepts
* **Projection:** Retrieving data by selecting specific columns.
* **Selection:** Retrieving data by filtering for specific rows.
* **Join:** Retrieving data from multiple tables.

### `SELECT` Statement
**Syntax:**
```sql
SELECT * / [DISTINCT] column_name / expression [AS alias]
FROM table_name;
```
**Order of Execution:** 1. `FROM`, 2. `SELECT`.

### `DISTINCT` Clause
> "It is used to remove duplicate or repeated values from the result table."
```sql
SELECT DISTINCT BRANCH FROM STUDENT;
```

---

## DAY 6: Expressions, Aliases, and Selection
_Thursday, July 23, 2020_

### Expressions
An expression is a combination of operands and operators (e.g., `SAL * 12`).

### Alias
An alias is a temporary, alternate name for a column or expression.
```sql
SELECT SAL * 12 AS Annual_Salary FROM EMP;
```

### Selection (`WHERE` Clause)
The `WHERE` clause is used to filter records based on a condition.
**Order of Execution:** 1. `FROM`, 2. `WHERE`, 3. `SELECT`.
```sql
SELECT ENAME FROM EMP WHERE SAL > 3000;
```

---

## DAY 7: SQL Operators
_Friday, July 24, 2020_

### Operator Categories
* **Arithmetic:** `+`, `-`, `*`, `/`
* **Concatenation:** `||` (joins strings)
* **Comparison:** `=`, `!=`, `<>`
* **Relational:** `>`, `<`, `>=`, `<=`
* **Logical:** `AND`, `OR`, `NOT`
* **Special:** `IN`, `BETWEEN`, `IS NULL`, `LIKE`

### Logical Operators (`AND`, `OR`)
Used to combine multiple conditions in a `WHERE` clause. Use parentheses `()` to control the order of logic.
```sql
SELECT ENAME, JOB, DEPTNO
FROM EMP
WHERE JOB = 'MANAGER' AND (DEPTNO = 10 OR DEPTNO = 20);
```

---

## DAY 8: Special Operators
_Monday, July 27, 2020_

* **`IN`**: Checks if a value matches any value in a list. Shorthand for multiple `OR`s.
  ```sql
  SELECT ENAME FROM EMP WHERE DEPTNO IN (10, 30);
  ```
* **`BETWEEN`**: Selects values within an inclusive range.
  ```sql
  SELECT ENAME FROM EMP WHERE SAL BETWEEN 1000 AND 3000;
  ```
* **`IS NULL` / `IS NOT NULL`**: Checks for the presence or absence of null values.
  ```sql
  SELECT ENAME FROM EMP WHERE COMM IS NULL;
  ```
* **`LIKE`**: Used for pattern matching in strings with wildcards:
    * `%`: Represents zero or more characters.
    * `_`: Represents a single character.
  ```sql
  SELECT ENAME FROM EMP WHERE ENAME LIKE 'S%'; -- Starts with S
  ```

---

## DAY 9: Functions
_Tuesday, July 28, 2020_

### Multi-Row (Aggregate) Functions
These functions operate on a group of rows and return a single result.
* `MAX()`: Maximum value.
* `MIN()`: Minimum value.
* `SUM()`: Sum of values.
* `AVG()`: Average of values.
* `COUNT()`: Number of values.

**Key Rule:** Aggregate functions **cannot** be used in a `WHERE` clause.

```sql
SELECT MAX(SAL) FROM EMP WHERE JOB = 'MANAGER';
```

---

## DAY 10: Grouping and Filtering
_Wednesday, July 29, 2020_

### `GROUP BY` Clause
Arranges identical data into groups, often used with aggregate functions.
```sql
-- Find the number of employees in each department
SELECT DEPTNO, COUNT(*) FROM EMP GROUP BY DEPTNO;
```

### `HAVING` Clause
Filters groups based on the results of aggregate functions.

### `WHERE` vs. `HAVING`
| `WHERE` Clause | `HAVING` Clause |
| :--- | :--- |
| Filters **rows** | Filters **groups** |
| Executes **before** `GROUP BY` | Executes **after** `GROUP BY` |
| **Cannot** use aggregate functions | **Can** use aggregate functions |

```sql
-- Find departments with at least 3 employees
SELECT DEPTNO, COUNT(*)
FROM EMP
GROUP BY DEPTNO
HAVING COUNT(*) >= 3;
```

---

## DAY 11: Subqueries
_Thursday, July 30, 2020_

> "A query written inside another query is known as a Subquery."

The inner query executes first, and its result is used by the outer query.
```sql
-- Find employees earning less than 'MILLER'
SELECT ENAME FROM EMP WHERE SAL < (SELECT SAL FROM EMP WHERE ENAME = 'MILLER');
```

---

## DAY 12: Advanced Subqueries
_Saturday, August 1, 2020_

Subqueries are powerful for cross-table conditions where the filter criteria for one table depends on a value from another table.
```sql
-- Find the department name of 'MILLER'
SELECT DNAME FROM DEPT WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'MILLER');
```

---

## DAY 13: Types of Subqueries
_Monday, August 3, 2020_

* **Single-Row Subquery:** Returns one value. Can use operators like `=, >, <`.
* **Multi-Row Subquery:** Returns multiple values. Must use operators like `IN, ANY, ALL`.
* **Nested Subquery:** A subquery within a subquery, often used to find Nth highest/lowest values.
```sql
-- Find the second highest salary
SELECT MAX(SAL) FROM EMP WHERE SAL < (SELECT MAX(SAL) FROM EMP);
```

---

## DAY 14: Employee and Manager Relations
_Tuesday, August 4, 2020_

Subqueries are essential for navigating hierarchical relationships in the same table.
```sql
-- Find the name of Allen's manager
SELECT ENAME FROM EMP WHERE EMPNO = (SELECT MGR FROM EMP WHERE ENAME = 'ALLEN');

-- Find employees reporting to 'KING'
SELECT ENAME FROM EMP WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'KING');
```

---

## DAY 15-16: Joins
_Wednesday, Aug 5 - Thursday, Aug 6, 2020_

> "A Join is the process of retrieving data from multiple tables simultaneously."
* **`INNER JOIN`**: Returns only matching records from both tables.
* **`LEFT JOIN`**: Returns all records from the left table and matching records from the right.
* **`RIGHT JOIN`**: Returns all records from the right table and matching records from the left.
* **`FULL OUTER JOIN`**: Returns all records from both tables.
* **`SELF JOIN`**: A table is joined to itself to query hierarchical data.
```sql
-- Self Join to find manager names
SELECT E1.ENAME AS Employee, E2.ENAME AS Manager
FROM EMP E1 JOIN EMP E2 ON E1.MGR = E2.EMPNO;
```

---

## DAY 17: Correlated Subqueries
_Friday, August 7, 2020_

> "A subquery where the inner query and the outer query are dependent on each other."

The inner query is evaluated once for each row of the outer query. Often used with `EXISTS` and `NOT EXISTS`.
```sql
-- Find departments that have at least one employee
SELECT DNAME FROM DEPT d WHERE EXISTS (SELECT 1 FROM EMP e WHERE e.DEPTNO = d.DEPTNO);
```

---

## DAY 18-19: Single-Row Functions
_Monday, Aug 10 - Tuesday, Aug 11, 2020_

These functions operate on a single row and return one result per row.

### String Functions
* `LENGTH()`, `CONCAT()`, `UPPER()`, `LOWER()`, `INITCAP()`, `REVERSE()`
* **`SUBSTR('string', pos, [len])`**: Extracts a substring.
* **`INSTR('string', 'substring')`**: Finds the position of a substring.
* **`REPLACE('string', 'search', ['replace'])`**: Replaces a substring.

### Numeric & Date Functions
* `MOD()`, `ROUND()`, `TRUNC()`
* `SYSDATE`, `MONTHS_BETWEEN()`, `LAST_DAY()`
* **`TO_CHAR(date, 'format')`**: Converts a date to a string.
* **`NVL(col, val)`**: Replaces a `NULL` value with a specified value.

---

## DAY 20-21: DDL, DML, & TCL
_Wednesday, Aug 12 - Thursday, Aug 13, 2020_

### DDL (Data Definition Language)
Manages the structure of database objects. Statements are **auto-commit**.
* `CREATE`, `ALTER`, `RENAME`, `DROP`, `TRUNCATE`

### DML (Data Manipulation Language)
Manages the data within objects. These are transactions.
* `INSERT`, `UPDATE`, `DELETE`

### TCL (Transaction Control Language)
Manages DML transactions.
* `COMMIT`: Saves transactions.
* `ROLLBACK`: Undoes transactions.
* `SAVEPOINT`: Creates a point to roll back to.

---

## DAY 22: Normalization
_Friday, August 14, 2020_

> "Normalization is the process of reducing a large table into smaller tables to remove data redundancy and improve data integrity."

### Normal Forms
* **1NF (First Normal Form):** Ensures cells hold single values (atomicity).
* **2NF (Second Normal Form):** Is in 1NF and has no partial dependencies.
* **3NF (Third Normal Form):** Is in 2NF and has no transitive dependencies.

A table is generally considered normalized if it is in **3NF**.