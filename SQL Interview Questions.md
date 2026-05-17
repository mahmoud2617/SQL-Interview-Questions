## *1. What is SQL and why is it used?*
SQL (Structured Query Language) is used to manage and manipulate relational databases. It allows users to retrieve, insert, update, and delete data efficiently.

## *2. Difference between SQL and MySQL*  
- *SQL* is a *language* used to interact with databases.  
- *MySQL* is a *relational database management system (RDBMS)* that uses SQL.  

Think of SQL as the language, and MySQL as the software that understands and processes it.

## *3. What are primary keys and foreign keys?*  
- *Primary Key* uniquely identifies each row in a table. It must be unique and not null.  
- *Foreign Key* links one table to another. It references the primary key of another table to maintain referential integrity.

## *4. What is a unique constraint?*  
It ensures that all values in a column (or combination of columns) are *unique* across the table. Unlike primary keys, columns with a unique constraint can accept *one NULL*.

## *5. Difference between WHERE and HAVING*  
- *WHERE* filters rows *before* aggregation.  
- *HAVING* filters groups *after* aggregation.  
Example: Use `WHERE` for filtering raw data, `HAVING` for filtering `GROUP BY` results.

## *6. What are joins? Types of joins?*
Joins combine data from multiple tables based on related columns.  
Types:  
- *INNER JOIN* – Returns matching rows  
- *LEFT JOIN* – All rows from left table + matched rows from right  
- *RIGHT JOIN* – All rows from right table + matched from left  
- *FULL JOIN* – All rows from both tables  
- *CROSS JOIN* – Cartesian product

## *7. Difference between INNER JOIN and LEFT JOIN*  
- *INNER JOIN* only returns rows with matching keys in both tables.  
- *LEFT JOIN* returns *all* rows from the left table, plus matching rows from the right table (NULLs if no match).

## *8. What is a subquery?*  
A subquery is a query nested inside another SQL query. It can be used in SELECT, FROM, or WHERE clauses to fetch intermediate results.

## *9. What are CTEs (Common Table Expressions)?*  
CTEs are temporary named result sets that make queries more readable and reusable.  
Syntax:  
```sql  
WITH cte_name AS (  
   SELECT ...  
)  
SELECT * FROM cte_name;  
```

## *10. What is a view in SQL?*  
A *view* is a virtual table based on a SQL query. It doesn't store data itself but provides a way to simplify complex queries, improve security, and reuse logic.

## *11. How do you remove duplicate records?*  
Use `DISTINCT` or `ROW_NUMBER()` with a CTE to delete duplicates.  
```sql
SELECT DISTINCT * FROM table_name;
```
Or:  
```sql
WITH Ranked AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY col1, col2 ORDER BY id) AS rn
  FROM table_name
)
DELETE FROM Ranked WHERE rn > 1;
```

## *12. What is normalization? Explain its types.*  
Normalization reduces redundancy and improves data integrity.  
- 1NF: Atomic columns (no repeating groups)  
- 2NF: 1NF + no partial dependency  
- 3NF: 2NF + no transitive dependency  
- BCNF: Advanced version of 3NF

## *13. What is denormalization?*  
The process of combining tables to improve read speed by introducing redundancy. Used for reporting and faster queries.

## *14. What is a stored procedure?*  
A saved set of SQL statements that can be reused.  
```sql
CREATE PROCEDURE GetUsers AS  
BEGIN  
  SELECT * FROM users;  
END;
```

## *15. What are indexes and why are they used?*  
Indexes speed up query performance by allowing quick data lookup. Useful on columns used in WHERE or JOIN.

## *16. What is the difference between clustered and non-clustered index?*  
- Clustered: Sorts actual table data. Only one per table.
- Non-clustered: Separate structure that references data. Can have many.

## *17. What is a transaction?*  
A group of operations treated as a single unit. It follows ACID principles to maintain data integrity.

## *18. ACID properties in SQL*  
- Atomicity: All or none of the operations run  
- Consistency: Data stays valid before/after transaction  
- Isolation: Transactions don’t interfere  
- Durability: Changes remain after success

## *19. Difference between DELETE, TRUNCATE, and DROP*  
- DELETE: Removes rows, can be rolled back  
- TRUNCATE: Removes all rows, faster, less logging  
- DROP: Deletes table structure and data

## *20. What is a NULL value in SQL?*  
NULL represents missing or unknown data. It's different from 0 or an empty string.

## *21. How do you handle NULLs in queries?*  
Use `IS NULL`, `IS NOT NULL`, `COALESCE()`, or `IFNULL()` to manage NULLs.  
Example:  
```sql
SELECT name FROM users WHERE email IS NULL;
```

## *22. What is COALESCE() in SQL?*  
It returns the first non-NULL value from a list.  
```sql
SELECT COALESCE(phone, 'Not Provided') FROM customers;
```

## *23. What are aggregate functions?*  
Functions that perform calculations on multiple rows:  
- `COUNT()`  
- `SUM()`  
- `AVG()`  
- `MAX()`  
- `MIN()`

## *24. What is GROUP BY and how does it work?*  
It groups rows that have the same values and is used with aggregate functions.  
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

## *25. What is the difference between COUNT(*) and COUNT(column)?*  
- `COUNT(*)`: Counts all rows, including those with NULLs  
- `COUNT(column)`: Counts non-NULL values in that column

## *26. What are window functions?*  
They perform calculations across rows related to the current row without collapsing results.  
Examples: `ROW_NUMBER()`, `RANK()`, `SUM() OVER()`

## *27. Difference between RANK(), DENSE_RANK(), and ROW_NUMBER()*  
- `RANK()`: Skips ranks on ties  
- `DENSE_RANK()`: No gaps in ranking
- `ROW_NUMBER()`: Unique sequence for each row

## *28. What is the use of LAG() and LEAD()?*  
They access previous (`LAG`) or next (`LEAD`) row values in the result set.  
```sql
SELECT name, salary, LAG(salary) OVER (ORDER BY id) AS prev_salary FROM employees;
```

## *29. What is a CASE statement?*  
It's used for conditional logic in queries.  
```sql
SELECT name,  
CASE  
  WHEN salary > 5000 THEN 'High'  
  ELSE 'Low'  
END AS salary_level  
FROM employees;
```

## *30. What is the difference between CHAR and VARCHAR?*  
- `CHAR(n)`: Fixed-length, always reserves `n` characters  
- `VARCHAR(n)`: Variable-length, uses space based on actual content

## *31. What are constraints in SQL?*  
Constraints are rules applied to columns to enforce data integrity:  
- `PRIMARY KEY` – Uniquely identifies each record  
- `FOREIGN KEY` – Ensures referential integrity  
- `UNIQUE` – Ensures all values are different  
- `NOT NULL` – Prevents null values  
- `CHECK` – Restricts values based on condition  
- `DEFAULT` – Assigns a default value

## *32. What is a composite key?*  
A composite key is a combination of two or more columns that together uniquely identify a row.  
Example: (StudentID, CourseID) in an enrollment table.

## *33. What are scalar vs table-valued functions?*  
- *Scalar function:* Returns a single value (e.g., `LEN()`, `GETDATE()`)  
- *Table-valued function:* Returns a table/data set and can be used in FROM clause

## *34. How does indexing affect performance?*  
Indexes improve read performance (SELECT) by allowing faster searches.  
Downsides:  
- Slower write operations (INSERT, UPDATE, DELETE)  
- Takes additional storage  

## *35. What is data integrity?*  
Ensures the accuracy, consistency, and reliability of data throughout its lifecycle.  
Maintained using constraints, transactions, and normalization.

## *36. What are triggers in SQL?*
Triggers are automatic actions executed in response to certain events on a table (e.g., INSERT, UPDATE, DELETE).  
Used for auditing, enforcing rules, or updating related tables.

## *37. What is a correlated subquery?*  
A subquery that depends on the outer query for its values. It’s evaluated once for each row of the outer query.  
Example:  
```sql
SELECT name FROM employees e  
WHERE salary > (SELECT AVG(salary) FROM employees WHERE dept_id = e.dept_id);
```

## *38. What is a cross join?*  
Combines each row from one table with every row from another — produces Cartesian product.  
Used rarely, typically when all combinations are needed.

## *39. What is UNION vs UNION ALL?*  
- `UNION`: Combines two queries, removes duplicates  
- `UNION ALL`: Combines all rows, keeps duplicates  
Both require same number and type of columns.

## *40. Difference between EXISTS and IN*  
- `IN`: Checks if a value exists in a list  
- `EXISTS`: Checks if subquery returns any rows  
`EXISTS` is often faster with large subqueries or joins.

## *41. What are set operations in SQL?*  
Set operations combine results from multiple `SELECT` queries:  
- `UNION`: Combines and removes duplicates  
- `UNION ALL`: Combines all, including duplicates  
- `INTERSECT`: Returns common records  
- `EXCEPT` / `MINUS`: Returns records from first query not in second  

## *42. What is a materialized view?*  
Unlike a normal view (which is virtual), a *materialized view* stores actual data physically.  
It improves performance for complex queries and can be refreshed manually or automatically.

## *43. Explain the BETWEEN operator*  
Used to filter data within a range (inclusive).  
```sql
SELECT * FROM products WHERE price BETWEEN 100 AND 500;
```

## *44. What is a pivot table in SQL?*  
A pivot table transforms rows into columns, helpful for summaries.  
Used with `GROUP BY`, `CASE`, or database-specific `PIVOT` keyword.  
Example: Monthly sales pivoted by region.

## *45. How do you optimize SQL queries?*  
- Use indexes properly  
- Avoid `SELECT *`  
- Use `WHERE` clauses to filter data early  
- Use `EXISTS` over `IN` in subqueries  
- Analyze execution plans  
- Avoid unnecessary joins or nested subqueries  

## *46. How do you handle slow queries?*  
- Check indexes on filter columns
- Break large queries into smaller parts  
- Use caching  
- Limit returned rows with `LIMIT` or `TOP`  
- Use `EXPLAIN`/`QUERY PLAN` to analyze performance  

## *47. What is execution plan in SQL?*  
It shows how the database engine executes a query.  
Helps identify slow operations (like full table scans) and suggests improvements.  
Use `EXPLAIN` in MySQL/PostgreSQL or `SET SHOWPLAN_ALL` in SQL Server.

## *48. What’s the use of LIMIT / OFFSET?*  
- `LIMIT`: Restricts number of rows returned  
- `OFFSET`: Skips rows before starting to return  
```sql
SELECT * FROM users LIMIT 10 OFFSET 20;
```  
Useful for pagination.

## *49. How do you import/export data in SQL?*  
- Import: `LOAD DATA INFILE`, `BULK INSERT`, or import tools  
- Export: `SELECT INTO OUTFILE`, `mysqldump`, `pg_dump`, or CSV export from GUI tools  

## *50. How would you clean messy data using SQL?*  
- Use `TRIM()` to remove spaces  
- Use `REPLACE()` for unwanted characters  
- Handle NULLs with `COALESCE()`  
- Use `CASE` for conditional transformations  
- Use subqueries or CTEs to identify duplicates or invalid entries  