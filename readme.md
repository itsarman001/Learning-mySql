# MySQL

## Structured Query Language (SQL)
- **S**: Structured  
- **Q**: Query  
- **L**: Language

SQL is a relational database language. It is not case-sensitive.

---

## Database
### Create Database:
```sql
CREATE DATABASE database_name;
```
### Select Database:
```sql
USE database_name;
```
### Delete Database:
```sql
DROP DATABASE database_name;
```
### Alter Database:
```sql
-- Set database to read-only
ALTER DATABASE database_name READ ONLY = 1;

-- Remove read-only mode
ALTER DATABASE database_name READ ONLY = 0;
```

---

## Table
### Create a Table:
```sql
CREATE TABLE employees (
  employee_id VARCHAR(10) PRIMARY KEY,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email_id VARCHAR(50) NOT NULL,
  phone_number INT(15),
  designation VARCHAR(100) NOT NULL,
  hourly_pay DECIMAL(5, 2) NOT NULL,
  hire_date DATE NOT NULL
);
```
### Unique Constraints:
```sql
-- Ensure column values are unique
CREATE TABLE unique_example (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(255) UNIQUE
);
```
### Not Null Constraints:
```sql
-- Ensure column values cannot be NULL
CREATE TABLE not_null_example (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL
);
```

### Delete a Table:
```sql
DROP TABLE table_name;
```
### Select a Table:
```sql
SELECT * FROM table_name;
```
### Add a Column:
```sql
ALTER TABLE table_name
ADD phone_number INT(10);
```
### Change a Column Type:
```sql
ALTER TABLE employees
MODIFY COLUMN email_id VARCHAR(50);
```
### Change a Column Name:
```sql
-- Rename using RENAME COLUMN syntax (supported in recent MySQL versions)
ALTER TABLE employees
RENAME COLUMN email_address TO email_id;

-- For older versions, use CHANGE COLUMN:
ALTER TABLE employees
CHANGE COLUMN email_address email_id VARCHAR(100) NOT NULL;
```
### Change Order of a Column:
```sql
ALTER TABLE employees
MODIFY email_id VARCHAR(50)
AFTER last_name;

-- To move it to the first position, use:
ALTER TABLE employees
MODIFY email_id VARCHAR(50) FIRST;
```

---

## Table Rows
### Insert a Row:
```sql
INSERT INTO employees VALUES
('E001', 'Alice', 'Johnson', 'alice.johnson@example.com', 1234567890, 'Software Engineer', 45.00, '2022-01-15');
```
### Insert a Row with Selected Columns:
```sql
INSERT INTO employees (employee_id, first_name, last_name, email_id, designation) VALUES
('E001', 'Alice', 'Johnson', 'alice.johnson@example.com', 'Software Engineer');
```
### Practice Data:
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

## Retrieve Data from Database:
```sql
-- Fetch all data
SELECT * FROM employees;

-- Fetch specific columns:
SELECT first_name FROM employees WHERE first_name = 'Bob';

-- Fetch data where it is not equal
SELECT * FROM employees WHERE first_name != 'Bob';

-- Fetch data where hourly_pay is greater than or equal to 40
SELECT * FROM employees WHERE hourly_pay >= 40;

-- Fetch data where hourly_pay is less than or equal to 40
SELECT * FROM employees WHERE hourly_pay <= 40;

-- Fetch data where phone_number is NULL
SELECT * FROM employees WHERE phone_number IS NULL;

-- Fetch data where phone_number is NOT NULL
SELECT * FROM employees WHERE phone_number IS NOT NULL;
```

---

## Update and Delete Data
### Update Data:
```sql
-- Update a single column
UPDATE employees
SET phone_number = 2343576890
WHERE employee_id = 'E003';

-- Update multiple columns
UPDATE employees
SET designation = 'Senior Software Engineer', hourly_pay = 50.00
WHERE employee_id = 'E001';
```
### Delete Data:
```sql
-- Delete a specific row
DELETE FROM employees WHERE employee_id = 'E012';

-- Delete all rows (use with caution!)
DELETE FROM employees;
```

---

## Transactions: Autocommit, Commit, and Rollback
### Autocommit:
```sql
SET autocommit = 0; -- Disable autocommit
SET autocommit = 1; -- Enable autocommit
```
### Commit:
```sql
COMMIT; -- Save changes permanently
```
### Rollback:
```sql
ROLLBACK; -- Undo changes made in the transaction
```

---

## Miscellaneous Functions
### Current Date and Time:
```sql
SELECT CURRENT_DATE(); -- Fetch the current date
SELECT CURRENT_TIME(); -- Fetch the current time
SELECT NOW(); -- Fetch the current date and time
```
