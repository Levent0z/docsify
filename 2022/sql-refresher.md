# SQL

- SQL Keywords are not case-sensitive, but use upper-case by convention.
- For standardization, use `;` after each statement
- Single-line comments use `--`, multi-line comments use `/*` and `*/`.

## CRUD for Databases

### Reads
```sql
SHOW DATABASES;
```

### Creates
```sql
CREATE DATABASE databasename;
```


### Deletes
```sql
DROP DATABASE databasename;
```

### Backup:
```sql
BACKUP DATABASE databasename TO DISK = 'filepath';

BACKUP DATABASE databasename TO DISK = 'filepath' WITH DIFFERENTIAL; -- backup only the delta since the last full backup
```

<hr>

## CRUD for Tables

### Creates
`CREATE TABLE ... (col1 type1 constraint, col2 type2 constraint, ...);`

- constraints are optional
- multiple constraints are space-separated

#### List of standard Constraints:
- `NOT NULL`: Prevent nulls
- `UNIQUE`
- `PRIMARY KEY`: Combination of NOT NULL and UNIQUE.
- `FOREIGN KEY`:
- `CHECK`: Custom condition for values, e.g. CHECK (field_name >= value)
- `DEFAULT`: Default value if none specified
- `CREATE_INDEX`
- `CONSTRAINT ... UNIQUE (col1, col2, ...)`:  Create a uniqueness on multiple columns


```sql
-- SQL Server, Oracle
CREATE TABLE Items (
    ItemID int IDENTITY(1,1) PRIMARY KEY, -- Start at 1, increment by 1
    NumberField int,
    TextField varchar(255),
    OtherItemID int FOREIGN KEY REFERENCES OtherItems(OtherItemID)
);

-- MySQL
CREATE TABLE Items (
    ItemID int NOT NULL AUTO_INCREMENT,
    NumberField int,
    TextField varchar(255),
    OtherItemID int,
    PRIMARY KEY (ItemID),
    FOREIGN KEY (OtherItemID) REFERENCES OtherItems(OtherItemID)
);

-- Also can use data from other tables
CREATE TABLE DerivedTable AS
    SELECT ... FROM ...

-- Views are virtual tables based on real tables
CREATE OR REPLACE VIEW [Virtual Table Name] AS -- "OR REPLACE" is optional
    SELECT ... FROM ...
```

#### Date Types
- `DATE`: YYYY-MM-DD
- `DATETIME`: YYYY-MM-DD HH:MI:SS
- `TIMESTAMP`: MySQL: YYYY-MM-DD HH:MI:SS, SQL Server: a unique number
- `YEAR`: MySQL: YYYY or YY
- `SMALDATETIME`: SQL Server: Similar to DATETIME


### Updates
```sql
-- Column add
ALTER TABLE table_name ADD column_name datatype;

-- Column delete
ALTER TABLE table_name DROP COLUMN column_name;

-- Column modify: to change data type or constraint (newconstraint is optional)
ALTER TABLE table_name ALTER COLUMN column_name newdatatype newconstraint; -- SQL Server
ALTER TABLE table_name MODIFY COLUMN column_name newdatatype newconstraint; -- My SQL, older Oracle
ALTER TABLE table_name MODIFY column_name newdatatype newconstraint; -- Oracle 10G+

-- Index CRUD
ALTER TABLE table_name CREATE INDEX;
ALTER TABLE table_name DROP INDEX;

-- Constraints
ALTER TABLE table_name ADD UNIQUE (col); -- Single Column
ALTER TABLE table_name ADD CONSTRAINT constraint_name UNIQUE(col1, col2, ...); -- Multiple Columns

ALTER TABLE table_name ADD FOREIGN KEY (other_table_id) REFERENCES other_table_name(other_table_id);
ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY (other_table_id) REFERENCES other_table_name(other_table_id); -- Multiple Columns

ALTER TABLE table_name DROP CONSTRAINT constraint_name; -- SQL Server, Oracle (also used to drop foreign keys)
ALTER TABLE table_name DROP PRIMARY KEY; -- MySQL
ALTER TABLE table_name DROP FOREIGN KEY foreign_key_name; --MySQL

-- Increment
ALTER TABLE table_name AUTO_INCREMENT=100; -- MySQL
```

<hr>

### Deletes
```sql
DROP TABLE table_name; -- delete the data and schema

TRUNCATE TABLE table_name; -- delete the data but keep the schema

DROP VIEW view_name; 
```

<hr>

## CRUD for Rows

### Reads
`SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... ASC|DESC`

`WHERE` specified a list of boolean conditions.

- Arithmetic operators: `+`, `-`, `*`, `/`, `%`
- Bitwise operators: `&`, `|`, `^` (XOR)
- Comparison operators: `=`, `>`, `<`, `>=`, `<=`, `<>` or `!=`
- Logical operators: `AND`, `OR`, `NOT`, `LIKE`, `IN`, `BETWEEN`, `ALL`, `ANY`, `SOME`
- Other operators: `IS`

Negation operator `NOT`: 
- For comparison operators, `NOT` comes before the condition it negates.
- For set operators, `NOT` comes before the operator name. e.g. `NOT LIKE`, `NOT IN`, `NOT BETWEEN`
- For nullness, `NOT` comes before `NULL`. e.g. `IS NOT NULL`

Notes:
- `IN` operator is followed with a list of **CSV** or another `SELECT` statement, inside **parantheses**.
- `BETWEEN` uses `AND` to specify the range between left and right value. Limit values are inclusive.
- `AS` operator allows aliasing a column (in `SELECT`) or a table (in `FROM`).
- Separate multiple tables in `FROM` using commas. This is referred to an implicit inner join. Reported deprecated.


Wildcards for `LIKE` operator (for SQL Server):

| symbol | matches                       | example   |
| ------ | ----------------------------- | --------- |
| %      | 0-n characters                | endsWith% |
| _      | 1 character                   | sp_ce     |
| []     | Any 1 character from the list | h[oa]t    |
| [^]    | Any character not in the list | h[^oa]t   |
| [-]    | Character range               | c[a-b]t   |


#### Examples:
```sql
--Get all data
SELECT * FROM table_name;

--Get specified columns of all rows
SELECT col1, col2 FROM table_name; 

--Get distinct(unique) values of col1
SELECT DISTINCT col1 FROM table_name;

--Get id column of rows whose is_flag=1. Don't quote numerical values.
SELECT id FROM table_name WHERE is_flag = 1;

--Get number of rows in table
SELECT count(*) FROM table_name; 

--Get count of each company
SELECT company, count(*) FROM table_name GROUP BY company; 

-- Get count of distinct values of col1. (Note: Won't work in FireFox/MS Access)
SELECT count(DISTINCT col1) FROM table_NAME;

-- Multiple conditions
SELECT * FROM Customers WHERE Country='Germany' AND (City='Berlin' OR City='München');

-- Get rows sorted by county first (in ascending order) and customer name second (in descending order)
SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;

-- Get from multiple tables
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Customers AS c, Orders AS o
WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;

-- Get countries and counts of countries having more than 5 customers in descending order of count
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

#### Limiting the number of rows returned:
```sql
SELECT TOP 10 * FROM table_name WHERE condition;                            -- SQL Server, MS Access
SELECT TOP 10 PERCENT * FROM table_name WHERE condition;                    -- SQL Server, MS Access
SELECT * FROM table_name WHERE condition LIMIT 10;                          -- MySQL
SELECT * FROM table_name WHERE cindition FETCH FIRST 10 ROWS ONLY;          -- Oracle 12
SELECT * FROM table_name WHERE cindition FETCH FIRST 10 PERCENT ROWS ONLY;  -- Oracle 12
SELECT * FROM table_name WHERE ROWNUM <= 10;                                -- Older Oracle
```

#### Function syntax
```sql
SELECT COUNT(column_name) FROM table_name WHERE condition;
SELECT MIN(column_name) FROM table_name WHERE condition;
SELECT MAX(column_name) FROM table_name WHERE condition;
SELECT AVG(column_name) FROM table_name WHERE condition;
SELECT SUM(column_name) FROM table_name WHERE condition;
```

Null functions:
- SQL Server: `ISNULL(column_name, value_if_null)`
- MySQL: `IFNULL(column_name, value_if_null)`
- Oracle: `NVL(column_name, value_if_null)`


#### Joins
- `INNER JOIN`: Records have matching values in both tables: $A \cap B$
- `LEFT JOIN` or `LEFT OUTER JOIN`: all records from the left table and the matching records from the right table: $A$
- `RIGHT JOIN` or `RIGHT OUTER JOIN`: all records from the right table, and the matching records from the left table: $B$
- `FULL JOIN` or `FULL OUTER JOIN`: all records from the right table, and the matching records from the left table: $A \cup B$
- For multiple joins use parantheses to group

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate 
FROM Orders INNER JOIN Customers  -- or use LEFT JOIN, etc..
ON Orders.CustomerID=Customers.CustomerID;

-- Self Join
SELECT column_name(s)
FROM table1 T1, table1 T2   -- notice same table being used
WHERE condition;
```

#### Union
- Column sequences must match exactly by number and type.
- Selects distinct values by default. Use `UNION ALL` instead otherwise.

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

#### Exists
- Used to test for the existence of any record in a subquery.
- The `EXISTS` operator returns TRUE if the subquery returns one or more records.

```sql
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

### Into
- Copy data from one table to another
- `SELECT INTO` can also be used to create a new, empty table using the schema of another. Just add a `WHERE` clause that returns FALSE.
```sql
SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

### Case

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```




### Creates
`INSERT INTO ... (..., ) VALUES (..., )`

Specifying column names are optional if providing values for all columns

```sql
INSERT INTO table_name (col1, col2, ...) VALUES (value1, value2, ...);

INSERT INTO table_name (co1, col2, ...) 
SELECT col1, col2, ... 
FROM  table_other
WHERE condition;
```

### Updates
`UPDATE ... SET ..., WHERE ...`

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;    -- specifying a condition is optional but required in practice
```

### Deletes
`DELETE FROM .... WHERE ...`

```sql
DELETE FROM table_name WHERE condition;
```

<hr>


## Stored Procedures

Create:

```sql
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```

Execute:
```sql
EXEC procedure_name;
```

