# SQL Logical Operators

## 1. AND Operator
### Definition
A logical operator that returns records when **all specified conditions are true**

### Description
- Combines multiple conditions in a WHERE clause
- Requires all conditions to be met simultaneously
- Used to filter data with strict multiple criteria

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3;
```

### Example
```sql
SELECT employee_id, CONCAT(first_name, " ", last_name) AS full_name, email_id
FROM `employees`
WHERE designation = "Software Engineer" and phone_number IS NOT NULL;
```

## 2. OR Operator
### Definition
A logical operator that returns records when **at least one condition is true**

### Description
- Allows retrieving rows that satisfy any of the specified conditions
- More flexible compared to AND operator
- Useful for broader data selection

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3;
```

### Example
```sql
SELECT employee_id, CONCAT(first_name, " ", last_name) AS full_name, email_id, designation
FROM `employees`
WHERE designation = "Software Engineer" OR phone_number IS NOT NULL;
```

## 3. BETWEEN Operator
### Definition
Selects values within a specified range

### Description
- Inclusive range selection
- Works with numeric, text, and date values
- Simplifies range-based queries

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Example
```sql
SELECT employee_id, CONCAT(first_name, " ", last_name) AS full_name, email_id, hourly_pay
FROM `employees`
WHERE hourly_pay BETWEEN 40 AND 50;
```

## 4. NOT Operator
### Definition
Negates a condition, returning opposite results

### Description
- Reverses boolean result of a condition
- Used to exclude specific records
- Can be combined with other operators

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

### Example
```sql
SELECT employee_id, CONCAT(first_name, " ", last_name) AS full_name, email_id, designation
FROM `employees`
WHERE NOT designation = "Software Engineer"
```

## 5. IN Operator
### Definition
Allows multiple value matching in a single condition

### Description
- Checks if a value matches any value in a list
- Simplifies multiple OR conditions
- Improves query readability and performance

### Syntax
```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

### Example
```sql
SELECT employee_id,
CONCAT(first_name, " ", last_name) AS full_name,
email_id, designation
FROM `employees`
WHERE designation IN ("Software Engineer", "DevOps Engineer")
```

## Pro Tips
- Combine logical operators for complex queries
- Use parentheses to control operator precedence
- Consider query performance with complex conditions
- Always test queries with sample data