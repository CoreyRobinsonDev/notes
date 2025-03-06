# PostgreSQL
- *PostgreSQL* is an open-source relational database management system (RDBMS)
- supports ACID (Atomicity, Consistency, Isolation, Durability) properties for reliable transaction processing
- uses multi-version concurrency control to give each transaction a snapshot of the database, allowing parallel processing without locking

[source](https://neon.tech/postgresql/tutorial)

## Querying Data
### SELECT
- use the `SELECT ... FROM` statement to retrieve data from a table
- PostgreSQL evaluates the `FROM` clause before the `SELECT` clause
- use a column alias to assign a temporary name to a column or an expression in a query
- in PostgreSQL the `FROM` clause is optional 
- the `SELECT` statement has the following cluases
    - use `DISTINCT` to select distinct rows
    - use `ORDER BY` to sort rows 
    - use `WHERE` to filter rows
    - use `LIMIT` or `FETCH` to select a subset of rows
    - use `GROUP BY` to group rows
    - use `HAVING` to filter groups
    - use join other tables with:
        - `INNER JOIN`
        - `LEFT JOIN`
        - `FULL OUTER JOIN`
        - `CROSS JOIN`
    - use `UNION`, `INTERSECT`, and `EXCEPT` to perform set operations

### ORDER BY
- column alias can be used in the `ORDER BY` clause 
- when sorting rows that contain `NULL`, you cna specify the order of with
    - `NULLS FIRST`
    - `NULLS LAST`
```sql
ORDER BY sort_expression [ASC | DESC] [NULLS FIRST | NULLS LAST]
```
- `ORDER BY` uses `ASC` option by default

### SELECT DISTINCT
- `SELECT DISTINCT` removes duplicate rows from a result set
- `DISTINCT` can be applied to one or more columns
```sql
SELECT
    DISTINCT column1, column2
FROM
    table_name;
```

## Filtering Data
### WHERE
- use a `WHERE` clause in the `SELECT` statement ot filter rows of a query based on one or more conditions

### Booleans
- in PostgreSQL a boolean value can be `true`, `false`, or `null`
- PostgreSQL uses `true`, `'t'`, `'true'`, `'y'`, `'yes'`, and `'1'` to represent `true`
- PostgreSQL uses `false`, `'f'`, `'false'`, `'n'`, `'no'`, and `'0'` to represent `false`

### LIMIT
- use `LIMIT` to constrain the number of rows returned by a query

```sql
SELECT
  select_list
FROM
  table_name
ORDER BY
  sort_expression
LIMIT
  row_count
OFFSET
  row_to_skip;
```
- use `OFFSET` to skip a number of rows before returning the *row_count*
- PostgreSQL evaluates the `OFFSET` clause before the `LIMIT` clause

### FETCH
- use `FETCH` to skip a certain number of rows and then fetch a specific number of rows
- the `FETCH` clause is functionally equivalent to `LIMIT`
- PostgreSQL supports this as a SQL standard
```sql
OFFSET row_to_skip { ROW | ROWS }
FETCH { FIRST | NEXT } [ row_count ] { ROW | ROWS } ONLY
```

### LIKE
- PostgreSQL offers two wildcardcs:
    - **%** matches any sequence of zero or more characters
    - **_** matches any singe character
- PostgreSQL `ILIKE` operator is similar to `LIKE` but allows for case-insensitive matching
- use `ESCAPE` to define an escape character to be used to exclude a wildcard charcter
```sql
SELECT * FROM t
WHERE message LIKE '%10$%%' ESCAPE '$';
```
- use the following operators to mirror the functionality of `LIKE`, `NOT LIKE`, `ILIKE`, and `NOT ILIKE`

| Operator | Equivalent |
|----------|------------|
| ~~ | LIKE |
| ~~* | ILIKE |
| !~~ | NOT LIKE |
| !~~* | NOT ILIKE |

## Join Tables
### Joins
![INNER JOIN](../../assets/PostgreSQL-Join-Inner-Join.avif)
- when equal the `INNER JOIN` creates a new row that contains columns from both tables and adds this new row to the result set

![LEFT JOIN](https://neon.tech/_next/image?url=%2Fpostgresqltutorial%2FPostgreSQL-Join-Left-Join.png&w=256&q=75&dpl=dpl_E7KLtH8jYxaZHJ8xeui4VnF9NBPK)
- when equal the `LEFT JOIN` creates a new row that contains columns from both tables and adds this new row to the result set
- when not equal the `LEFT JOIN` also creates a new row that contains columns from both tables but fills the right table with `NULL`
- `LEFT JOIN` is the same as `LEFT OUTER JOIN`

![RIGHT JOIN](https://neon.tech/_next/image?url=%2Fpostgresqltutorial%2FPostgreSQL-Join-Right-Join.png&w=256&q=75&dpl=dpl_E7KLtH8jYxaZHJ8xeui4VnF9NBPK)
- when equal the `RIGHT JOIN` creates a new row that contains columns from both tables and adds this new row to the result set
- when not equal the `RIGHT JOIN` also creates a new row that contains columns from both tables but fills the left table with `NULL`
- `RIGHT JOIN` is the same as `RIGHT OUTER JOIN`

![FULL OUTER JOIN](https://neon.tech/_next/image?url=%2Fpostgresqltutorial%2FPostgreSQL-Join-Full-Outer-Join.png&w=256&q=75&dpl=dpl_E7KLtH8jYxaZHJ8xeui4VnF9NBPK)
- `FULL JOIN` returns a result set that contains all rows from both left and right tables, with matching rows from both

### Self-Joins
- a PostgreSQL *self-join* is a regular join that joins a table to itself using the `INNER JOIN` or `LEFT JOIN`
- *self-joins* are very useful for querying hierarchical data or comparing rows within the same table

### CROSS JOIN
- use `CROSS JOIN` to combine each row from the first table with every row from the second table, resulting in a complete combination of all rows
```sql
SELECT
  select_list
FROM
  table1
CROSS JOIN table2;
```














