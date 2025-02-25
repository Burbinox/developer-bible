# SQL
- [ACID](#acid)
- [Database Scaling Methods](#database_scaling_methods)
- [Difference between DELETE, DROP and TRUNCATE](#difference_between_delete_drop_and_truncate)
- [Index in database](#index_in_database)
- [Normalization](#normalization)
- [SELECT DISTINCT](#select_distinct)

## ACID <a name="acid"></a>
ACID is a set of properties of database transactions:
- Atomicity: This property ensures that a transaction is treated as a single, indivisible unit of work. If any part of the transaction fails, the entire transaction is rolled back, and the database is returned to its original state before the transaction started.
- Consistency: This property ensures that the database remains in a consistent state before and after a transaction. In other words, a transaction should not leave the database in an inconsistent state where the data violates any constraints or rules.
- Isolation: This property ensures that each transaction is isolated from other transactions running concurrently on the database. Each transaction must execute as if it is the only transaction running on the database, and it should not interfere with the correctness of other concurrent transactions.
- Durability: This property ensures that the changes made by a committed transaction are permanent and persistent. Once a transaction is committed, its changes should be saved and remain in the database even in the event of a system failure or crash.

## Database Scaling Methods <a name="database_scaling_methods"></a>

- Read replicas - There is one database for writing and many for reading. It allows to speed up read process but it can cause data inconsistency.
- Sharding - The database is split into more databases. Every DB has some part of the data.

## Difference between DELETE, DROP and TRUNCATE <a name="difference_between_delete_drop_and_truncate"></a>
- DELETE deletes a record from table 
- DROP deletes whole table 
- TRUNCATE deletes all records in table

## Index in database <a name="index_in_database"></a>
Index in a database creates a data structure that speeds up the reading process but slows down the write/update/delete process because the index data structure needs to be updated to reflect the changes made.

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