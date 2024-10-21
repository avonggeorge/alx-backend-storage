# MySQL advanced  
### Overview of MySQL

**MySQL** is one of the most popular open-source relational database management systems (RDBMS) in the world. It is widely used in web applications and is a fundamental component of the LAMP (Linux, Apache, MySQL, PHP/Python/Perl) stack. MySQL is known for its reliability, ease of use, and scalability, making it a preferred choice for small and large applications alike.

#### Key Concepts and Features of MySQL

1.  **Relational Database**:
    
    -   MySQL is a **relational database**, which means it stores data in tables (structured format) and uses SQL (Structured Query Language) for querying and managing data.
    -   Tables are collections of related data organized into rows and columns. Each table has a unique primary key that identifies each row.
2.  **SQL (Structured Query Language)**:
    
    -   SQL is a standard language for interacting with relational databases. MySQL supports a large subset of SQL, including:
        -   **SELECT**: Retrieve data from one or more tables.
        -   **INSERT**: Add new data into a table.
        -   **UPDATE**: Modify existing data in a table.
        -   **DELETE**: Remove data from a table.
        -   **CREATE**: Create a new table or database.
        -   **DROP**: Delete a table or database.
3.  **Data Types**: MySQL supports various data types to define the nature of data stored in each column:
    
    -   **Numeric types**: `INT`, `FLOAT`, `DECIMAL`, `DOUBLE`, etc.
    -   **String types**: `VARCHAR`, `TEXT`, `CHAR`, etc.
    -   **Date and time types**: `DATE`, `DATETIME`, `TIMESTAMP`, etc.
    -   **Boolean type**: MySQL does not have a native `BOOLEAN` type, but you can use `TINYINT(1)` where `0` represents `False` and `1` represents `True`.
4.  **Indexes**:
    
    -   Indexes are used to improve the speed of data retrieval operations on tables. Without indexes, MySQL has to scan the entire table to find specific records.
    -   Indexes are created on columns that are frequently queried, such as a primary key or foreign key.
5.  **Primary Key and Foreign Key**:
    
    -   A **primary key** is a unique identifier for each record in a table. It ensures that no two rows have the same value in the primary key column(s).
    -   A **foreign key** is a field in one table that refers to the primary key in another table. This establishes relationships between tables, allowing for normalized data storage and referential integrity.
6.  **Normalization**:
    
    -   **Normalization** is a database design technique to minimize data redundancy and dependency by organizing data into related tables.
    -   This allows for efficient data storage and ensures that updates to data are easily managed, reducing data anomalies.
7.  **ACID Compliance**: MySQL ensures data integrity and consistency through **ACID properties**:
    
    -   **Atomicity**: Ensures that all operations within a transaction are completed successfully, or none of them are.
    -   **Consistency**: Guarantees that the database remains in a valid state before and after the transaction.
    -   **Isolation**: Ensures that concurrently executing transactions do not interfere with each other.
    -   **Durability**: Guarantees that once a transaction is committed, the changes are permanent.
8.  **Transactions**:
    
    -   A **transaction** is a sequence of operations performed as a single logical unit of work, often used in scenarios like banking to ensure data consistency.
    -   You can control transactions in MySQL using `BEGIN`, `COMMIT`, and `ROLLBACK` statements.
9.  **Stored Procedures and Triggers**:
    
    -   **Stored Procedures**: These are SQL statements saved in the database that can be executed as needed. They help reduce repetitive code and can improve performance.
    -   **Triggers**: These are automated actions that are triggered when certain events (such as an `INSERT`, `UPDATE`, or `DELETE`) occur in a table.
10.  **Replication**:
    
      MySQL supports **replication**, which is the process of copying data from one database server (master) to another (slave). This improves availability and allows for read scalability.
      MySQL supports different types of replication:
           **Asynchronous Replication**: The master server continues operations without waiting for the slave to confirm.
           **Synchronous Replication**: The master waits for confirmation from the slave.
           **Semi-Synchronous Replication**: A hybrid model where the master waits for confirmation from at least one slave.
11.  **Scalability**:
    
       MySQL scales well with web applications. Vertical scaling (increasing the power of the server) and horizontal scaling (distributing the database across multiple servers) are both possible.
       MySQL can handle databases with millions of records and supports clustering techniques like **MySQL Cluster** for high availability and load balancing.
12.  **Security**:
    
       MySQL offers multiple security mechanisms, including user roles, encrypted connections, and fine-grained access control.
       You can grant specific permissions to different users or applications, and MySQL supports SSL/TLS for encrypted client-server communications.
13.  **Storage Engines**:
    
      MySQL allows you to use different **storage engines** for different tables:
        -   **InnoDB**: The default storage engine, offering ACID compliance and transaction support.
        -   **MyISAM**: Faster in read-heavy environments but doesn’t support transactions or foreign keys.
        -   **Memory**: Stores data in memory for quick access, but data is lost when the database restarts.
        -   **CSV**: Allows table data to be stored in CSV format for easy import/export.
14.  **MySQL Workbench**:
    
       **MySQL Workbench** is a graphical user interface (GUI) tool for managing MySQL databases. It offers tools for database design, SQL development, administration, and data migration.

### Example of MySQL Queries

-   **Create a database**:
```
CREATE DATABASE example_db;
```
-  **Create a table**:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
- **Insert data**:
```
INSERT INTO users (name, email) VALUES ('John Doe', 'john.doe@example.com');
```
- **Select data**:
```
SELECT * FROM users;
```
- **Update data**:
```
UPDATE users SET name = 'Jane Doe' WHERE id = 1;
```
- **Delete data**:
```
DELETE FROM users WHERE id = 1;
```
### Use Cases

-   **Web applications**: MySQL is the backbone for many websites, such as Facebook, Twitter, and YouTube, for managing their user data, transactions, and content.
-   **E-commerce platforms**: MySQL powers many online stores and handles product catalogs, user accounts, and order histories.
-   **Data warehousing**: MySQL can be used in reporting and analytics systems that require efficient querying and storing large datasets.

### Summary

MySQL is a robust, scalable, and widely-used relational database management system. Its ease of use, SQL support, and strong ecosystem make it a popular choice for developers building web and enterprise applications. Its open-source nature also means it’s highly customizable and cost-effective.
### Concepts  

  
_For this project, we expect you to look at this concept:_  
  
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
## More Info

### Comments for your SQL file:
```
$ cat my_script.sql
-- 3 first students in the Batch ID=3
-- because Batch 3 is the best!
SELECT id, name FROM students WHERE batch_id = 3 ORDER BY created_at DESC LIMIT 3;
$
```

### Use “container-on-demand” to run MySQL

- Ask for container `Ubuntu 18.04 - Python 3.7`
- Connect via SSH
- Or via the WebTerminal
- In the container, you should start MySQL before playing with it:
```
$ service mysql start
* MySQL Community Server 5.7.30 is started
$
$ cat 0-list_databases.sql | mysql -uroot -p my_database
Enter password:
Database
information_schema
mysql
performance_schema
sys
$
```
**In the container, credentials are `root/root`**

### How to import a SQL dump
```
$ echo "CREATE DATABASE hbtn_0d_tvshows;" | mysql -uroot -p
Enter password:
$ curl "https://s3.amazonaws.com/intranet-projects-files/holbertonschool-higher-level_programming+/274/hbtn_0d_tvshows.sql" -s | mysql -uroot -p hbtn_0d_tvshows
Enter password:
$ echo "SELECT * FROM tv_genres" | mysql -uroot -p hbtn_0d_tvshows
Enter password:
id name
1 Drama
2 Mystery
3 Adventure
4 Fantasy
5 Comedy
6 Crime
7 Suspense
8 Thriller
$
```