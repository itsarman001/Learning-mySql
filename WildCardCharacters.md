# SQL Wildcard Characters

## Definition
Wildcard characters are special symbols used in SQL to represent one or more characters during pattern matching, allowing flexible text searches within database queries.

## Types of Wildcard Characters

### 1. % (Percent) Wildcard
#### Definition
Represents zero, one, or multiple characters in a string

#### Description
- Most commonly used wildcard character
- Allows flexible text searching
- Can be placed before, after, or around search term

#### Syntax
```sql
WHERE column_name LIKE '%pattern%'
```

#### Example
```sql
SELECT employee_id,
CONCAT(first_name, " ", last_name) AS full_name,
email_id, designation
FROM `employees`
WHERE designation LIKE "%Manager";
```

### 2. _ (Underscore) Wildcard
#### Definition
Represents exactly one single character

#### Description
- Matches precisely one character in a specific position
- Useful for precise pattern matching
- Can replace single character in search

#### Syntax
```sql
WHERE column_name LIKE '_pattern'
```

#### Example
```sql
SELECT employee_id,
CONCAT(first_name, " ", last_name) AS full_name,
email_id, hire_date
FROM `employees`
WHERE hire_date LIKE "2022-__-__";
```

### 3. [] (Square Brackets) Wildcard
#### Definition
Represents any single character within the specified range or set

#### Description
- Allows matching characters within defined set
- Can specify character ranges
- Provides character-level filtering

#### Syntax
```sql
WHERE column_name LIKE '[A-C]%'
```

#### Example
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       email_id
FROM `employees`
WHERE first_name LIKE '[A-E]%';

/* It is not supported by MySQL, as MySQL doesn't interpret character ranges like [A-E] in the LIKE clause. Instead, you can use a combination of conditions with OR or use REGEXP for pattern matching.
*/

SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       email_id
FROM `employees`
WHERE first_name REGEXP '^[A-E]';
```

### 4. [!] Wildcard
#### Definition
Represents characters NOT in the specified range

#### Description
- Negates character matching
- Excludes specified character set
- Useful for filtering out specific patterns

#### Syntax
```sql
WHERE column_name LIKE '[!A-C]%'
```

#### Example
```sql
SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       email_id
FROM employees
WHERE first_name LIKE '[!A-C]%';

/* It is not supported by MySQL, as MySQL doesn't interpret character ranges like [A-E] in the LIKE clause. Instead, you can use a combination of conditions with OR or use REGEXP for pattern matching.
*/

SELECT employee_id,
       CONCAT(first_name, " ", last_name) AS full_name,
       email_id
FROM employees
WHERE first_name REGEXP '^[!A-C]';

```

## Pro Tips
- Always use LIKE operator with wildcards
- Be cautious with performance on large datasets
- Combine wildcards for complex pattern matching
- Test queries with sample data before production use

## Compatibility
Wildcard usage is supported across most SQL databases:
- MySQL
- PostgreSQL
- Oracle
- SQL Server
- SQLite