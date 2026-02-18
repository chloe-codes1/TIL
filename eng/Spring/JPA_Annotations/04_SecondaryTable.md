# @SecondaryTable

### Description

- An annotation used in JPA when an entity class is mapped to multiple tables
- When a single entity is mapped to multiple tables, additional tables can be defined and mapped

### Attributes

- `name`
  - Specifies the name of the other table to map
- `pkJoinColumns`
  - Specifies the JOIN column that connects the primary key of the other table to map
- `uniqueContraints`
  - Specifies unique constraints
