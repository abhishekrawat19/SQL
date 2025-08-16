
---

## DAY 1: Introduction to SQL and Databases


### SQL (Structured Query Language)

SQL is the standard language used to communicate and interact with a relational database management system (RDBMS).

---

### What is Data?

> "Data is a raw fact which describes the attributes of an Entity."

An **Entity** is any real-world object, and **Attributes** are its properties.

* **Entity: A Person**
    * **Attributes:**
        * First name: Rohan
        * Surname: Singh
        * Phone number: 9876543210
        * DOB: 14-MAY-199X
* **Entity: A Laptop**
    * **Attributes:**
        * Brand: Dell
        * RAM: 8gb
        * Touch: no
* **Entity: A Water Bottle**
    * **Attributes:**
        * Height: 20cms
        * Color: blue
        * Capacity: 500ml

---

### Database

> "A Database is a place or a medium in which we store data in a systematic and organized manner."

The basic operations that can be performed on a database are referred to as **"CRUD" Operations**:
* **C**reate / **I**nsert
* **R**ead / **R**etrieve
* **U**pdate / **M**odify
* **D**elete / **D**rop

---

### Database Management System (DBMS)

> "It is a software which is used to maintain and manage the database."

A DBMS provides important features like **security** and **authorization**. We use a query language to communicate with the DBMS.



---

### Relational Database Management System (RDBMS)

> "It is a type of DBMS software in which we store the data in the form of Tables (rows & columns)."

An RDBMS that follows the **Relational Model** (designed by E.F. Codd) stores all data, including metadata, in tables.

* **DBMS:** Stores data in files.
* **RDBMS:** Stores data in tables.

---

## DAY 2: Relational Model and Datatypes


### Table
> "A Table is a logical organization of data which consists of Columns & Rows."

| Columns / Attributes / Fields | | |
| :--- | :--- | :--- |
| **EID** | **ENAME** | **SALARY** |
| 1 | SMITH | 1000 |
| 2 | ALLEN | 1500 |
| 3 | CLARK | 2000 |
| **Rows / Records / Tuples** | | |

---

### Rules of E.F. Codd (for Relational Model)

1.  **Data in a cell must be single-valued (atomic).** You cannot store multiple values in a single cell.

    * **Incorrect:**
        | EID | ENAME | PHONE_NO |
        | :-- | :--- | :--- |
        | 2 | ALLEN | 102, 202 |

    * **Correct:**
        | EID | ENAME | PHONE_NO | ALTERNATE_NO |
        | :-- | :--- | :--- | :--- |
        | 2 | ALLEN | 102 | 202 |

2.  **Data can be stored in multiple tables.** If needed, a connection can be established between tables using a **Key Attribute**.

3.  **Everything is stored in tables, including Metadata.**
    * **Metadata:** Data about data. For example, the details of an image file (name, size, format) are its metadata.

4.  **Data entered into a table is validated in two steps:**
    * By assigning **Datatypes** (Mandatory).
    * By assigning **Constraints** (Optional).

---

### SQL Datatypes
A datatype specifies the type of data that a column can hold. **Note:** SQL is not a case-sensitive language.

1.  **`CHAR(size)`**
    * Stores characters: 'A-Z', 'a-z', '0-9', and special characters.
    * Characters must be enclosed in single quotes (e.g., `'QSP'`).
    * Size is mandatory and specifies the exact number of characters. Max size is 2000 characters.
    * Follows **fixed-length** memory allocation. If you define `CHAR(8)` and store "QSP", it still uses all 8 characters of memory, leading to potential memory wastage.

2.  **`VARCHAR(size)` / `VARCHAR2(size)`**
    * Stores the same types of characters as `CHAR`.
    * Follows **variable-length** memory allocation. If you define `VARCHAR(8)` and store "QSP", it only uses 3 characters of memory, freeing the rest.
    * `VARCHAR2` is an updated version (common in Oracle) that can store up to 4000 characters.

| Feature | `CHAR` | `VARCHAR` / `VARCHAR2` |
| :--- | :--- | :--- |
| **Memory Allocation**| Fixed-Length | Variable-Length |
| **Memory Usage** | Can waste memory | Efficient memory usage |
| **Max Size** | 2000 characters | 2000 / 4000 characters |
| **Use Case**| Fixed-size data (e.g., PAN card, USN) | Variable-size data (e.g., names, addresses) |

---

## DAY 3: Numeric and Date Datatypes


### `NUMBER(precision, scale)`
Used to store numeric values.

* **Precision:** The total number of digits.
* **Scale:** The number of digits to the right of the decimal point. It is optional and defaults to 0.

* `NUMBER(3)`: Stores integers up to +/- 999.
* `NUMBER(5, 2)`: Stores numbers up to +/- 999.99.
* `NUMBER(4, 4)`: Stores numbers up to +/- .9999.

### `DATE`
Used to store dates. In Oracle, the default format is `'DD-MON-YY'` (e.g., `'22-JUN-20'`).

### Large Objects (LOBs)
Used to store large amounts of data up to 4GB.

1.  **`CLOB` (Character Large Object):** Used to store large blocks of text.
2.  **`BLOB` (Binary Large Object):** Used to store binary files like images, audio, or video.

---

## DAY 4: Constraints

### Constraints
> "A constraint is a rule given to a column for validation."

1.  **`UNIQUE`**: Prevents duplicate values in a column.
2.  **`NOT NULL`**: Ensures a column cannot have an empty (`NULL`) value.
3.  **`CHECK`**: Provides extra validation with a condition (e.g., `CHECK (Salary > 0)`).
4.  **`PRIMARY KEY`**: Uniquely identifies each record in a table. It is a combination of `UNIQUE` and `NOT NULL`.
5.  **`FOREIGN KEY`**: Establishes a connection between two tables, linking a column in a child table to a primary key in a parent table.

### Primary Key vs. Foreign Key

| Feature | `PRIMARY KEY` (PK) | `FOREIGN KEY` (FK) |
| :--- | :--- | :--- |
| **Purpose** | Uniquely identify a record in its table. | Establish a link between two tables. |
| **Uniqueness** | Cannot accept duplicate values. | Can accept duplicate values. |
| **NULL Values** | Cannot accept `NULL`. | Can accept `NULL`. |
| **Quantity per Table** | Only **one** PK per table. | Can have **multiple** FKs in a table. |
| **Underlying Rule** | Combination of `UNIQUE` and `NOT NULL`. | No underlying combination. |

### The `NULL` Keyword
`NULL` is a keyword used to represent a missing or empty value in a cell.
* `NULL` is not the same as 0 or a blank space.
* Any arithmetic operation performed on `NULL` results in `NULL`.
* `NULL` does not occupy any memory.

---

## DAY 5: Data Query Language (DQL)

### Overview of SQL Statements
SQL commands are broadly categorized into the following languages:
1.  **DDL** (Data Definition Language)
2.  **DML** (Data Manipulation Language)
3.  **TCL** (Transaction Control Language)
4.  **DCL** (Data Control Language)
5.  **DQL** (Data Query Language)

### Data Query Language (DQL)
> "DQL is used to retrieve data from the database."

The primary command in DQL is `SELECT`. Its usage involves the following concepts:
1.  **SELECT:** The keyword to retrieve data.
2.  **Projection:** Retrieving data by selecting specific columns.
3.  **Selection:** Retrieving data by filtering for specific rows.
4.  **Join:** Retrieving data from multiple tables simultaneously.

### Projection
> "Projection is a process of retrieving data by selecting only the columns."

In a projection, all rows for the selected columns are returned by default.

**Syntax:**
```sql
SELECT * / [DISTINCT] column_name / expression [AS alias]
FROM table_name;
```
**Order of Execution:**
1.  `FROM` Clause
2.  `SELECT` Clause

The `FROM` clause executes first. It finds the specified table in the database and makes it available for the query. The `SELECT` clause then executes, picking the specified columns from that table to create the final result.

**Example:** "Write a query to display names of all the students."

* **Student Table:**
| SID | SNAME | BRANCH | PER |
| :-- | :---- | :----- | :-- |
| 1 | A | ECE | 60 |
| 2 | B | CSE | 75 |
| 3 | C | ME | 50 |
| 4 | D | ECE | 80 |
| 5 | C | CSE | 75 |
| 6 | E | CIVIL | 95 |

* **Query:**
```sql
SELECT SNAME
FROM STUDENT;
```

* **Result:**
| SNAME |
| :---- |
| A |
| B |
| C |
| D |
| C |
| E |


#### More Projection Examples

* **Display student ID and names:**
    ```sql
    SELECT SID, SNAME
    FROM STUDENT;
    ```
* **Display all details from the student table:**
    ```sql
    SELECT *
    FROM STUDENT;
    ```
* **Display employee name, salary, and commission from the `emp` table:**
    ```sql
    SELECT ename, sal, comm
    FROM emp;
    ```

### The `DISTINCT` Clause
> "It is used to remove duplicate or repeated values from the result table."

`DISTINCT` must be the first argument in the `SELECT` clause. It can be used on single or multiple columns to remove duplicate rows based on the combination of those columns.

* **Query for unique branches:**
    ```sql
    SELECT DISTINCT BRANCH
    FROM STUDENT;
    ```
* **Result:**
| BRANCH |
| :----- |
| ECE |
| CSE |
| ME |
| CIVIL |

* **Query for unique combinations of branch and percentage:**
    ```sql
    SELECT DISTINCT BRANCH, PER
    FROM STUDENT;
    ```
* **Result:**
| BRANCH | PER |
| :----- | :-- |
| ECE | 60 |
| CSE | 75 |
| ME | 50 |
| ECE | 80 |
| CIVIL | 95 |

---


## DAY 6: Expressions, Aliases, and Selection

### Expressions
> "A statement which gives a result is known as an Expression."

An expression is a combination of operands (values) and operators (symbols like `+`, `*`).

* **Display employee name and annual salary:**
    ```sql
    SELECT ENAME, SAL * 12
    FROM EMP;
    ```
* **Display employee name and salary with a 20% hike:**
    ```sql
    SELECT ENAME, SAL + SAL * 20/100
    FROM EMP;
    ```

### Alias
> "An alias is an alternate name given to a column or an expression in the result table."

You can assign an alias with or without the `AS` keyword. If an alias contains spaces, it must be enclosed in double quotes.

* **Example without `AS`:**
    ```sql
    SELECT SAL * 12 Annual_Salary
    FROM EMP;
    ```
* **Example with `AS` and double quotes:**
    ```sql
    SELECT SAL - SAL * 32/100 AS "Deduction Amount"
    FROM EMP;
    ```

### Selection
> "Selection is a process of retrieving data by selecting both columns and rows."

Selection is achieved by adding a `WHERE` clause to the query.

**Syntax:**
```sql
SELECT * / [DISTINCT] column_name / expression [AS alias]
FROM table_name
WHERE condition;
```
**Order of Execution:**
1.  `FROM`
2.  `WHERE`
3.  `SELECT`

The `WHERE` clause is used to filter records. It is executed after `FROM` but before `SELECT`.

* **Display names of employees earning more than 300:**
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE SAL > 300;
    ```
* **Display details of the employee whose name is 'MILLER':**
    ```sql
    SELECT *
    FROM EMP
    WHERE ENAME = 'MILLER';
    ```
* **Display employees hired before 1985:**
    ```sql
    SELECT ENAME, SAL, HIREDATE
    FROM EMP
    WHERE HIREDATE < '01-JAN-1985';
    ```

---

## DAY 7: SQL Operators


### Operator Categories
1.  **Arithmetic:** `+`, `-`, `*`, `/`
2.  **Concatenation:** `||`
3.  **Comparison:** `=`, `!=`, `<>`
4.  **Relational:** `>`, `<`, `>=`, `<=`
5.  **Logical:** `AND`, `OR`, `NOT`
6.  **Special:** `IN`, `BETWEEN`, `IS NULL`, `LIKE`

### Concatenation Operator (`||`)
> "It is used to join strings."

* **Example:**
    ```sql
    SELECT 'Hi ' || ename AS Greeting
    FROM EMP
    WHERE JOB = 'MANAGER';
    ```
* **Result:**
| GREETING |
| :--- |
| Hi ALLEN |
| Hi MARTIN |
| Hi SMITH |

### Logical Operators (`AND`, `OR`, `NOT`)
Used to combine multiple conditions in a `WHERE` clause.
* **`AND`**: All conditions must be true.
* **`OR`**: At least one of the conditions must be true.

* **Display employees working as a MANAGER in department 10:**
    ```sql
    SELECT ENAME, DEPTNO, JOB
    FROM EMP
    WHERE JOB = 'MANAGER' AND DEPTNO = 10;
    ```
* **Display employees working in department 10 or 20:**
    ```sql
    SELECT ENAME, DEPTNO
    FROM EMP
    WHERE DEPTNO = 10 OR DEPTNO = 20;
    ```
* **Display employees working as a MANAGER in either department 10 or 20.** (Note the use of parentheses to control the order of logic).
    ```sql
    SELECT ENAME, JOB, DEPTNO
    FROM EMP
    WHERE JOB = 'MANAGER' AND (DEPTNO = 10 OR DEPTNO = 20);
    ```
* **Display employees who are a CLERK or a MANAGER in department 10:**
    ```sql
    SELECT ENAME, JOB, DEPTNO
    FROM EMP
    WHERE (JOB = 'CLERK' OR JOB = 'MANAGER') AND DEPTNO = 10;
    ```


---

## DAY 8: Special Operators

Special operators are used in the `WHERE` clause to perform operations beyond standard comparisons.

### 1. `IN` Operator
> `IN` is a multi-valued operator that checks if a value matches any value in a given list. It's a shorthand for multiple `OR` conditions.

**Syntax:** `column_name IN (value1, value2, ...)`

* **Task:** Display the name and department number of employees working in department 10 or 30.
    * **Using `OR`:**
        ```sql
        SELECT ENAME, DEPTNO FROM EMP WHERE DEPTNO = 10 OR DEPTNO = 30;
        ```
    * **Using `IN`:**
        ```sql
        SELECT ENAME, DEPTNO FROM EMP WHERE DEPTNO IN (10, 30);
        ```

* **Task:** Display the name and job of employees working as a 'CLERK', 'MANAGER', or 'SALESMAN'.
    ```sql
    SELECT ENAME, JOB
    FROM EMP
    WHERE JOB IN ('CLERK', 'MANAGER', 'SALESMAN');
    ```

### 2. `NOT IN` Operator
> `NOT IN` is the opposite of `IN`. It checks if a value does **not** match any value in a given list.

**Syntax:** `column_name NOT IN (value1, value2, ...)`

* **Task:** Display the name and department number of all employees except those working in department 10 or 40.
    ```sql
    SELECT ENAME, DEPTNO
    FROM EMP
    WHERE DEPTNO NOT IN (10, 40);
    ```

* **Task:** Display employees in department 20 who are not a 'CLERK' or 'MANAGER'.
    ```sql
    SELECT ENAME, DEPTNO, JOB
    FROM EMP
    WHERE DEPTNO = 20 AND JOB NOT IN ('CLERK', 'MANAGER');
    ```

### 3. `BETWEEN` Operator
> `BETWEEN` is used to select values within a given range. The range is inclusive (includes the start and end values).

**Syntax:** `column_name BETWEEN lower_range AND upper_range`

* **Task:** Display employees earning a salary in the range of 1000 to 3000.
    ```sql
    SELECT ENAME, SAL
    FROM EMP
    WHERE SAL BETWEEN 1000 AND 3000;
    ```
* **Task:** Display employees in department 10 who were hired anytime during the year 2019.
    ```sql
    SELECT ENAME, DEPTNO
    FROM EMP
    WHERE DEPTNO = 10 AND HIREDATE BETWEEN '01-JAN-2019' AND '31-DEC-2019';
    ```

### 4. `NOT BETWEEN` Operator
> `NOT BETWEEN` is the opposite of `BETWEEN`. It selects values outside the given range.

**Syntax:** `column_name NOT BETWEEN lower_range AND upper_range`

* **Task:** Display employees not earning a salary in the range of 1000 to 3000.
    ```sql
    SELECT ENAME, SAL
    FROM EMP
    WHERE SAL NOT BETWEEN 1000 AND 3000;
    ```

### 5. `IS NULL` Operator
> `IS NULL` is used to check for `NULL` (empty) values. You cannot use `= NULL`.

**Syntax:** `column_name IS NULL`

* **Task:** Display the names of employees who do not get a commission.
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE COMM IS NULL;
    ```

### 6. `IS NOT NULL` Operator
> `IS NOT NULL` is used to check for non-empty values.

**Syntax:** `column_name IS NOT NULL`

* **Task:** Display the names of employees who are getting a salary.
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE SAL IS NOT NULL;
    ```

### 7. `LIKE` Operator
> `LIKE` is used for pattern matching in string data. It uses two special wildcard characters:

* `%` (Percent): Represents zero, one, or multiple characters.
* `_` (Underscore): Represents a single character.

**Syntax:** `column_name LIKE 'pattern'`

* **Task:** Find employees whose name starts with 'S'.
    ```sql
    SELECT * FROM EMP WHERE ENAME LIKE 'S%';
    ```
* **Task:** Find employees whose name ends with 'S'.
    ```sql
    SELECT * FROM EMP WHERE ENAME LIKE '%S';
    ```
* **Task:** Find employees who have the character 'S' anywhere in their name.
    ```sql
    SELECT * FROM EMP WHERE ENAME LIKE '%S%';
    ```
* **Task:** Find employees whose name has 'A' as the second character.
    ```sql
    SELECT ENAME FROM EMP WHERE ENAME LIKE '_A%';
    ```
* **Task:** Find employees whose name contains at least two 'A's.
    ```sql
    SELECT ENAME FROM EMP WHERE ENAME LIKE '%A%A%';
    ```
* **Task:** Find employees hired in November.
    ```sql
    SELECT ENAME FROM EMP WHERE HIREDATE LIKE '%NOV%';
    ```

### 8. `NOT LIKE` Operator
> `NOT LIKE` is the opposite of `LIKE`. It finds strings that do not match the specified pattern.

---

## DAY 9: Functions
_Tuesday, July 28, 2020_

> **Functions** are blocks of code or instructions used to perform a specific task.

### Types of Functions in SQL
1.  **Single Row Functions:** Operate on a single row and return one result per row.
2.  **Multi-Row Functions:** Operate on a group of rows and return a single result for the entire group. Also known as **Aggregate** or **Group** functions.

### Multi-Row (Aggregate) Functions
These functions take multiple inputs (a set of rows) and return a single output.

**List of Aggregate Functions:**
* `MAX()`: Returns the maximum value in a column.
* `MIN()`: Returns the minimum value in a column.
* `SUM()`: Returns the sum of all values in a column.
* `AVG()`: Returns the average of the values in a column.
* `COUNT()`: Returns the number of values in a column.

#### Key Rules for Aggregate Functions
* They can only accept one argument (a column name or an expression).
* You cannot select an individual column alongside an aggregate function without using a `GROUP BY` clause.
* All aggregate functions ignore `NULL` values.
* Aggregate functions **cannot** be used in a `WHERE` clause.
* `COUNT()` is the only aggregate function that can accept `*` as an argument (`COUNT(*)` counts all rows).

#### Examples

* **Task:** Find the maximum salary given to a 'MANAGER'.
    ```sql
    SELECT MAX(SAL)
    FROM EMP
    WHERE JOB = 'MANAGER';
    ```
* **Task:** Find the total salary given to employees in department 10.
    ```sql
    SELECT SUM(SAL)
    FROM EMP
    WHERE DEPTNO = 10;
    ```
* **Task:** Find the number of employees earning more than 1500 in department 20.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE SAL > 1500 AND DEPTNO = 20;
    ```
* **Task:** Find the number of employees who receive a commission.
    * **Method 1:**
        ```sql
        SELECT COUNT(*) FROM EMP WHERE COMM IS NOT NULL;
        ```
    * **Method 2 (more direct):**
        ```sql
        SELECT COUNT(COMM) FROM EMP;
        ```

---

## Solved Assignment: Multi-Row Functions (MRF)

Here are the solved problems for the Multi-Row Functions assignment.

1.  **Task:** Find the number of employees getting a salary less than 2000 in department 10.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE DEPTNO = 10 AND SAL < 2000;
    ```

2.  **Task:** Find the total salary needed to pay employees working as 'CLERK'.
    ```sql
    SELECT SUM(SAL)
    FROM EMP
    WHERE JOB = 'CLERK';
    ```

3.  **Task:** Find the average salary needed to pay all employees.
    ```sql
    SELECT AVG(SAL)
    FROM EMP;
    ```

4.  **Task:** Find the number of employees having 'A' as their first character.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE ENAME LIKE 'A%';
    ```

5.  **Task:** Find the number of employees working as 'CLERK' or 'MANAGER'.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE JOB IN ('MANAGER', 'CLERK');
    ```

6.  **Task:** Find the total salary needed to pay employees hired in February.
    ```sql
    SELECT SUM(SAL)
    FROM EMP
    WHERE HIREDATE LIKE '%FEB%';
    ```

7.  **Task:** Find the number of employees reporting to manager 7839.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE MGR = 7839;
    ```

8.  **Task:** Find the number of employees getting a commission in department 30.
    ```sql
    SELECT COUNT(COMM)
    FROM EMP
    WHERE DEPTNO = 30;
    ```

9.  **Task:** Find the avg salary, total salary, number of employees, and maximum salary for employees working as 'PRESIDENT'.
    ```sql
    SELECT AVG(SAL), SUM(SAL), COUNT(*), MAX(SAL)
    FROM EMP
    WHERE JOB = 'PRESIDENT';
    ```

10. **Task:** Find the number of employees having 'A' in their names.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE ENAME LIKE '%A%';
    ```

11. **Task:** Find the number of employees and total salary for employees who have two consecutive 'L's in their names.
    ```sql
    SELECT COUNT(*), SUM(SAL)
    FROM EMP
    WHERE ENAME LIKE '%LL%';
    ```

12. **Task:** Find the number of distinct departments present in the employee table.
    ```sql
    SELECT COUNT(DISTINCT DEPTNO)
    FROM EMP;
    ```

13. **Task:** Find the number of employees having the character `_` (underscore) in their names.
    *Note: The `ESCAPE` clause is used to treat the wildcard `_` as a literal character.*
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE ENAME LIKE '%!_%' ESCAPE '!';
    ```

14. **Task:** Find the number of employees having at least one `%` (percentile) in their names.
    *Note: The `ESCAPE` clause is used to treat the wildcard `%` as a literal character.*
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE ENAME LIKE '%!%%' ESCAPE '!';
    ```

15. **Task:** Find the total salary for employees working as 'CLERK' in department 30.
    ```sql
    SELECT SUM(SAL)
    FROM EMP
    WHERE JOB = 'CLERK' AND DEPTNO = 30;
    ```

16. **Task:** Find the maximum salary given to employees working as 'ANALYST'.
    ```sql
    SELECT MAX(Sal)
    FROM EMP
    WHERE JOB = 'ANALYST';
    ```

17. **Task:** Find the number of distinct salaries present in the employee table.
    ```sql
    SELECT COUNT(DISTINCT SAL)
    FROM EMP;
    ```

18. **Task:** Find the number of distinct jobs present in the employee table.
    ```sql
    SELECT COUNT(DISTINCT JOB)
    FROM EMP;
    ```

19. **Task:** Find the average salary given to the 'CLERK's.
    ```sql
    SELECT AVG(SAL)
    FROM EMP
    WHERE JOB = 'CLERK';
    ```

20. **Task:** Find the minimum salary for employees who work in department 10 as a 'MANAGER' or a 'CLERK'.
    ```sql
    SELECT MIN(SAL)
    FROM EMP
    WHERE DEPTNO = 10 AND JOB IN ('MANAGER', 'CLERK');
    ```

---

## DAY 10: Grouping and Filtering
_Wednesday, July 29, 2020_

### `GROUP BY` Clause
The `GROUP BY` clause is used to arrange identical data into groups. It is almost always used with aggregate functions (`COUNT`, `MAX`, `SUM`, etc.) to perform calculations on each group.

**Syntax:**
```sql
SELECT group_expression, aggregate_function(column)
FROM table_name
[WHERE condition]
GROUP BY group_expression;
```

**Order of Execution:**
1. `FROM` (Row-by-row)
2. `WHERE` (Row-by-row)
3. `GROUP BY` (Forms groups)
4. `SELECT` (Group-by-group)

#### `GROUP BY` Examples
* **Task:** Find the number of employees working in each department.
    ```sql
    SELECT DEPTNO, COUNT(*)
    FROM EMP
    GROUP BY DEPTNO;
    ```
* **Task:** Find the maximum salary given for each job.
    ```sql
    SELECT JOB, MAX(SAL)
    FROM EMP
    GROUP BY JOB;
    ```
* **Task:** Find the number of employees getting a commission in each department.
    ```sql
    SELECT DEPTNO, COUNT(COMM)
    FROM EMP
    GROUP BY DEPTNO;
    ```

### `HAVING` Clause
> "The `HAVING` Clause is used to filter groups."

It is used after `GROUP BY` to filter groups based on the results of aggregate functions.

**Full Order of Execution:**
1. `FROM`
2. `WHERE`
3. `GROUP BY`
4. `HAVING`
5. `SELECT`

#### `WHERE` vs. `HAVING`

| `WHERE` Clause | `HAVING` Clause |
| :--- | :--- |
| Filters **rows**. | Filters **groups**. |
| Executes **before** `GROUP BY`. | Executes **after** `GROUP BY`. |
| Executes row-by-row. | Executes group-by-group. |
| **Cannot** use aggregate functions. | **Can** use aggregate functions. |

#### `HAVING` Examples
* **Task:** Find departments where there are at least 3 employees.
    ```sql
    SELECT DEPTNO, COUNT(*)
    FROM EMP
    GROUP BY DEPTNO
    HAVING COUNT(*) >= 3;
    ```
* **Task:** Find the job titles held by at least 2 employees.
    ```sql
    SELECT JOB, COUNT(*)
    FROM EMP
    GROUP BY JOB
    HAVING COUNT(*) >= 2;
    ```
* **Task:** Find repeated employee names.
    ```sql
    SELECT ENAME, COUNT(*)
    FROM EMP
    GROUP BY ENAME
    HAVING COUNT(*) > 1;
    ```
* **Task:** Find the total salary for each job, but only for jobs where the total salary is greater than 3450.
    ```sql
    SELECT JOB, SUM(SAL)
    FROM EMP
    GROUP BY JOB
    HAVING SUM(SAL) > 3450;
    ```
* **Task:** In each job, find the number of employees earning more than 1200, but only show jobs where the total salary for those employees exceeds 3800.
    ```sql
    SELECT JOB, COUNT(*), SUM(SAL)
    FROM EMP
    WHERE SAL > 1200
    GROUP BY JOB
    HAVING SUM(SAL) > 3800;
    ```

---

## DAY 11: Subqueries
_Thursday, July 30, 2020_

> "A query written inside another query is known as a Subquery."

### Working Principle
* The **Inner Query** (the subquery) executes first and produces an output.
* The output of the Inner Query is then used as an input for the **Outer Query**.
* The Outer Query executes and generates the final result.

### Use Case: Finding Unknowns
We use subqueries when a condition in our query depends on an unknown value that must first be retrieved from the database.

* **Task:** Find the names of employees earning less than 'MILLER'. (We don't know Miller's salary).
    ```sql
    -- The inner query finds Miller's salary (e.g., 1500)
    -- The outer query then finds employees earning less than that value.
    SELECT ENAME
    FROM EMP
    WHERE SAL < (SELECT SAL FROM EMP WHERE ENAME = 'MILLER');
    ```
* **Task:** Find the name and department number of employees working in the same department as 'SMITH'.
    ```sql
    SELECT ENAME, DEPTNO
    FROM EMP
    WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'SMITH');
    ```
* **Task:** Find employees who were hired after 'JONES'.
    ```sql
    SELECT ENAME, HIREDATE
    FROM EMP
    WHERE HIREDATE > (SELECT HIREDATE FROM EMP WHERE ENAME = 'JONES');
    ```
* **Task:** Find employees earning more than 'SMITH' but less than 'KING'.
    ```sql
    SELECT *
    FROM EMP
    WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'SMITH')
      AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'KING');
    ```

#### Key Rules for Single-Row Subqueries
* The inner query cannot select more than one column.
* The data type of the column returned by the inner query must match the data type of the column used in the outer query's `WHERE` clause.

---

## DAY 12: Advanced Subqueries
_Saturday, August 1, 2020_

### Subquery Use Case 2: Cross-Table Conditions
> A subquery is used whenever the data to be selected and the condition to be executed are present in different tables.

This is a very common scenario. For example, you want to find the department *name* (from the `DEPT` table) for an employee named 'MILLER' (whose record is in the `EMP` table).

* **EMP Table**
| EID | ENAME | SAL | DEPTNO |
| :-- | :---- | :-- | :--- |
| 1 | ALLEN | 1000 | 20 |
| 2 | BLAKE | 2000 | 10 |
| 3 | CLARK | 3000 | 30 |
| 4 | MILLER | 1500 | 10 |
| 5 | ADAMS | 2500 | 20 |

* **DEPT Table**
| DEPTNO | DNAME | LOC |
| :--- | :--- | :--- |
| 10 | D1 | L1 |
| 20 | D2 | L2 |
| 30 | D3 | L3 |

#### Examples
* **Task:** Find the department name of the employee 'MILLER'.
    ```sql
    -- The inner query finds Miller's DEPTNO from the EMP table (result is 10).
    -- The outer query then finds the DNAME from the DEPT table where DEPTNO is 10.
    SELECT DNAME
    FROM DEPT
    WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'MILLER');
    ```

* **Task:** Find the location of 'ADAMS'.
    ```sql
    SELECT LOC
    FROM DEPT
    WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'ADAMS');
    ```

* **Task:** Find the names of employees working in location 'L2'.
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC = 'L2');
    ```

* **Task:** Find the number of employees working in department 'D3'.
    ```sql
    SELECT COUNT(*)
    FROM EMP
    WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'D3');
    ```

* **Task:** Find the maximum salary of an employee working in 'DALLAS'.
    ```sql
    SELECT MAX(SAL)
    FROM EMP
    WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS');
    ```

### Subqueries with Aggregate Functions (`MAX` & `MIN`)

A common use case for subqueries is finding non-aggregate data related to an aggregate value. For example, you cannot select `ENAME` and `MAX(SAL)` in the same query without a `GROUP BY`. A subquery solves this.

* **Task:** Find the name of the employee earning the maximum salary.
    ```sql
    -- This is the correct way. The inner query finds the maximum salary value.
    -- The outer query then finds the employee whose salary matches that value.
    SELECT ENAME
    FROM EMP
    WHERE SAL = (SELECT MAX(SAL) FROM EMP);
    ```

* **Task:** Find the name and salary of the employee earning the minimum salary.
    ```sql
    SELECT ENAME, SAL
    FROM EMP
    WHERE SAL = (SELECT MIN(SAL) FROM EMP);
    ```

---

## DAY 13: Types of Subqueries
_Monday, August 3, 2020_

### Single-Row vs. Multi-Row Subqueries

1.  **Single-Row Subquery:**
    * The inner query returns exactly **one** value (one row, one column).
    * You can use standard comparison operators (`=`, `>`, `<`, etc.).
    * **Example:** `... WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'ALLEN')` - This is safe because an employee has only one department.

2.  **Multi-Row Subquery:**
    * The inner query can return **more than one** value.
    * You **cannot** use standard single-row operators like `=`. You must use multi-row operators like `IN`.
    * **Example:** Find the department names for 'ALLEN' and 'SMITH'.
        ```sql
        -- The subquery returns two DEPTNOs (10 and 20).
        -- Using '=' would cause an error. Using 'IN' works correctly.
        SELECT DNAME
        FROM DEPT
        WHERE DEPTNO IN (SELECT DEPTNO FROM EMP WHERE ENAME IN ('ALLEN', 'SMITH'));
        ```

### Subquery Operators (`ALL` and `ANY`)
These are used with relational operators (`>`, `<`, etc.) when the subquery might return multiple rows.

1.  **`ALL`**: The condition must be true for **all** values returned by the subquery.
    * `> ALL`: Greater than the maximum value.
    * `< ALL`: Less than the minimum value.

2.  **`ANY`**: The condition must be true for **at least one** of the values returned by the subquery.
    * `> ANY`: Greater than the minimum value.
    * `< ANY`: Less than the maximum value.

* **Task:** Find employees earning more than **all** employees in department 10.
    ```sql
    -- This is equivalent to finding employees who earn more than the MAX salary in dept 10.
    SELECT ENAME, SAL
    FROM EMP
    WHERE SAL > ALL (SELECT SAL FROM EMP WHERE DEPTNO = 10);
    ```

* **Task:** Find employees earning more than **at least one** employee in department 10.
    ```sql
    -- This is equivalent to finding employees who earn more than the MIN salary in dept 10.
    SELECT ENAME, SAL
    FROM EMP
    WHERE SAL > ANY (SELECT SAL FROM EMP WHERE DEPTNO = 10);
    ```

### Nested Subqueries
> "A subquery written inside another subquery is known as a Nested Subquery."

This is commonly used to find the Nth highest/lowest value.

* **Task:** Find the second maximum salary.
    ```sql
    -- The innermost query finds the max salary.
    -- The outer query finds the max salary that is LESS THAN the absolute max.
    SELECT MAX(SAL)
    FROM EMP
    WHERE SAL < (SELECT MAX(SAL) FROM EMP);
    ```

* **Task:** Find the third minimum salary.
    ```sql
    SELECT MIN(SAL)
    FROM EMP
    WHERE SAL > (SELECT MIN(SAL) FROM EMP WHERE SAL > (SELECT MIN(SAL) FROM EMP));
    ```

---

## DAY 14: Employee and Manager Relations
_Tuesday, August 4, 2020_

Subqueries are essential for navigating hierarchical relationships within the same table, such as an employee-manager structure where `MGR` refers to another employee's `EID`.

### Case 1: Finding the Manager
* **Task:** Find the name of Allen's manager.
    ```sql
    -- The inner query gets Allen's manager ID (MGR).
    -- The outer query finds the employee whose employee ID (EID) matches that manager ID.
    SELECT ENAME
    FROM EMP
    WHERE EID = (SELECT MGR FROM EMP WHERE ENAME = 'ALLEN');
    ```

* **Task:** Find the name of Smith's manager's manager. (Nested Subquery)
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE EID = (SELECT MGR FROM EMP WHERE EID = (SELECT MGR FROM EMP WHERE ENAME = 'SMITH'));
    ```

### Case 2: Finding the Employees
* **Task:** Find the names of employees reporting to 'KING'.
    ```sql
    -- The inner query gets King's employee ID (EID).
    -- The outer query finds all employees whose manager ID (MGR) matches King's ID.
    SELECT ENAME
    FROM EMP
    WHERE MGR = (SELECT EID FROM EMP WHERE ENAME = 'KING');
    ```

---

## DAY 15: Introduction to Joins
_Wednesday, August 5, 2020_

> "A Join is the process of retrieving data from multiple tables simultaneously."

### Types of Joins
1.  **Cross Join** (Cartesian Join)
2.  **Inner Join** (Equi Join)
3.  **Outer Join** (Left, Right, Full)
4.  **Self Join**
5.  **Natural Join**

### 1. Cross Join
In a Cross Join, every record from the first table is merged with every record from the second table.
* **Number of Columns:** Sum of columns from both tables.
* **Number of Rows:** Product of rows from both tables.

**Syntax:**
```sql
-- ANSI Syntax
SELECT ENAME, DNAME
FROM EMP CROSS JOIN DEPT;

-- Oracle Syntax
SELECT ENAME, DNAME
FROM EMP, DEPT;
```

### 2. Inner Join
> "An Inner Join is used to obtain only the matching records from two tables based on a join condition."

**Syntax:**
```sql
-- ANSI Syntax
SELECT ENAME, DNAME
FROM EMP
INNER JOIN DEPT ON EMP.DEPTNO = DEPT.DEPTNO;

-- Oracle Syntax
SELECT ENAME, DNAME
FROM EMP, DEPT
WHERE EMP.DEPTNO = DEPT.DEPTNO;
```

* **Task:** Find the name and location for all employees working as a 'MANAGER'.
    ```sql
    SELECT e.ENAME, d.LOC
    FROM EMP e, DEPT d
    WHERE e.DEPTNO = d.DEPTNO AND e.JOB = 'MANAGER';
    ```

* **Task:** Find the employee name, department number, department name, and location for employees earning more than 2000 in 'NEW YORK'.
    ```sql
    SELECT e.ENAME, e.DEPTNO, d.DNAME, d.LOC
    FROM EMP e, DEPT d
    WHERE e.DEPTNO = d.DEPTNO
      AND e.SAL > 2000
      AND d.LOC = 'NEW YORK';
    ```

---

## Solved Assignment: Inner Join

1.  **Task:** Display the name of the employee and their location.
    ```sql
    SELECT ENAME, LOC
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO;
    ```
2.  **Task:** Display the department name and salary for all employees working in 'ACCOUNTING'.
    ```sql
    SELECT DNAME, SAL
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND DNAME = 'ACCOUNTING';
    ```
3.  **Task:** Display the department name and annual salary for all employees whose salary is more than 2340.
    ```sql
    SELECT DNAME, SAL * 12
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND SAL > 2340;
    ```
4.  **Task:** Display the employee name and department name for employees having the character 'A' in their name.
    ```sql
    SELECT ENAME, DNAME
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND ENAME LIKE '%A%';
    ```
5.  **Task:** Display the employee name and department name for all employees working as 'SALESMAN'.
    ```sql
    SELECT ENAME, DNAME
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND JOB = 'SALESMAN';
    ```
6.  **Task:** Display the department name and job for employees whose job and department name both start with 'S'.
    ```sql
    SELECT DNAME, JOB
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND JOB LIKE 'S%' AND DNAME LIKE 'S%';
    ```
7.  **Task:** Display the department name and manager number for employees reporting to manager 7839.
    ```sql
    SELECT DNAME, MGR
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO AND MGR = 7839;
    ```
8.  **Task:** Display the department name and hire date for employees hired after 1983 in the 'ACCOUNTING' or 'RESEARCH' departments.
    ```sql
    SELECT DNAME, HIREDATE
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO
      AND HIREDATE > '31-DEC-83'
      AND DNAME IN ('ACCOUNTING', 'RESEARCH');
    ```
9.  **Task:** Display the employee name and department name for employees who get a commission in department 10 or 30.
    ```sql
    SELECT ENAME, DNAME
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO
      AND COMM IS NOT NULL
      AND EMP.DEPTNO IN (10, 30);
    ```
10. **Task:** Display the department name and employee number for employees whose `EMPNO` is 7839 or 7902 and are working in 'NEW YORK'.
    ```sql
    SELECT DNAME, EMPNO
    FROM EMP, DEPT
    WHERE EMP.DEPTNO = DEPT.DEPTNO
      AND EMPNO IN (7839, 7902)
      AND LOC = 'NEW YORK';
    ```

---

## DAY 16: Outer Joins & Self Joins


### Outer Joins
> "An Outer Join is used to obtain unmatched records from one or both tables, along with the matching records."



1.  **`LEFT OUTER JOIN`**
    > "Returns all records from the **left** table and only the matching records from the right table."
    * **ANSI Syntax:**
        ```sql
        SELECT E.ENAME, D.DNAME
        FROM EMP E
        LEFT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
        ```
    * **Oracle Syntax:**
        ```sql
        SELECT E.ENAME, D.DNAME
        FROM EMP E, DEPT D
        WHERE E.DEPTNO = D.DEPTNO(+);
        ```

2.  **`RIGHT OUTER JOIN`**
    > "Returns all records from the **right** table and only the matching records from the left table."
    * **ANSI Syntax:**
        ```sql
        SELECT E.ENAME, D.DNAME
        FROM EMP E
        RIGHT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
        ```
    * **Oracle Syntax:**
        ```sql
        SELECT E.ENAME, D.DNAME
        FROM EMP E, DEPT D
        WHERE E.DEPTNO(+) = D.DEPTNO;
        ```

3.  **`FULL OUTER JOIN`**
    > "Returns all records from **both** the left and right tables, including all matched and unmatched records."
    * **ANSI Syntax:**
        ```sql
        SELECT E.ENAME, D.DNAME
        FROM EMP E
        FULL OUTER JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
        ```

### Self Join
> "Joining a table to itself is known as a Self Join. It is used when the data you need to compare is in different rows of the same table."

This is common for hierarchical data, like an employee-manager relationship.

* **Task:** Display the employee's name and their manager's name for all employees.
    ```sql
    -- E1 is an alias for the employee record, E2 is an alias for the manager's record.
    SELECT E1.ENAME AS Employee_Name, E2.ENAME AS Manager_Name
    FROM EMP E1
    JOIN EMP E2 ON E1.MGR = E2.EMPNO;
    ```

* **Task:** Display the employee's name, their salary, their manager's name, and the manager's salary if the manager earns more than the employee.
    ```sql
    SELECT E1.ENAME AS Emp_Name, E1.SAL AS Emp_Sal, E2.ENAME AS Mgr_Name, E2.SAL AS Mgr_Sal
    FROM EMP E1
    JOIN EMP E2 ON E1.MGR = E2.EMPNO
    WHERE E2.SAL > E1.SAL;
    ```

**Note:** To join 'N' number of tables, you need 'N-1' join conditions.

---

## DAY 17: Correlated Subqueries
_Friday, August 7, 2020_

> "A Correlated Subquery is a subquery where the inner query and the outer query are dependent on each other."

In a correlated subquery, the inner query is evaluated once for each row processed by the outer query. They are often used with `EXISTS` and `NOT EXISTS`.

| Subquery | Correlated Subquery |
| :--- | :--- |
| Inner query executes first and only once. | Outer query executes first; inner query executes for each outer row. |
| Outer query is dependent on the inner query. | Both queries are interdependent. |
| A join condition is not mandatory. | A join condition in the inner query is mandatory. |

* **Task:** Find the names of departments that have at least one employee.
    ```sql
    SELECT DNAME
    FROM DEPT D
    WHERE EXISTS (SELECT 1 FROM EMP E WHERE E.DEPTNO = D.DEPTNO);
    ```

* **Task:** Find the names of departments that have no employees.
    ```sql
    SELECT DNAME
    FROM DEPT D
    WHERE NOT EXISTS (SELECT 1 FROM EMP E WHERE E.DEPTNO = D.DEPTNO);
    ```

---

## DAY 18: Single-Row Functions

Single-row functions operate on a single row and return one result per row.

### String Functions
* **`LENGTH('string')`**: Counts the number of characters.
* **`CONCAT('string1', 'string2')`**: Joins two strings.
* **`UPPER('string')`**: Converts a string to uppercase.
* **`LOWER('string')`**: Converts a string to lowercase.
* **`INITCAP('string')`**: Capitalizes the first letter of each word.
* **`REVERSE('string')`**: Reverses the characters in a string.
* **`SUBSTR('string', position, [length])`**: Extracts a substring.
    * `SUBSTR('QSPIDER', 2, 3)` returns `SPI`.
    * `SUBSTR('QSPIDER', -3)` returns `DER`.
* **`REPLACE('string', 'search', ['replace'])`**: Replaces occurrences of a substring.
    * `REPLACE('BANANA', 'A', 'C')` returns `BCNCNC`.
    * `REPLACE('BANANA', 'A')` returns `BNN` (replaces with nothing).

**Trick:** Count occurrences of a character in a string.
* **Task:** Count the number of 'A's in 'MALAYALAM'.
    ```sql
    -- DUAL is a dummy table used for single-row function tests
    SELECT LENGTH('MALAYALAM') - LENGTH(REPLACE('MALAYALAM', 'A'))
    FROM DUAL;
    ```

---

## DAY 19: Advanced Single-Row Functions

### `INSTR()` Function
> `INSTR()` is used to find the starting position of a substring within a string. It returns the position if found, otherwise it returns 0.

**Syntax:** `INSTR('original_string', 'substring', [start_position], [occurrence])`
* `start_position`: The position in the original string to start searching from. Defaults to 1.
* `occurrence`: Which occurrence of the substring to find. Defaults to 1.

* **Example:** Find the 2nd occurrence of 'A' in 'BANANA', starting from the beginning.
    ```sql
    INSTR('BANANA', 'A', 1, 2) -- Returns 4
    ```

* **Example:** Find the 3rd occurrence of 'A' in 'BANANA'.
    ```sql
    INSTR('BANANA', 'A', 1, 3) -- Returns 6
    ```

* **Task:** Find names of employees that have the character 'A' present at least twice.
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE INSTR(ENAME, 'A', 1, 2) > 0;
    ```
* **Task:** Find names of employees that have the character 'A' present exactly twice.
    ```sql
    SELECT ENAME
    FROM EMP
    WHERE INSTR(ENAME, 'A', 1, 2) > 0 AND INSTR(ENAME, 'A', 1, 3) = 0;
    ```

### Numeric Functions
* **`MOD(m, n)`**: Returns the modulus (remainder) of `m` divided by `n`.
    * **Task:** Find employees with an odd Employee ID.
        ```sql
        SELECT * FROM EMP WHERE MOD(EMPNO, 2) = 1;
        ```
* **`ROUND(number, [scale])`**: Rounds a number to a specified number of decimal places (the scale).
    * `ROUND(5.6)` returns `6`.
    * `ROUND(124.235, 2)` returns `124.24`.
    * `ROUND(8426, -1)` returns `8430` (rounds to the nearest 10).
* **`TRUNC(number, [scale])`**: Truncates (cuts off) a number to a specified number of decimal places without rounding.
    * `TRUNC(5.6)` returns `5`.
    * `TRUNC(124.235, 2)` returns `124.23`.

### Date Functions
* **`SYSDATE` / `CURRENT_DATE`**: Returns the current database server date.
* **`SYSTIMESTAMP`**: Returns the current database server date, time, and time zone.
* **`MONTHS_BETWEEN(date1, date2)`**: Returns the number of months between two dates.
* **`LAST_DAY(date)`**: Returns the last day of the month for a given date.
* **`TO_CHAR(date, 'format_model')`**: Converts a date to a string in a specified format.
    * `TO_CHAR(SYSDATE, 'YYYY')` -> `2025`
    * `TO_CHAR(SYSDATE, 'MONTH')` -> `AUGUST`
    * `TO_CHAR(SYSDATE, 'DAY')` -> `SATURDAY`
    * `TO_CHAR(SYSDATE, 'HH24:MI:SS')` -> `17:39:10`
    * **Task:** Find employees who were hired on a Sunday.
        ```sql
        SELECT *
        FROM EMP
        WHERE TO_CHAR(HIREDATE, 'DY') = 'SUN';
        ```

### `NVL()` Function (Null Value Logic)
> `NVL()` is used to substitute a value when a null value is encountered. This is useful for preventing nulls from disrupting arithmetic operations.

**Syntax:** `NVL(column_or_expression, substitute_value)`

* **Task:** Calculate total earnings (`SAL` + `COMM`) for all employees, treating null commissions as 0.
    ```sql
    -- Without NVL, SAL + NULL would result in NULL.
    SELECT ENAME, SAL + NVL(COMM, 0) AS Total_Salary
    FROM EMP;
    ```

---

## DAY 20: Data Definition Language (DDL)

> "DDL is used to construct objects in the database and deals with the structure of the object."

The 5 main DDL statements are:
1.  **`CREATE`**: Builds an object (like a table).
2.  **`RENAME`**: Changes the name of an object.
3.  **`ALTER`**: Modifies the structure of a table.
4.  **`TRUNCATE`**: Removes all records from a table permanently.
5.  **`DROP`**: Removes a table's structure and data permanently.

### DDL Examples
* **`CREATE TABLE`**:
    ```sql
    CREATE TABLE CUSTOMER (
        CID NUMBER(2) PRIMARY KEY,
        CNAME VARCHAR(10) NOT NULL,
        CNO NUMBER(10) NOT NULL UNIQUE CHECK(LENGTH(CNO) = 10),
        ADDRESS VARCHAR(15)
    );
    ```
* **`RENAME TABLE`**:
    ```sql
    RENAME CUSTOMER TO CUST;
    ```
* **`ALTER TABLE`**:
    ```sql
    -- Add a column
    ALTER TABLE CUST ADD MAIL_ID VARCHAR(15);
    -- Drop a column
    ALTER TABLE CUST DROP COLUMN MAIL_ID;
    -- Rename a column
    ALTER TABLE CUST RENAME COLUMN CNO TO PHONE_NO;
    -- Modify a column's datatype
    ALTER TABLE CUST MODIFY CNAME CHAR(10);
    ```
* **`TRUNCATE TABLE`**:
    ```sql
    TRUNCATE TABLE CUST;
    ```
* **`DROP TABLE`**:
    ```sql
    DROP TABLE CUST;
    ```
    * **To recover a dropped table (Oracle specific):**
      ```sql
      FLASHBACK TABLE CUST TO BEFORE DROP;
      ```
    * **To permanently delete from recycle bin (Oracle specific):**
      ```sql
      PURGE TABLE CUST;
      ```
**Note:** DDL statements are **auto-commit**, meaning their changes are saved immediately and cannot be rolled back.

---

## DAY 21: Data Manipulation Language (DML) & TCL

### Data Manipulation Language (DML)
DML is used to manipulate the data within tables. These operations are also known as transactions.
1. `INSERT`: Adds new records.
2. `UPDATE`: Modifies existing records.
3. `DELETE`: Removes specific records.

* **`INSERT`**:
    ```sql
    INSERT INTO CUSTOMER VALUES (1, 'DINGA', 9876543210, 'BANGALORE');
    ```
* **`UPDATE`**:
    ```sql
    UPDATE CUSTOMER
    SET CNO = 7778889994
    WHERE CNAME = 'ABDUL';
    ```
* **`DELETE`**:
    ```sql
    DELETE FROM CUSTOMER
    WHERE CNAME = 'ABDUL';
    ```

### `TRUNCATE` vs. `DELETE`
| `TRUNCATE` | `DELETE` |
| :--- | :--- |
| DDL command. | DML command. |
| Removes **all** records. | Removes specific records (or all if no `WHERE` clause). |
| Cannot be rolled back (auto-commit). | Can be rolled back. |
| Very fast. | Slower, as it deletes row by row. |

### Transaction Control Language (TCL)
TCL is used to manage DML transactions.
1. `COMMIT`: Saves transactions permanently.
2. `ROLLBACK`: Undoes transactions to the last `COMMIT`.
3. `SAVEPOINT`: Creates a marker within a transaction you can roll back to.

---

## DAY 22: Normalization

> "Normalization is the process of reducing a large table into smaller tables to remove data redundancy and improve data integrity."

### Normal Forms
* **First Normal Form (1NF):**
    * The table must have a primary key.
    * Each cell must contain a single, atomic value (no multi-valued data).
* **Second Normal Form (2NF):**
    * Must be in 1NF.
    * Must not have any partial dependencies (all non-key attributes must be fully dependent on the entire primary key, which is relevant for composite keys).
* **Third Normal Form (3NF):**
    * Must be in 2NF.
    * Must not have any transitive dependencies (a non-key attribute should not depend on another non-key attribute).

**Note:** A table is generally considered normalized if it is in **3NF**.