# MySQL Functions 

## CONCAT Function
### Definition
- String concatenation function that merges multiple strings into a single string

### Description
- Combines text from different columns or literal strings
- Allows adding separators between merged strings
- Useful for creating full names, addresses, or complex text representations

### Syntax
```sql
CONCAT(string1, separator, string2)
```

### Example
```sql
SELECT CONCAT(first_name, " ", last_name) AS full_name, employee_id 
FROM `employees`
```

## COUNT Function
### Definition
- Aggregate function that counts the number of rows or non-null values in a column

### Description
- Returns total count of records matching specified conditions
- Can be used with * to count all rows
- Helps in understanding dataset size and record frequency
- Ignores NULL values when counting specific columns

### Syntax
```sql
COUNT(column_name or *)
```

### Example
```sql
SELECT COUNT(employee_id) AS total_employees 
FROM `employees` 
-- Result: 15
```

## MAX Function
### Definition
- Aggregate function that retrieves the highest/maximum value in a column

### Description
- Works with numeric, date, and text columns
- Returns the maximum value based on column's data type
- Useful for finding highest salaries, latest dates, or alphabetically last names
- Helps in identifying peak or extreme values in datasets

### Syntax
```sql
MAX(column_name)
```

### Example
```sql
SELECT MAX(employee_id) 
FROM `employees`
-- Result: E015
```

## MIN Function
### Definition
- Aggregate function that retrieves the lowest/minimum value in a column

### Description
- Compatible with numeric, date, and text columns
- Returns the minimum value based on column's data type
- Helps in finding lowest salaries, earliest dates, or alphabetically first names
- Useful for understanding dataset's lower boundaries

### Syntax
```sql
MIN(column_name)
```

### Example
```sql
SELECT MIN(employee_id) 
FROM `employees`
-- Result: E001
```

## AVG Function
### Definition
- Aggregate function calculating the arithmetic mean of numeric values

### Description
- Computes average by summing all values and dividing by total count
- Automatically ignores NULL values
- Provides central tendency measure for numerical data
- Useful in statistical analysis and reporting

### Syntax
```sql
AVG(column_name)
```

### Example
```sql
SELECT AVG(hourly_pay) 
FROM `employees`
-- Result: 43.583333
```

## SUM Function
### Definition
- Aggregate function that calculates total sum of numeric values in a column

### Description
- Adds all non-null numeric values
- Useful for calculating total revenue, expenses, quantities
- Provides cumulative insights into numerical data
- Handles decimal and integer values

### Syntax
```sql
SUM(column_name)
```

### Example
```sql
SELECT SUM(hourly_pay) 
FROM `employees`
-- Result: 653.75
```

## Most frequently used MySQL FUNCTIONS

### String Functions
- **CONCAT()**: Combines multiple strings into one
- **LENGTH()**: Returns the length of a string in bytes
- **CHAR()**: Returns character for each integer passed
- **LOWER()**: Converts string to lowercase
- **UPPER()**: Converts string to uppercase
- **TRIM()**: Removes leading and trailing spaces

### Numeric Functions
- **MOD()**: Returns remainder of division
- **POWER()/POW()**: Raises a value to a specified power
- **ROUND()**: Rounds numeric expressions
- **SIGN()**: Returns sign of a number
- **SQRT()**: Calculates square root

### Date and Time Functions
- **MONTH()**: Extracts month from a date
- **YEAR()**: Extracts year from a date
- **NOW()**: Returns current date and time
- **SYSDATE()**: Returns current system date and time
- **CURDATE()**: Returns current date

### Aggregate Functions
- **COUNT()**: Counts number of rows
- **MAX()**: Finds maximum value
- **MIN()**: Finds minimum value
- **AVG()**: Calculates average
- **SUM()**: Calculates total sum

### Comparison Functions
- **COALESCE()**: Returns first non-null value
- **GREATEST()**: Returns highest value
- **LEAST()**: Returns lowest value
- **ISNULL()**: Checks if value is null