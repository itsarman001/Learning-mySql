# Employees Table Structure and Documentation

## Overview

This document outlines the creation and structure of the `employees` table, its constraints, and the corresponding data insertion commands. The table is designed to manage employee records in a structured manner.

---

## Table Structure

### Create Table Command

```sql
CREATE TABLE employees (
  employee_id VARCHAR(10) PRIMARY KEY, -- Unique identifier for each employee
  first_name VARCHAR(100) NOT NULL, -- Employee's first name
  last_name VARCHAR(100) NOT NULL, -- Employee's last name
  email_id VARCHAR(100) NOT NULL UNIQUE, -- Employee's email, must be unique
  phone_number BIGINT UNIQUE DEFAULT NULL, -- Unique phone number, defaults to NULL if not provided
  designation VARCHAR(100) NOT NULL, -- Job title of the employee
  hourly_pay DECIMAL(6, 2) NOT NULL CHECK (hourly_pay >= 20), -- Hourly pay, must be >= 20
  hire_date DATE NOT NULL DEFAULT CURRENT_DATE -- Date of hire, defaults to current date
);
```

---

### Explanation of Columns

| Column Name    | Data Type      | Constraints              | Description                                      |
| -------------- | -------------- | ------------------------ | ------------------------------------------------ |
| `employee_id`  | `VARCHAR(10)`  | `PRIMARY KEY`            | Unique identifier for each employee.             |
| `first_name`   | `VARCHAR(100)` | `NOT NULL`               | Employee's first name.                           |
| `last_name`    | `VARCHAR(100)` | `NOT NULL`               | Employee's last name.                            |
| `email_id`     | `VARCHAR(100)` | `NOT NULL`, `UNIQUE`     | Employee's email, must be unique.                |
| `phone_number` | `BIGINT`       | `UNIQUE`, `DEFAULT NULL` | Unique phone number, defaults to NULL if absent. |
| `designation`  | `VARCHAR(100)` | `NOT NULL`               | Job title of the employee.                       |
| `hourly_pay`   | `DECIMAL(6,2)` | `NOT NULL`, `CHECK`      | Hourly pay rate, must be >= 20.                  |
| `hire_date`    | `DATE`         | `NOT NULL`, `DEFAULT`    | Date of hire, defaults to the current date.      |

---

## Data Constraints

1. **`PRIMARY KEY`**:
   - Ensures each employee has a unique identifier (`employee_id`).
2. **`UNIQUE`**:
   - Enforces unique values for `email_id` and `phone_number`.
3. **`NOT NULL`**:
   - Prevents empty values for critical fields (`first_name`, `last_name`, `email_id`, `designation`, `hourly_pay`, `hire_date`).
4. **`DEFAULT`**:
   - `phone_number` defaults to `NULL` when not provided.
   - `hire_date` defaults to the current date if not specified.
5. **`CHECK`**:
   - Ensures `hourly_pay` is at least 20.

---

## Sample Data Insertion

### Insert Data Command

```sql
INSERT INTO employees (employee_id, first_name, last_name, email_id, phone_number, designation, hourly_pay, hire_date) VALUES
('E001', 'Alice', 'Johnson', 'alice.johnson@example.com', 1234567890, 'Software Engineer', 45.00, '2022-01-15'),
('E002', 'Bob', 'Smith', 'bob.smith@example.com', 9876543210, 'Project Manager', 60.50, '2020-06-20'),
('E003', 'Charlie', 'Brown', 'charlie.brown@example.com', NULL, 'UX Designer', 40.00, '2021-09-01'),
('E004', 'Dana', 'White', 'dana.white@example.com', 1122334455, 'DevOps Engineer', 50.75, '2019-11-10'),
('E005', 'Evan', 'Green', 'evan.green@example.com', NULL, 'Technical Writer', 35.25, '2023-03-05'),
('E006', 'Alice', 'Brown', 'alice.brown@example.com', 7788990011, 'QA Analyst', 38.50, '2021-07-12'),
('E007', 'John', 'Doe', 'john.doe@example.com', 9988776655, 'Intern', 25.00, '2024-01-01'),
('E008', 'Jane', 'Smith', 'jane.smith@example.com', 5544332211, 'Software Engineer', 45.00, '2022-10-10'),
('E009', 'Bob', 'Johnson', 'bob.johnson@example.com', NULL, 'Business Analyst', 42.00, '2021-05-15'),
('E010', 'Sophia', 'Williams', 'sophia.williams@example.com', 6677889900, 'Marketing Specialist', 48.00, '2020-02-28'),
('E011', 'Mason', 'Taylor', 'mason.taylor@example.com', 3344556677, 'Product Manager', 55.00, '2019-09-10'),
('E012', 'Alice', 'Smith', 'alice.smith@example.com', NULL, 'Software Engineer', 45.00, '2023-04-22'),
('E013', 'Olivia', 'Brown', 'olivia.brown@example.com', NULL, 'Content Writer', 30.50, '2023-06-11'),
('E014', 'Liam', 'Davis', 'liam.davis@example.com', 7766554433, 'HR Specialist', 41.25, '2020-12-01'),
('E015', 'Isabella', 'Wilson', 'isabella.wilson@example.com', 9988112233, 'Finance Analyst', 52.00, '2018-07-30');
```

---

## Query Examples

### Select All Data

```sql
SELECT * FROM employees;
```

### Select Specific Columns

```sql
SELECT first_name, last_name, designation FROM employees;
```

### Filter Data

```sql
-- Employees earning more than 40 per hour
SELECT * FROM employees WHERE hourly_pay > 40;

-- Employees hired in 2023
SELECT * FROM employees WHERE YEAR(hire_date) = 2023;
```

### Update Data

```sql
-- Update phone number for an employee
UPDATE employees
SET phone_number = 4455667788
WHERE employee_id = 'E003';
```

### Delete Data

```sql
-- Delete a specific employee record
DELETE FROM employees WHERE employee_id = 'E015';
```

---

## Additional Notes

- Use constraints to maintain data integrity and avoid duplication.
- Carefully handle `DELETE` operations as they are irreversible.
- Use transactions (`BEGIN`, `COMMIT`, `ROLLBACK`) for critical operations to ensure data consistency.
