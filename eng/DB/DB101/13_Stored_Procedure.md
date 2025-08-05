# Stored Procedure

<br>

## What is a Stored Procedure?

- A `collection of queries` to execute a series of queries like `a single function`
  - `Multiple queries` bundled into one function

<br>

## Advantages of Stored Procedures

- Reusability and minimizing duplicate code
  - You can reuse SQL statements that perform the same task without writing them repeatedly
  - You can use control statements like IF or While in SQL, reducing application source code
- Reduced network load
  - Since Stored Procedures are executed within the DB, they can reduce network traffic between client ↔ db server
  - Performance can be improved because complex queries or data processing are performed on the server rather than requested from the client
- Reduced `processing time` and improved performance
  - Performance is improved compared to executing individual SQL statements because a series of SQL statements can be executed at once
  - The DB server provides faster execution speed and performance by pre-compiling and optimizing stored procedures to generate execution plans
- Maintaining data `integrity`
  - Complex data validation logic can be processed within Stored Procedures to maintain integrity
  - Multiple operations can be bundled into a single transaction within Stored Procedures to ensure consistency between multiple tables, or roll back in case of failure to maintain data consistency

<br>

## Disadvantages of Stored Procedures

- Increased complexity
  - Since code is stored inside the DB, debugging, testing, and maintenance can be more difficult than managing it in the application
- Inconvenient maintenance
  - Because they are stored inside the DB, it is difficult to perform version control using SCM, track changes, or perform rollback operations
- Difficulty in DB scaling
  - The syntax and functionality of Stored Procedures can vary by DB vendor, making them dependent on specific vendors
    - This may require modifications when changing or migrating DBs
- Limitations in performance optimization
  - Since they run independently within the DB engine, they can be more difficult to optimize than code written at the application level
    - For complex query optimization, it may be necessary to understand the internal workings of the DB engine
- Difficulty in testing
  - Since testing is done inside the DB, it can be more complex and cumbersome than testing at the application level 
