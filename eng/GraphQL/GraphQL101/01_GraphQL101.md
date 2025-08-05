# Intro to GraphQL

> Getting started with GraphQL!
>
> <https://tech.kakao.com/2019/08/01/graphql-basic/>
>
> <https://www.slideshare.net/shilpe34/typescript-200-graphql-179690400>

<br>

<br>

## What is GraphQL?

> Query Language for APIs!

- Query Language like SQL (Structured Query Language)
  - but, there's a big difference in linguistic structure
    - As a result, the utilization of these two is different
    - **Purpose of use**
      - `sql` : Purpose is to efficiently retrieve data stored in **DB**
      - `gql` : Purpose is for **Web Client** to efficiently retrieve data **from server**
    - **Calling**
      - `sql` : Written and called in **Backend** system
      - `gql` : Written and called in **Client** system
- Can load a lot of data with a single request
- Type system
- Provides powerful developer tools

<br>

<br>

### Serverside GraphQL application

- Takes queries written in `gql` as input, processes the queries and returns the results back to **client**
- GraphQL server

<br>

<br>

### Differences between REST API and GraphQL API

- #### REST API

  - Various Endpoints exist because they combine `URL`, `METHOD`, etc.
    - Database SQL query differs for each Endpoint

- #### gql API

  - Only one Endpoint exists
  - The type of data to load is determined through query combinations
    - Database SQL query differs for each **gql schema type**

<br>

*The advantages and disadvantages of each change depending on the configured infrastructure, business model, and purpose of use!*

<br>

<br>

### schema / type

<br>

ex)

```
type Character {
    name: String!
    appearIn: [Episode!]!
}
```

- `Object type` : Character
- `Field` : name, appearIn
- `Scala type` : String, Id, Int etc.
- `!` : Required value (non-nullable)
- `[ ,]` : Array

<br><br>

### Resolver

- gql query parsing is handled by most gql libraries
  - but, the specific process of retrieving data is handled by `resolver` and must be implemented directly!
- If the field is a `scalar value` (**primitive** type like string or number), execution terminates
  - That is, no more chained resolver calls occur

<br>

<br> 
