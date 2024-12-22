# MySQL Notes

MySQL is a popular open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) for managing data in relational databases.

---

## Structured Query Language (SQL)

- **S**: Structured
- **Q**: Query
- **L**: Language

### Key Features:
- SQL is not case-sensitive.
- MySQL databases consist of tables that store data in a structured format.
- Each table is made up of rows and columns:
  - Rows represent individual data records.
  - Columns represent specific attributes or fields within those records.

---

## Database Management

### Creating a Database

```sql
CREATE DATABASE database_name;
```
- Replace `database_name` with the desired name for your database.

### Selecting a Database

```sql
USE database_name;
```
- Choose the database you want to work with.

### Deleting a Database

```sql
DROP DATABASE database_name;
```
- **Caution**: Deleting a database is irreversible.

### Altering a Database

```sql
-- Set database to read-only
ALTER DATABASE database_name READ ONLY = 1;

-- Remove read-only mode
ALTER DATABASE database_name READ ONLY = 0;
```

---

## Table Management

### Creating a Table

```sql
CREATE TABLE table_name (
  column1 data_type constraint1,
  column2 data_type constraint2,
  ...
);
```
- Replace `table_name` with your desired table name.
- Specify the data type for each column (e.g., `VARCHAR`, `INT`, `DECIMAL`, `DATE`).
- Define constraints as needed (e.g., `PRIMARY KEY`, `NOT NULL`, `UNIQUE`, `DEFAULT`).

#### Example Table

```sql
CREATE TABLE employees (
  employee_id VARCHAR(10),
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email_id VARCHAR(50) NOT NULL,
  phone_number INT(15),
  designation VARCHAR(100) NOT NULL,
  hourly_pay DECIMAL(5, 2) NOT NULL,
  hire_date DATE NOT NULL
);

-- Adding a primary key constraint
ALTER TABLE employees
ADD CONSTRAINT PRIMARY KEY (employee_id);
```

### Common Constraints

- **PRIMARY KEY**: Uniquely identifies each row in a table (a table can only have one primary key).
- **NOT NULL**: Ensures a column cannot have `NULL` values.
- **UNIQUE**: Prevents duplicate values within a column.
- **DEFAULT**: Sets a default value for a column if no value is explicitly provided during insertion.

#### Example of Constraints

```sql
-- UNIQUE Constraint
CREATE TABLE unique_example (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(255) UNIQUE
);

-- NOT NULL Constraint
CREATE TABLE not_null_example (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL
);

-- DEFAULT Value
CREATE TABLE cafeteria (
  product_id INT AUTO_INCREMENT PRIMARY KEY,
  product_name VARCHAR(100),
  price DECIMAL(4, 2) DEFAULT 0.00
);

-- Alter an existing table to add a default value
ALTER TABLE cafeteria
ALTER price SET DEFAULT 0.00;
```

### Modifying Tables

#### Adding a Column

```sql
ALTER TABLE table_name
ADD column_name data_type;
```

#### Changing a Column Type

```sql
ALTER TABLE table_name
MODIFY COLUMN column_name new_data_type;
```

#### Renaming a Column

```sql
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

#### Changing Column Order

```sql
ALTER TABLE table_name
MODIFY column_name data_type
AFTER another_column;

-- Move column to the first position
ALTER TABLE table_name
MODIFY column_name data_type FIRST;
```

### Deleting a Table

```sql
DROP TABLE table_name;
```

---

## Table Rows

### Inserting Data

#### Insert a Row

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

#### Insert Multiple Rows

```sql
INSERT INTO employees (employee_id, first_name, last_name, email_id, phone_number, designation, hourly_pay, hire_date) VALUES
('E001', 'Alice', 'Johnson', 'alice.johnson@example.com', 1234567890, 'Software Engineer', 45.00, '2022-01-15'),
('E002', 'Bob', 'Smith', 'bob.smith@example.com', 9876543210, 'Project Manager', 60.50, '2020-06-20');
```

### Retrieving Data

#### Select All Columns

```sql
SELECT * FROM table_name;
```

#### Select Specific Columns

```sql
SELECT column1, column2 FROM table_name;
```

#### Filtering Results

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

### Updating Data

```sql
UPDATE table_name
SET column1 = new_value1, column2 = new_value2
WHERE condition;
```

### Deleting Data

```sql
DELETE FROM table_name WHERE condition;

-- Delete all rows
DELETE FROM table_name;
```

---

## Transactions

- Transactions group multiple operations into a single unit.
- Ensure data consistency by committing all changes or rolling back if an error occurs.

### Autocommit Mode

```sql
SET autocommit = 0; -- Disable autocommit
SET autocommit = 1; -- Enable autocommit
```

### Commit Changes

```sql
COMMIT;
```

### Rollback Changes

```sql
ROLLBACK;
```

---

## Miscellaneous Functions

### Fetching Current Date and Time

```sql
SELECT CURRENT_DATE(); -- Current date
SELECT CURRENT_TIME(); -- Current time
SELECT NOW();          -- Current date and time
```

### Using CHECK Constraints

- CHECK constraints limit the values that can be entered into a column.

```sql
ALTER TABLE employees
ADD CONSTRAINT check_hourly_pay CHECK (hourly_pay >= 20);

-- Dropping a CHECK constraint
ALTER TABLE employees
DROP CHECK check_hourly_pay;

-- Example: Inserting data violating the CHECK constraint
INSERT INTO employees (employee_id, first_name, last_name, email_id, designation, hourly_pay) VALUES
('E016', 'Alice', 'Johnson', 'alice.johnson@example.com', 'Software Engineer', 15); -- Will fail if CHECK exists
```
