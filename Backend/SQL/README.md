# SQL
- [ACID](#acid)
- [Clustered index and non-clustered index](#clustered_index_and_non-clustered_index)
- [Database Scaling Methods](#database_scaling_methods)
- [Difference between DELETE, DROP and TRUNCATE](#difference_between_delete_drop_and_truncate)
- [Difference between WHERE and HEAVING](#difference_between_where_and_heaving)
- [Index in database](#index_in_database)
- [JOIN and UNION](#join_and_union)
- [Normalization](#normalization)
- [Scaling methods](#scaling_methods)
- [SELECT DISTINCT](#select_distinct)

## ACID <a name="acid"></a>
ACID is a set of properties of database transactions:
- Atomicity: This property ensures that a transaction is treated as a single, indivisible unit of work. If any part of the transaction fails, the entire transaction is rolled back, and the database is returned to its original state before the transaction started.
- Consistency: This property ensures that the database remains in a consistent state before and after a transaction. In other words, a transaction should not leave the database in an inconsistent state where the data violates any constraints or rules.
- Isolation: This property ensures that each transaction is isolated from other transactions running concurrently on the database. Each transaction must execute as if it is the only transaction running on the database, and it should not interfere with the correctness of other concurrent transactions.
- Durability: This property ensures that the changes made by a committed transaction are permanent and persistent. Once a transaction is committed, its changes should be saved and remain in the database even in the event of a system failure or crash.

## Clustered index and non-clustered index <a name="clustered_index_and_non-clustered_index"></a>
- Clustered index - creating clustered index physically sorts and reorganizes the data on disk, usually by the primary key (PRIMARY KEY) by default. At the same time, it creates a data structure in the form of a B-Tree, which significantly speeds up reading and searching data based on that key.
- non-clustered index - an additional index created on one or more columns that also creates a separate data structure (a B-Tree). It contains the index keys and pointers to the original data in the table, enabling fast access to records based on those columns without changing the physical order of the data.
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    LastName VARCHAR(50),
    Department VARCHAR(50),
    HireDate DATE
);

CREATE NONCLUSTERED INDEX idx_LastName ON Employees(LastName);

SELECT * FROM Employees WHERE EmployeeID = 123;  -- use clustered index
SELECT * FROM Employees WHERE LastName = 'Kowalski';  -- use non-lustered index
```

## Database Scaling Methods <a name="database_scaling_methods"></a>
- Vertical scaling (scaling up) - increasing the capacity of a single server, by adding more CPU, RAM, or bigger/faster storage 
- Horizontal scaling (scaling out) - adding more servers/nodes to a system so that the workload is distributed across multiple machines. The following methods are commonly used: Read replicas - There is one database for writing and many for reading. It allows to speed up read process but it can cause data inconsistency. Sharding - The database is split into more databases. Every DB has some part of the data.

## Difference between DELETE, DROP and TRUNCATE <a name="difference_between_delete_drop_and_truncate"></a>
- DELETE deletes a record from table 
- DROP deletes whole table 
- TRUNCATE deletes all records in table

## Difference between WHERE and HEAVING <a name="difference_between_where_and_heaving"></a>
- HAVING filters grouped and aggregated results after GROUP BY (e.g., SUM(), COUNT(), AVG())
- WHERE filters individual rows based on conditions before grouping
``` sql 
-- WHERE filters rows before grouping
SELECT Customer, SUM(Amount) AS TotalAmount
FROM Orders
WHERE Amount > 40
GROUP BY Customer;

-- HAVING filters groups after grouping
SELECT Customer, SUM(Amount) AS TotalAmount
FROM Orders
GROUP BY Customer
HAVING SUM(Amount) > 70;

```

## Index in database <a name="index_in_database"></a>
Index in a database creates a data structure that speeds up the reading process but slows down the write/update/delete process because the index data structure needs to be updated to reflect the changes made.

## JOIN and UNION <a name="join_and_union"></a>
- LEFT JOIN — returns all rows from the left table plus matched rows from the right table (NULL if no match in right table)
```sql
SELECT A.id, A.name, B.city
FROM A
LEFT JOIN B ON A.id = B.id;
```

- RIGHT JOIN — returns all rows from the right table plus matched rows from the left table (NULL if no match in left table)
```sql
SELECT A.id, A.name, B.city
FROM A
RIGHT JOIN B ON A.id = B.id;
```

- FULL JOIN — returns all rows from both tables, with NULLs where there’s no match on either side
```sql
SELECT A.id, A.name, B.city
FROM A
FULL JOIN B ON A.id = B.id;
```

- INNER JOIN — returns only the rows that have matching values in both tables
```sql
SELECT A.id, A.name, B.city
FROM A
INNER JOIN B ON A.id = B.id;
```

- UNION - combines the results of two or more SELECT queries by stacking them vertically (one after another). It removes duplicates by default (use UNION ALL to keep all duplicates). All queries involved must have the same number of columns and compatible data types in corresponding positions.
```sql
SELECT * FROM A
UNION
SELECT * FROM B;
```

- CROSS JOIN —  returns all possible combinations of rows from both tables. 
```sql
SELECT * FROM A, B;
SELECT * FROM A CROSS JOIN B;
```

## Normalization <a name="normalization"></a>
It is dividing large tables into smaller, related tables and defining relationships between them using foreign keys.
Normalization reduces data redundancy, so nothing is stored twice. This makes it easier to update information and helps prevent mistakes!

**Before Normalization (Single Table)**
| StudentID | Name  | Course  | Professor     |
|-----------|-------|--------|----------------|
| 1         | Alice | Math    | Dr. Smith      |
| 1         | Alice | Physics | Dr. Johnson    |
| 2         | Bob   | Math    | Dr. Smith      |


**Students Table:**  
| StudentID | Name  |
|-----------|-------|
| 1         | Alice |
| 2         | Bob   |

**Enrollments Table:**  
| EnrollmentID | StudentID | Course  | Professor     |
|--------------|-----------|---------|----------------|
| 1            | 1         | Math    | Dr. Smith      |
| 2            | 1         | Physics | Dr. Johnson    |
| 3            | 2         | Math    | Dr. Smith      |

## SELECT DISTINCT <a name="select_distinct"></a>
return unique values from a specified column by eliminating duplicate entries in the result set.
``` sql
SELECT Country FROM Customers; --> Returns: Germany, Poland, Poland, USA
```

``` sql
SELECT DISTINCT Country FROM Customers; --> Returns: Germany, Poland, USA
```