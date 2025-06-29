# How to Avoid N+1 Queries

> JPA를 사용하면 자주 만나게 되는 N+1 Query에 대해 알아보아요
>
> References: [jojoldu.tistory.com](https://jojoldu.tistory.com/165)

<br>

<br>

## What are N+1 queries?

하위 엔티티들을 **첫 쿼리 실행시 한 번에 가져오지 않고**, Lazy Loading으로 필요한 곳에서 사용되어 쿼리가 실행될 때 발생하는 문제

<br>

<br>

## How to Avoid N+1 Queries?

### 1. Join Fetch

조회 시 바로 가져오고 싶은 Entity Field를 지정 하는 것

ex)

 ```sql
 SELECT a FROM School a JOIN FETCH a.subjects
 ```

<br>

하위 Entity까지 한 번에 가져와야 할 때도 사용할 수 있다.

ex)

```sql
SELECT a from School a JOIN FETCH a.subjets s JOIN FETCH s.teacher
```

but, 이 방법은 **불필요한 쿼리문이 추가**되는 단점이 있다

`이 field는 Eager 조회, 저 field는 Lazy 조회 를 해야한다` 까지 **query에서 표현**하는 것은 불필요하다고 느낄 수 있다.

그럴 때, 아래의 방법을 사용할 수 있다.

<br>

<br>

### 2. @EntityGraph

`@EntityGraph`의 `attributePath`에 query 수행 시 바로 가져올 field명을 지정하면, **Lazy**가 아닌 **Eager** 조회로 가져오게 된다

ex)

```java
@EntityGraph(attributePaths = "subjects")
@Query("SELECT a FROM School a")
```

위와 같이 `attributePath` 를 지정하면, 원본 쿼리 (SELECT a FROM School a)의 손상 없이 **Eager/Lazy** field를 정의하고 사용할 수 있다.

<br>

추가로 Tearcher까지 한 번에 가져오는 query도 아래와 같이 표현할 수 있다

```java
@EntityGraph(attributePaths = {"subjects", "subjects.teacher"})
@Query("SELECT a FROM School a")
```

<br>

<br>

## 주의할 점

`JoinFetch`는 **Inner Join**, `Entity Graph`는 **Outer Join** 라는 차이점이 있음을 유의하자.
공통적으로 **카테시안 곱(Cartesian Product)** 이 발생하여, `Subject` 수 만큼 `School`이 **중복 발생**하게 된다

<br>
<br>

## 해결 방안

### Solution 1
>
> 1:N field의 type을 `Set`으로 선언하기
`Set`은 중복을 허용하지 않는 자료 구조이기 때문에, 중복 등록이 되지 않는다

ex)

```java
    @OneToMany(cascade = CascadeType.ALL)
    @JoinColumn(name="school_id")
    private Set<Subject> subjects = new LinkedHashSet<>();

```

`Set`은 순서가 보장되지 않기 때문에, `LinkedHashSet`을 사용하여 순서를 보장한다

<br>

### Solution 2
>
> `distinct`를 사용하여 **중복을 제거**하기

이 부분은 `@Query`에서 적용하는 것이기 때문에, `join fetch`, `@EntityGraph`는 동일하다

ex)

```java
@Query("select DISTINCT a from School a join fetch a.subjects s join fetch s.teacher")
List<Academy> findAllWithTeacher();
```

```java
@EntityGraph(attributePaths = {"subjects", "subjects.teacher"})
@Query("select DISTINCT a from School a")
List<Academy> findAllEntityGraphWithTeacher();
```
