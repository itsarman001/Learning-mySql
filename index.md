# mySql

S: STRUCTURED
Q: QUERY
L: LANGUAGE

SQL is a relational database, it is not case sensitise.

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

### ALTER Database:
```sql
# READONLY
ALTER DATABASE database_name READ ONLY = 1;
# !READONLY
ALTER DATABASE database_name READ ONLY = 0;
```

## Table

### Create a table
```sql
CREATE TABLE employees (
  employee_id INT,
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  hourly_pay DECIMAL(5, 2),
  hire_date DATE
);
```

### Delete a Table:
```sql
DROP table_name;
```

### Select a Table:
```sql
SELECT * FROM table_name;
```

### Add a column:
```sql
ALTER TABLE table_name
ADD phone_number INT(10);
```
### Change a column type:
```sql
ALTER TABLE employees
MODIFY COLUMN email_id VARCHAR(50);
```

### Change a column name:
```sql
ALTER TABLE employees
RENAME COLUMN email_address to email_id;
```

### Change order of a column:
```sql
ALTER TABLE employees
MODIFY email_id VARCHAR(50)
AFTER last_name;
```