# Database

<br>

## Database

> A database is a collection of data that is systematically organized, integrated, and managed for the purpose of sharing and use by multiple people.

<br>

### DBMS (Database Management System)

- RDBMS
  - Database management system based on relational model

<br>

### Relational Database (RDBMS)

- Consists of a collection of tables organized as relationships with columns and rows
- Each column records a specific type of data
- Table rows are collections of values related to each object/entity

<br>

### RDBMS vs NOSQL

![Difference between SQL and NOSQL ](https://www.agiratech.com/wp-content/uploads/2018/01/Difference-between-SQL-and-NOSQL-2.png)

<br>

<br>

### Basic Terms

<br>

#### Schema

- An overall specification regarding the structure and constraints (structure, representation method, relationships, etc.) of data in a database

<br>

#### Table (Relation)

- A collection of data elements organized using a model of columns and rows

<br>

#### PK

- A unique value for each row that can uniquely identify stored records

<br>

<br>

## SQL (Structured Query Language)

> A language specifically designed to manage data in RDBMS

<br>

![DBMS SQL command](https://static.javatpoint.com/dbms/images/dbms-sql-command.png)

<br>

### Creating Tables

```sql
CREATE TABLE table (
 column1 datatype [constraints],
 column2 datatype [constaraints],
);
```

ex)

```sqlite
CREATE TABLE contacts (
 contact_id INTEGER PRIMARY KEY,
 first_name TEXT NOT NULL,
 last_name TEXT NOT NULL,
 email TEXT NOT NULL UNIQUE,
 phone TEXT NOT NULL UNIQUE
);
```

<br>

<br>

### Rename Table

```sqlite
ALTER TABLE table_name
 RENAME TO new_table_name;
```

<br>

<br>

### Data Types (in `SQLite`)

![All About Data Types In sqlite](https://www.guru99.com/images/SQLite/SQLlite_datatype.jpg)

<br>

<br>

### SELECT

- `DISTINCT`

  - Retrieve without duplicates

    ```sqlite
    sqlite> SELECT DISTINCT waypoint FROM flights;
    
    waypoint  
    ----------
    Beijing   
    Moscow    
    Beijing  
    ```

- `COUNT()`

  - Retrieve specific count

- `LIKE`

  - Wild cards
    - `%` : There may or may not be a string
    - `_` : There must be exactly one character

- `LIMIT ... OFFSET`

  - Limit count .... up to what number

  - ex)
  
    ```sql
    -- Returns the first 10 rows
    SELECT * FROM test LIMIT 10;
    -- The above SQL and the below SQL have the same result
    SELECT * FROM test LIMIT 10 OFFSET 0;
     
    -- Returns 10 rows starting from the 11th.
    SELECT * FROM test LIMIT 10 OFFSET 10;
    ```

<br>

```sql
.schema ____
```

<br>

<br>

### CREATE

```sql
sqlite> CREATE TABLE flights(
   ...> id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...> flight_num TEXT NOT NULL,
   ...> departure TEXT NOT NULL,
   ...> waypoint TEXT NOT NULL,
   ...> arrival TEXT NOT NULL,
   ...> price INTEGER NOT NULL
   ...> );
```

<br>

#### IF NOT EXISTS

- Create only when the table does not exist

```sqlite
sqlite> CREATE TABLE IF NOT EXISTS flights(
   ...> id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...> flight_num TEXT NOT NULL,
   ...> departure TEXT NOT NULL,
   ...> waypoint TEXT NOT NULL,
   ...> arrival TEXT NOT NULL,
   ...> price INTEGER NOT NULL
   ...> );
```

<br>

#### View Tables

```sqlite
sqlite> .tables
```

<br>

<br>

### INSERT

```sql
lite> INSERT INTO flights(flight_num, departure, waypoint, arrival, price) VALUES('RT9122', 'Madrid', 'Beijing', 'Incheon', 200);

id          flight_num  departure   waypoint    arrival     price     
----------  ----------  ----------  ----------  ----------  ----------
1           RT9122      Madrid      Beijing     Incheon     200    
```

<br>

<br>

### UPDATE

```sqlite
sqlite> UPDATE flights SET waypoint = 'Tokyo' WHERE flight_num = 'SQ0972';
```

<br>

<br>

### DELETE

```sqlite
sqlite> DROP TABLE flights;

sqlite> .tables
sqlite> select*from flights;
Error: no such table: flights
```

<br>

<br>

### Select exercise

#### 1. Retrieve all data from the flights table

```sqlite
sqlite> SELECT * FROM flights;

id          flight_num  departure   waypoint    arrival     price     
----------  ----------  ----------  ----------  ----------  ----------
1           RT9122      Madrid      Beijing     Incheon     200       
2           XZ0352      LA          Moscow      Incheon     800       
3           SQ0972      London      Beijing     Sydney      500 
```

<br>

#### 2. Retrieve all waypoints

```sqlite
sqlite> SELECT waypoint FROM flights;

waypoint  
----------
Beijing   
Moscow    
Beijing   
```

<br>

#### 3. Retrieve id and flight_num of flights with airfare less than 600

```sqlite
sqlite> SELECT id, flight_num from flights WHERE price<600;

id          flight_num
----------  ----------
1           RT9122    
3           SQ0972   
```

<br>

#### 4. Retrieve departure of flights with destination Incheon and price 500 or above

```sqlite
sqlite> SELECT departure FROM flights WHERE arrival = 'Incheon' AND 500 <= price;

departure 
----------
LA    
```

<br>

#### 5. Retrieve id and flight_num of flights where the numeric part starts with 0 and ends with 2, and the waypoint is Beijing

> ver 1

```sqlite
sqlite> SELECT id, flight_num FROM flights where waypoint = 'Beijing' AND flight_num LIKE '__0__2';

id          flight_num
----------  ----------
3           SQ0972 
```

<br>

> ver 2

```sqlite
sqlite> SELECT id, flight_num FROM flights where waypoint = 'Beijing' AND flight_num LIKE '__0%2';

id          flight_num
----------  ----------
3           SQ0972 
```

<br>

> ver 3

```sql
sqlite> SELECT id, flight_num FROM flights where waypoint = 'Beijing' AND flight_num LIKE '%0%2';

id          flight_num
----------  ----------
3           SQ0972    
```

<br>

### .read

```sqlite
sqlite> .read hello_user.sql
1,"정호","유",40,"전라북도",016-7280-2855,370
2,"경희","이",36,"경상남도",011-9854-5133,5900
3,"정자","구",37,"전라남도",011-4177-8170,3100
4,"미경","장",40,"충청남도",011-9079-4419,250000
5,"영환","차",30,"충청북도",011-2921-4284,220
6,"서준","이",26,"충청북도",02-8601-7361,530
7,"주원","민",18,"경기도",011-2525-1976,390
8,"예진","김",33,"충청북도",010-5123-9107,3700
9,"서현","김",23,"제주특별자치도",016-6839-1106,43000
10,"서윤","오",22,"충청남도",011-9693-6452,49000
```

<br>

<br>

`+`

### Pretty Display in CLI

```sqlite
sqlite> .headers on
sqlite> .mode column
```

<br> 
