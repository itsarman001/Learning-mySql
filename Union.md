
# Bookstore Database Project

This project is designed to help you practice various SQL concepts including creating databases, tables, views, self-joins, and using UNION and UNION ALL. The database represents a bookstore with information about books and their authors.

## Database Structure

### Database
- `BookstoreDB`

### Tables
1. **Authors**
   - `AuthorID` (INT, Primary Key)
   - `FirstName` (VARCHAR(50))
   - `LastName` (VARCHAR(50))

2. **Books**
   - `BookID` (INT, Primary Key)
   - `Title` (VARCHAR(100))
   - `AuthorID` (INT, Foreign Key)
   - `Genre` (VARCHAR(50))
   - `Price` (DECIMAL(10, 2))
   - `PublicationDate` (DATE)

## Sample Data

### Authors Table

| AuthorID | FirstName | LastName      |
|----------|-----------|---------------|
| 1        | George    | Orwell        |
| 2        | Jane      | Austen        |
| 3        | J.K.      | Rowling       |
| 4        | Mark      | Twain         |
| 5        | Agatha    | Christie      |

### Books Table

| BookID | Title                                   | AuthorID | Genre      | Price | PublicationDate |
|--------|-----------------------------------------|----------|------------|-------|-----------------|
| 1      | 1984                                    | 1        | Dystopian  | 9.99  | 1949-06-08      |
| 2      | Pride and Prejudice                     | 2        | Romance    | 12.99 | 1813-01-28      |
| 3      | Harry Potter and the Sorcerer's Stone   | 3        | Fantasy    | 19.99 | 1997-06-26      |
| 4      | Adventures of Huckleberry Finn          | 4        | Adventure  | 8.99  | 1884-12-10      |
| 5      | Murder on the Orient Express            | 5        | Mystery    | 10.99 | 1934-01-01      |

## SQL Queries

### 1. Create View
Create a view to show books with their authors' names.

```sql
CREATE VIEW BookAuthor AS
SELECT b.BookID, b.Title, a.FirstName, a.LastName, b.Genre, b.Price, b.PublicationDate
FROM Books b
JOIN Authors a ON b.AuthorID = a.AuthorID;
```

### 2. Self Join
Find books that share the same author.

```sql
SELECT b1.Title AS Book1, b2.Title AS Book2, a.FirstName, a.LastName
FROM Books b1
JOIN Books b2 ON b1.AuthorID = b2.AuthorID AND b1.BookID <> b2.BookID
JOIN Authors a ON b1.AuthorID = a.AuthorID;
```

### 3. UNION and UNION ALL
Combine results of two queries - one for books in the 'Fantasy' genre and another for all books.

```sql
-- UNION (removes duplicates)
SELECT Title, Genre, Price
FROM Books
WHERE Genre = 'Fantasy'
UNION
SELECT Title, Genre, Price
FROM Books;

-- UNION ALL (includes duplicates)
SELECT Title, Genre, Price
FROM Books
WHERE Genre = 'Fantasy'
UNION ALL
SELECT Title, Genre, Price
FROM Books;
```

## How to Run

1. **Create Database and Tables:**
   ```sql
   CREATE DATABASE BookstoreDB;
   USE BookstoreDB;

   CREATE TABLE Authors (
       AuthorID INT PRIMARY KEY,
       FirstName VARCHAR(50),
       LastName VARCHAR(50)
   );

   CREATE TABLE Books (
       BookID INT PRIMARY KEY,
       Title VARCHAR(100),
       AuthorID INT,
       Genre VARCHAR(50),
       Price DECIMAL(10, 2),
       PublicationDate DATE
   );
   ```

2. **Insert Sample Data:**
   ```sql
   INSERT INTO Authors (AuthorID, FirstName, LastName)
   VALUES 
   (1, 'George', 'Orwell'),
   (2, 'Jane', 'Austen'),
   (3, 'J.K.', 'Rowling'),
   (4, 'Mark', 'Twain'),
   (5, 'Agatha', 'Christie');

   INSERT INTO Books (BookID, Title, AuthorID, Genre, Price, PublicationDate)
   VALUES 
   (1, '1984', 1, 'Dystopian', 9.99, '1949-06-08'),
   (2, 'Pride and Prejudice', 2, 'Romance', 12.99, '1813-01-28'),
   (3, 'Harry Potter and the Sorcerer''s Stone', 3, 'Fantasy', 19.99, '1997-06-26'),
   (4, 'Adventures of Huckleberry Finn', 4, 'Adventure', 8.99, '1884-12-10'),
   (5, 'Murder on the Orient Express', 5, 'Mystery', 10.99, '1934-01-01');
   ```