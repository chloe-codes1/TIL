# GraphQL Korea Meetup on 6/13/2020

<br>

<br>

## 1. Relay with Python

> Presenter: Jaehyun!!! ㅎ_ㅎ
>
> *"Unexpected efficiency from predictable consistency"*

<br>

### Graphene

- When defined in ORM way, it converts to GraphQL Schema
- Objectifies GraphQL and makes it well!

<br>

#### Relay

> Graphene supports `Relay`
>
> **Relay**
>
> : JavaScript framework for building GraphQL-based data-driven React applications

- Node
  - Interface provided by `graphene.relay`
  - Has only one `ID!` field
- Connection
  - Enhanced version of list that provides slicing and pagination
    - Each point distributed in the Graph is called **Node**, meaning one entity that constitutes the data structure,
    - The line connecting related **Nodes** is called **Edge**
      - In GraphQL, the address of each Node is called **Cursor**,
        - **Connection** is a `pagination` design pattern based on **Cursor**
  - ex)
    - `relay.Connection`
    - `relay.ConnectionField`
- Mutations
  - Mutations that perform data modification work can be easily managed in Graphene through subclass `relay.ClientIDMutation`

<br>

### Graphene-Django

> [Docs](https://docs.graphene-python.org/projects/django/en/latest/)

- Helps to easily apply GraphQL in Django

<br>

<br>

## 2. How to handle GraphQL as a language

> Presenter: Hyesung Kim
>
> *"Today, GraphQL is not only implementing APIs but also acting as a powerful "modeling language". I introduce how to handle GraphQL language with JavaScript and various cases of extending it."*

<br>

### Document

- Top-level node of GraphQL AST
- Contains various Definitions underneath

<br>

<br>

### Definition

- Executable Definition
  - Query / Mutation / Fragment etc.
- Other Definition
  - That part familiar to Client developers.. ㅎ

<br>

<br>

### SDL (Schema Definition Language)

> Powerful general-purpose modeling language

- Directed cyclic graph
- Type system-based validation
- Polymorphism support through Interface / Union
- Extensibility
- Macro

<br>

<br>

### Schema vs ExecutableSchema

<br>

- Adds `runtime` through several preprocessing tasks
  - Resolvers
  - Directives
    - Directives that can provide additional information to GraphQL Document processors
      - Standard (`@deprecated`, `@include`, `@skip`)
      - Schema Directive
        - ex) `@deprecated`
      - Operational Directive
        - ex) `@include`, `@skip`

<br>

<br><br>

`+`

#### Impressions

- I became more interested in GraphQL!!!!!!
- I should study it more deeply, it's so interesting! 
