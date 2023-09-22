# Database

<br>

## Database

> Database는 여러 사람이 공유하여 사용할 목적으로 체계화해 통합, 관리하는 데이터의 집합이다.

<br>

### DBMS (Database Management System)

- RDBMS
  - 관계형 모델 기반 databse 관리 시스템

<br>

### 관계형 데이터베이스 (RDBMS)

- 관계를 열과 행으로 이루어진 테이블 집합으로 구성
- 각 열에 특정 종류의 데이터를 기록
- 테이블의 행은 각 객체/entity와 관련된 값의 모음

<br>

### RDBMS vs NOSQL

![Difference between SQL and NOSQL ](https://www.agiratech.com/wp-content/uploads/2018/01/Difference-between-SQL-and-NOSQL-2.png)

<br>

<br>

### 기본 용어

<br>

#### Schema

- Database에서 자료의 구조와 제약조건 (구조, 표현 방법, 관계 등)에 관한 전반적인 명세

<br>

#### Table (관계)

- 열과 행의 모델을 사용해 조작된 데이터 요소들의 집합

<br>

#### PK

- 각행의 고유값으로 저장된 레코드를 고유하게 식별할 수 있는 값

<br>

<br>

## SQL (Structured Query Language)

> RDBMS의 data를 관리하기 위해 특수하게 설계된 언어

<br>

![DBMS SQL command](https://static.javatpoint.com/dbms/images/dbms-sql-command.png)

<br>

### Table 생성

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

  - 중복없이 가져오기

    ```sqlite
    sqlite> SELECT DISTINCT waypoint FROM flights;
    
    waypoint  
    ----------
    Beijing   
    Moscow    
    Beijing  
    ```

- `COUNT()`

  - 특정 개수 가져오기

- `LIKE`

  - 와일드 카드
    - `%` : 문자열이 있을 수도 있다
    - `_` : 반드시 한 개의 문자가 있다

- `LIMIT ... OFFSET`

  - 개수 제한 .... 몇 번째까지

  - ex)
  
    ```sql
    -- 처음 10개의 Row를 반환
    SELECT * FROM test LIMIT 10;
    -- 위 SQL과 아래의 SQL은 같은 결과
    SELECT * FROM test LIMIT 10 OFFSET 0;
     
    -- 11번째 부터 10개의 Row를 반환.
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

- 해당 table이 존재하지 않을 때에만 생성하기

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

#### Table 조회

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

#### 1. flights 테이블 전체 데이터를 조회하시오

```sqlite
sqlite> SELECT * FROM flights;

id          flight_num  departure   waypoint    arrival     price     
----------  ----------  ----------  ----------  ----------  ----------
1           RT9122      Madrid      Beijing     Incheon     200       
2           XZ0352      LA          Moscow      Incheon     800       
3           SQ0972      London      Beijing     Sydney      500 
```

<br>

#### 2. 모든 waypoint를 조회하시오

```sqlite
sqlite> SELECT waypoint FROM flights;

waypoint  
----------
Beijing   
Moscow    
Beijing   
```

<br>

#### 3. 항공권 가격이 600 미만인 항공편들의 id와 flight_num을 조회하시오

```sqlite
sqlite> SELECT id, flight_num from flights WHERE price<600;

id          flight_num
----------  ----------
1           RT9122    
3           SQ0972   
```

<br>

#### 4. 도착지가 Incheon이고 가격이 500 이상인 항공편의 departure를 조회하시오

```sqlite
sqlite> SELECT departure FROM flights WHERE arrival = 'Incheon' AND 500 <= price;

departure 
----------
LA    
```

<br>

#### 5. 항공편의 숫자부분이 0으로 시작하고 2로 끝나면서 경유지가 Beijing인 항공편들의 id와 flight_num을 조회하시오

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

> ver 2

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

### CLI에서 예쁘게 보기

```sqlite
sqlite> .headers on
sqlite> .mode column
```

<br>
