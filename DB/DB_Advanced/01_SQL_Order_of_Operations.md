# SQL Order of Operations

> SELECT 쿼리 실행 순서에 대해 알아보아요.
>
> Reference: [SQL BOLT](https://sqlbolt.com/lesson/select_queries_order_of_execution)

<br>
<br>

### 문법 순서

1. `SELECT` column 명
2. `FROM` table 명
3. `WHERE` 조건식
4. `GROUP BY` column 명
5. `HAVING` 조건식
6. `ORDER BY` column 명

<br>
<br>

### 실행 순서

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

### 실행 순서 자세히 알아보기

#### 1. `FROM` and `JOIN`s

- `JOIN`이 먼저 실행되어 data set이 모아진다
- 이 작업에는 **subquery**들도 포함되어, JOIN 된 모든 row와 column이 포함된 임시 table을 생성한다

#### 2. `WHERE`

- Data set을 형성하면, `WHERE`의 조건이 각 행에 적용된다
- `WHERE` 절의 제약 조건은 `FROM`절로 요청된 table에 적용된다

#### 3. `GROUP BY`

- `WHERE` 절이 적용된 후 남아있는 row들은 `GROUP BY`절에 지정된 column의 공통된 값을 기준으로 그룹화된다
- `GROUP BY` 절을 사용하면 해당 column으로 aggregate function (집계 함수)를 사용할 수 있다
  
#### 4. `HAVING`

- `GROUP BY` 절이 query에 있는 경우, `HAVING` 절의 제약 조건이 group화 된 row에 적용된다
- `HAVING` 절의 조건 변경은 결과 data의 변경은 없고, 출력되는 record 개수만 변경될 수 있다

#### 5. `SELECT`

- `SELECT` 절이 마지막으로 실행된다

#### 6. `DISTINCT`

- 남아있는 row 중에서, column 값이 중복된 row들은 삭제된다

#### 7.`ORDER BY`

- 저장된 값을 오름차순 혹은 내림차순으로 정렬한다
- Query의 `SELECT` 절이 이미 실행되었기 때문에, `ORDER_BY` 절에서는 **alias**를 참조할 수 있다
  