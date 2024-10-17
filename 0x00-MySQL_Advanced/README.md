# MySQL advanced  
### Concepts  
  
_For this project, it is expectes of you to look at this concept:_  
  
- [Advanced SQL](https://intranet.alxswe.com/concepts/555)  
  
## Resources  
  
**Read or watch**:  
  
- [MySQL cheatsheet](https://intranet.alxswe.com/rltoken/8w9di_hk19DIMSBEV3EayQ "MySQL cheatsheet")  
- [MySQL Performance: How To Leverage MySQL Database Indexing](https://intranet.alxswe.com/rltoken/2GJbZ48zRPA70o2YhTdH7g "MySQL Performance: How To Leverage MySQL Database Indexing")  
- [Stored Procedure](https://intranet.alxswe.com/rltoken/K180X2OCzb6gzPngjn-EIg "Stored Procedure")  
- [Triggers](https://intranet.alxswe.com/rltoken/cJ1qA4o-rRm4rWIsqYKSZg "Triggers")  
- [Views](https://intranet.alxswe.com/rltoken/vHg1z3UAOcWMvOt8xZHeiA "Views")  
- [Functions and Operators](https://intranet.alxswe.com/rltoken/g-c1m6iljScpi4LeqxBRqQ "Functions and Operators")  
- [Trigger Syntax and Examples](https://intranet.alxswe.com/rltoken/gLVwKjQfRL0Jr_nWqAS7VQ "Trigger Syntax and Examples")  
- [CREATE TABLE Statement](https://intranet.alxswe.com/rltoken/X789nJ22H6HVh1uCQPl0lg "CREATE TABLE Statement")  
- [CREATE PROCEDURE and CREATE FUNCTION Statements](https://intranet.alxswe.com/rltoken/mfrWMt1KL3NHXblJykMgZg "CREATE PROCEDURE and CREATE FUNCTION Statements")  
- [CREATE INDEX Statement](https://intranet.alxswe.com/rltoken/oCu8Rg9WfKyF4BhTt8dZGQ "CREATE INDEX Statement")  
- [CREATE VIEW Statement](https://intranet.alxswe.com/rltoken/FEZNlZFKZmD1ISnLINkCwQ "CREATE VIEW Statement")  
  
## Learning Objectives  
  
At the end of this project, you are expected to be able to [explain to anyone](https://intranet.alxswe.com/rltoken/NEA0Fr7muHfukl5lziVAhg "explain to anyone"), **without the help of Google**:  
  
### General  
  
- How to create tables with constraints  
- How to optimize queries by adding indexes  
- What is and how to implement stored procedures and functions in MySQL  
- What is and how to implement views in MySQL  
- What is and how to implement triggers in MySQL  
  
## Requirements  
  
### General  
  
- All your files will be executed on Ubuntu 18.04 LTS using `MySQL 5.7` (version 5.7.30)  
- All your files should end with a new line  
- All your SQL queries should have a comment just before (i.e. syntax above)  
- All your files should start by a comment describing the task  
- All SQL keywords should be in uppercase (`SELECT`, `WHERE`…)  
- A `README.md` file, at the root of the folder of the project, is mandatory  
- The length of your files will be tested using `wc`  

# Overview
Here's a guide to help you understand key concepts in MySQL, including tables with constraints, indexes, stored procedures, functions, views, and triggers. I'll break down each topic step-by-step so that you can explain them confidently.

### 1. **Creating Tables with Constraints**

**Constraints** in MySQL are rules that enforce certain conditions on the data in the database tables, ensuring integrity and accuracy.

#### Common Constraints:

-   **PRIMARY KEY**: Uniquely identifies each record in the table.
-   **FOREIGN KEY**: Links records between tables to enforce relationships.
-   **UNIQUE**: Ensures all values in a column are distinct.
-   **NOT NULL**: Prevents NULL values from being entered into a column.
-   **CHECK**: Enforces a condition that values in a column must satisfy.

#### Example: Creating a table with constraints
```
CREATE TABLE employees (
    employee_id INT PRIMARY KEY, -- PRIMARY KEY constraint
    first_name VARCHAR(50) NOT NULL, -- NOT NULL constraint
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE, -- UNIQUE constraint
    department_id INT,
    salary DECIMAL(10, 2) CHECK (salary > 0), -- CHECK constraint
    FOREIGN KEY (department_id) REFERENCES departments(department_id) -- FOREIGN KEY constraint
);
```
**Explanation**:

-   **PRIMARY KEY**: Ensures that `employee_id` is unique for each employee.
-   **NOT NULL**: Ensures first name and last name cannot be NULL.
-   **UNIQUE**: Ensures no two employees share the same email.
-   **CHECK**: Ensures that salary is always greater than 0.
-   **FOREIGN KEY**: Links `department_id` to another table (departments).

----------

### 2. **Optimizing Queries by Adding Indexes**

An **index** in MySQL speeds up query performance by allowing the database to find records more efficiently. Indexes are created on one or more columns in a table.

#### Example: Adding an index
```
CREATE INDEX idx_lastname ON employees(last_name);
```
**Explanation**:

-   This creates an index on the `last_name` column, allowing queries that filter or search by `last_name` to execute faster.
-   Indexes improve read performance but slightly slow down write operations (inserts/updates).

#### When to use indexes:

-   On columns frequently used in `WHERE`, `JOIN`, and `ORDER BY` clauses.
-   Avoid adding indexes on columns with a lot of duplicate values (low selectivity).

----------

### 3. **Stored Procedures and Functions in MySQL**

**Stored Procedures** and **Functions** are reusable blocks of SQL code that can be executed to perform specific tasks.

#### Stored Procedure
A **Stored Procedure** is a set of SQL statements that perform a task and can accept input parameters.

##### Example: Creating a Stored Procedure
```
DELIMITER //
CREATE PROCEDURE GetEmployeeSalary (IN emp_id INT)
BEGIN
    SELECT salary FROM employees WHERE employee_id = emp_id;
END //
DELIMITER ;
```
**Explanation**:

-   The `GetEmployeeSalary` procedure takes an `emp_id` as input and retrieves the corresponding employee's salary.
-   You can call this procedure using `CALL GetEmployeeSalary(5);`.

#### Function

A **Function** is similar but must return a value and can be used directly in SQL queries.

##### Example: Creating a Function
```
DELIMITER //
CREATE FUNCTION CalculateBonus (salary DECIMAL(10, 2)) RETURNS DECIMAL(10, 2)
BEGIN
    RETURN salary * 0.10; -- Calculates 10% of salary
END //
DELIMITER ;
```
**Explanation**:

-   This function takes a salary as input and returns 10% of it.
-   You can use it in queries like `SELECT CalculateBonus(salary) FROM employees;`.

----------

### 4. **Views in MySQL**

A **View** is a virtual table created by a `SELECT` query. It does not store data itself but provides a way to simplify complex queries by encapsulating them in a reusable form.

#### Example: Creating a View
```
CREATE VIEW employee_details AS
SELECT e.employee_id, e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
```
**Explanation**:

-   The view `employee_details` combines data from `employees` and `departments` tables. You can query it like a table:
 ```
SELECT * FROM employee_details WHERE department_name = 'Sales';
```
**Benefits of Views**:

-   Simplifies complex queries.
-   Adds security by restricting access to specific data.

----------

### 5. **Triggers in MySQL**

A **Trigger** is a piece of SQL code that automatically executes (fires) in response to certain events on a table, such as `INSERT`, `UPDATE`, or `DELETE`.

#### Example: Creating a Trigger
```
CREATE TRIGGER before_employee_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;
END;
```
**Explanation**:

-   This trigger is called **before** a new employee is inserted into the `employees` table. It checks if the `salary` is less than 0 and, if so, sets it to 0.
-   Triggers ensure that certain business rules are enforced automatically.

----------

### Summary of Concepts:

-   **Tables with Constraints**: Enforce data rules like primary keys, foreign keys, uniqueness, and data validation (`CHECK`, `NOT NULL`).
-   **Indexes**: Speed up queries by allowing faster data retrieval on specific columns.
-   **Stored Procedures**: Predefined SQL code that can perform tasks and accept parameters.
-   **Functions**: Similar to procedures but must return a value and can be used in queries.
-   **Views**: Virtual tables that encapsulate complex queries.
-   **Triggers**: Automatically execute SQL in response to certain events like `INSERT`, `UPDATE`, or `DELETE`.
