# SQL Order of Operations

> Let's learn about the execution order of SELECT queries.
>
> Reference: [SQL BOLT](https://sqlbolt.com/lesson/select_queries_order_of_execution)

<br>
<br>

### Syntax Order

1. `SELECT` column name
2. `FROM` table name
3. `WHERE` condition
4. `GROUP BY` column name
5. `HAVING` condition
6. `ORDER BY` column name

<br>
<br>

### Execution Order

1. **`FROM`**
2. `ON`
3. `JOIN`
4. **`WHERE`**
5. **`GROUP BY`**
6. **`HAVING`**
7. **`SELECT`**
8. `DISTINCT`
9. **`ORDER BY`**

<br>
<br>

### Detailed Look at Execution Order

#### 1. `FROM` and `JOIN`s

- `JOIN` is executed first to collect the data set
- This operation includes **subqueries**, creating a temporary table that contains all JOINed rows and columns

#### 2. `WHERE`

- Once the data set is formed, the conditions in `WHERE` are applied to each row
- The constraints in the `WHERE` clause are applied to the tables requested in the `FROM` clause

#### 3. `GROUP BY`

- After the `WHERE` clause is applied, the remaining rows are grouped based on common values in the columns specified in the `GROUP BY` clause
- When using a `GROUP BY` clause, you can use aggregate functions on those columns
  
#### 4. `HAVING`

- If there is a `GROUP BY` clause in the query, the constraints in the `HAVING` clause are applied to the grouped rows
- Changing the conditions in the `HAVING` clause does not change the result data, only the number of output records

#### 5. `SELECT`

- The `SELECT` clause is executed last

#### 6. `DISTINCT`

- Among the remaining rows, rows with duplicate column values are deleted

#### 7.`ORDER BY`

- The stored values are sorted in ascending or descending order
- Since the `SELECT` clause of the query has already been executed, **aliases** can be referenced in the `ORDER_BY` clause 
