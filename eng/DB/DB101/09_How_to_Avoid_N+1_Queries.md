# How to Avoid N+1 Queries

> Let's learn about N+1 Queries that you often encounter when using JPA
>
> References: [jojoldu.tistory.com](https://jojoldu.tistory.com/165)

<br>

<br>

## What are N+1 queries?

A problem that occurs when sub-entities are **not fetched all at once during the first query execution**, but are executed via Lazy Loading when needed in the necessary places

<br>

<br>

## How to Avoid N+1 Queries?

### 1. Join Fetch

Specifying the Entity Field you want to fetch immediately during query

ex)

 ```sql
 SELECT a FROM School a JOIN FETCH a.subjects
 ```

<br>

This can also be used when you need to fetch sub-entities all at once.

ex)

```sql
SELECT a from School a JOIN FETCH a.subjets s JOIN FETCH s.teacher
```

but, this method has the disadvantage of **adding unnecessary query statements**

It may feel unnecessary to **express in the query** things like `this field should be Eager fetched, that field should be Lazy fetched`.

In such cases, you can use the method below.

<br>

<br>

### 2. @EntityGraph

If you specify the field name to be fetched immediately during query execution in the `attributePath` of `@EntityGraph`, it will be fetched as **Eager** rather than **Lazy**.

ex)

```java
@EntityGraph(attributePaths = "subjects")
@Query("SELECT a FROM School a")
```

By specifying `attributePath` as above, you can define and use **Eager/Lazy** fields without damaging the original query (SELECT a FROM School a).

<br>

Additionally, a query that fetches Teacher all at once can be expressed as follows:

```java
@EntityGraph(attributePaths = {"subjects", "subjects.teacher"})
@Query("SELECT a FROM School a")
```

<br>

<br>

## Points to Note

Note that `JoinFetch` uses **Inner Join**, while `Entity Graph` uses **Outer Join**.
Commonly, a **Cartesian Product** occurs, causing `School` to **duplicate** as many times as there are `Subject`s.

<br>
<br>

## Solutions

### Solution 1
>
> Declare the type of 1:N field as `Set`
Since `Set` is a data structure that does not allow duplicates, duplicate registration does not occur.

ex)

```java
    @OneToMany(cascade = CascadeType.ALL)
    @JoinColumn(name="school_id")
    private Set<Subject> subjects = new LinkedHashSet<>();

```

Since `Set` does not guarantee order, use `LinkedHashSet` to ensure order.

<br>

### Solution 2
>
> Use `distinct` to **remove duplicates**

Since this is applied in `@Query`, both `join fetch` and `@EntityGraph` are the same.

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
