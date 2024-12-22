## MySQL Foreign Key

A **foreign key** is a field (or collection of fields) in one table that uniquely identifies a row of another table. It establishes a relationship between two tables by enforcing a link between the foreign key column(s) and the primary key column(s) of the referenced table.

### Key Concepts

1. **Primary Key (PK)**
   - Uniquely identifies each row in a table.
   - Must contain unique values and cannot be NULL.

2. **Foreign Key (FK)**
   - A column (or columns) that creates a relationship between two tables.
   - Ensures referential integrity by linking to a primary key in another table.

### Creating Foreign Key Constraints

1. **Syntax**
   ```sql
   CREATE TABLE child_table (
       id INT PRIMARY KEY,
       parent_id INT,
       FOREIGN KEY (parent_id) REFERENCES parent_table(id)
   );
   ```

2. **Using ALTER TABLE**
   ```sql
   ALTER TABLE child_table
   ADD CONSTRAINT fk_parent
   FOREIGN KEY (parent_id) REFERENCES parent_table(id);
   ```

### Example

1. **Parent Table (Departments)**
   ```sql
   CREATE TABLE Departments (
       DeptID INT PRIMARY KEY,
       DeptName VARCHAR(100) NOT NULL
   );
   ```

2. **Child Table (Employees)**
   ```sql
   CREATE TABLE Employees (
       EmpID INT PRIMARY KEY,
       EmpName VARCHAR(100) NOT NULL,
       DeptID INT,
       FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
   );
   ```

### Referential Actions

- **ON DELETE CASCADE**
  - Deletes all rows in the child table that are related to the deleted row in the parent table.
  ```sql
  FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
  ON DELETE CASCADE;
  ```

- **ON UPDATE CASCADE**
  - Updates all rows in the child table when the referenced row in the parent table is updated.
  ```sql
  FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
  ON UPDATE CASCADE;
  ```

### Benefits

- **Data Integrity**: Ensures that the data in one table is related to the data in another.
- **Consistency**: Maintains consistent relationships between tables.
- **Prevents Orphans**: Avoids orphaned records in the child table by enforcing referential integrity.