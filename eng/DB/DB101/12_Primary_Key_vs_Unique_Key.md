# Primary key vs Unique key

<br>

### Primary key

- The only key in a table
- Used to uniquely identify each record in the table
  - For this role, it has `Unique` & `Not Null` properties
- Can consist of one row or multiple rows within a table
- When composed of multiple rows, it's called a `Composite Primary Key`
- Primary Key automatically creates an `Index`, which helps to quickly search and manage records

<br>

### Unique key

- Plays the role of not allowing duplicates (`Unique`)
  - Can identify each record
- Allows Null
  - This means there can be multiple Null values as long as the row is not duplicated
- Multiple Unique Keys can be defined within one table
- If a Primary Key is defined, that row automatically becomes a Unique Key
  - but, the reverse is not true
    - Unique Key cannot replace the role of Primary Key! 
