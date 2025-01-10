
# ORDER BY Clause in MySQL

## Definition
- A SQL clause used to sort query results based on one or more columns
- Allows sorting in ascending or descending order

## Syntax
```sql
SELECT column1, column2
FROM table_name
ORDER BY column_name [ASC|DESC];
```

## 1. Single Column Sorting
### Ascending Order (Default)
- Sorts from lowest to highest
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, hourly_pay
FROM employees
ORDER BY hourly_pay;
```

### Descending Order
- Sorts from highest to lowest
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, hourly_pay
FROM employees
ORDER BY hourly_pay DESC;
```

## 2. Multiple Column Sorting
### Description
- Allows sorting by multiple columns
- Applies sorting in order of column specification
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, hourly_pay
FROM employees
ORDER BY hourly_pay DESC, designation;
```

## 3. Sorting by Column Position
### Description
- Sort using column index instead of name
```sql
SELECT first_name, last_name, hourly_pay
FROM employees
ORDER BY 3 DESC;
-- Sorts by 3rd column (hourly_pay)
```

## 4. Sorting with Expressions
### Description
- Create calculated columns for sorting
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation,
       hourly_pay * 9 AS per_day_cost
FROM employees
ORDER BY per_day_cost DESC;
```

## 5. Handling NULL Values
### Techniques
```sql
-- NULL values first
SELECT * FROM employees 
ORDER BY commission_pct ASC NULLS FIRST;
-- Upper method is supported only in SQL databases like PostgreSQL or Oracle.

-- in my Sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, phone_number
FROM employees
ORDER BY phone_number IS NULL ASC;

-- NULL values last
SELECT * FROM employees 
ORDER BY commission_pct DESC NULLS LAST;
-- Upper method is supported only in SQL databases like PostgreSQL or Oracle.

-- in my Sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, phone_number
FROM employees
ORDER BY phone_number IS NULL DESC;
```

## 6. Case-Insensitive Sorting
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       designation, email_id, phone_number
FROM employees
ORDER BY LOWER(last_name)
```