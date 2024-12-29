# MySQL Joins: Practice Notes

## Table of Contents
1. [Create a Database](#create-a-database)
2. [Create Tables](#create-tables)
3. [Insert Sample Data](#insert-sample-data)
4. [Practice Joins](#practice-joins)
    - [INNER JOIN](#inner-join)
    - [LEFT JOIN](#left-join)
    - [RIGHT JOIN](#right-join)
    - [FULL OUTER JOIN](#full-outer-join)
    - [Aggregate Functions with JOIN](#aggregate-functions-with-join)
5. [Advanced Joins](#advanced-joins)

---

## 1. Create a Database

```sql
CREATE DATABASE company;
USE company;
```

---

## 2. Create Tables

### Create the `departments` Table

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY AUTO_INCREMENT,
    department_name VARCHAR(100) NOT NULL
);
```

### Create the `employees` Table

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    department_id INT,
    hire_date DATE,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

### Create the `projects` Table

```sql
CREATE TABLE projects (
    project_id INT PRIMARY KEY AUTO_INCREMENT,
    project_name VARCHAR(100) NOT NULL,
    department_id INT,
    start_date DATE,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

### Create the `salaries` Table

```sql
CREATE TABLE salaries (
    employee_id INT,
    salary DECIMAL(10, 2),
    effective_date DATE,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);
```

---

## 3. Insert Sample Data

### Insert Data into `departments`

```sql
INSERT INTO departments (department_name) VALUES
('Engineering'),
('Sales'),
('HR'),
('Marketing');
```

### Insert Data into `employees`

```sql
INSERT INTO employees (first_name, last_name, department_id, hire_date) VALUES
('John', 'Doe', 1, '2020-01-15'),
('Jane', 'Smith', 2, '2021-02-22'),
('Michael', 'Brown', 1, '2019-07-30'),
('Emily', 'Davis', 3, '2018-05-10'),
('Chris', 'Miller', 4, '2022-03-15');
```

### Insert Data into `projects`

```sql
INSERT INTO projects (project_name, department_id, start_date) VALUES
('Project A', 1, '2023-06-01'),
('Project B', 2, '2023-08-15'),
('Project C', 1, '2023-07-20'),
('Project D', 4, '2023-09-10');
```

### Insert Data into `salaries`

```sql
INSERT INTO salaries (employee_id, salary, effective_date) VALUES
(1, 70000, '2023-01-01'),
(2, 65000, '2023-01-01'),
(3, 75000, '2023-01-01'),
(4, 60000, '2023-01-01'),
(5, 58000, '2023-01-01');
```

---

## 4. Practice Joins

### INNER JOIN

An `INNER JOIN` returns only the rows that have matching values in both tables.

Example: Get a list of employees along with their department names:

```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id;
```

### LEFT JOIN (or LEFT OUTER JOIN)

A `LEFT JOIN` returns all records from the left table and matching records from the right table. If there is no match, `NULL` is returned for columns from the right table.

Example: Get a list of employees and their projects, including employees who are not assigned to any project:

```sql
SELECT e.first_name, e.last_name, p.project_name
FROM employees e
LEFT JOIN projects p ON e.department_id = p.department_id;
```

### RIGHT JOIN (or RIGHT OUTER JOIN)

A `RIGHT JOIN` returns all records from the right table and matching records from the left table. If there is no match, `NULL` is returned for columns from the left table.

Example: Get a list of projects and the employees working on them (show projects even if no employee is assigned to them):

```sql
SELECT p.project_name, e.first_name, e.last_name
FROM projects p
RIGHT JOIN employees e ON p.department_id = e.department_id;
```

### FULL OUTER JOIN (Simulated)

MySQL does not directly support `FULL OUTER JOIN`. However, you can simulate it by using `UNION` to combine `LEFT JOIN` and `RIGHT JOIN`.

Example: Get all employees and all projects, even if there is no match:

```sql
SELECT e.first_name, e.last_name, p.project_name
FROM employees e
LEFT JOIN projects p ON e.department_id = p.department_id
UNION
SELECT e.first_name, e.last_name, p.project_name
FROM employees e
RIGHT JOIN projects p ON e.department_id = p.department_id;
```

### Aggregate Functions with JOIN

You can use aggregate functions like `COUNT`, `SUM`, etc., with joins.

Example: Get the number of employees in each department:

```sql
SELECT d.department_name, COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id
GROUP BY d.department_name;
```

---

## 5. Advanced Joins

### Join with Multiple Tables

You can join more than two tables together by chaining `JOIN` operations.

Example: Get a list of employees along with their department names, project names, and salaries:

```sql
SELECT e.first_name, e.last_name, d.department_name, p.project_name, s.salary
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id
LEFT JOIN projects p ON e.department_id = p.department_id
INNER JOIN salaries s ON e.employee_id = s.employee_id;
```

### Self-Join

A **self-join** is a join where a table is joined with itself. This can be useful when you need to find relationships between rows in the same table.

Example: Find employees who work in the same department as John Doe:

```sql
SELECT e1.first_name, e1.last_name
FROM employees e1
INNER JOIN employees e2 ON e1.department_id = e2.department_id
WHERE e2.first_name = 'John' AND e2.last_name = 'Doe';
```

### Using Aliases

Aliases are used to give a temporary name to a table or a column for better readability and convenience.

Example:

```sql
SELECT e.first_name AS EmployeeName, d.department_name AS Department
FROM employees e
INNER JOIN departments d ON e.department_id = d.department_id;
```

### `ON` vs `USING` in Joins

- **`ON`**: Used when you need to specify a join condition explicitly. Commonly used with complex conditions.
- **`USING`**: Used when you want to join on columns with the same name in both tables.

Example with `USING`:

```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d USING (department_id);
```

---