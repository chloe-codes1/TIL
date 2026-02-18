# Locality of Reference

> Cache Locality
>

<br>

### Locality

- Cache memory is a general-purpose memory designed to reduce bottleneck issues caused by speed differences between fast and slow devices
  - To fulfill this role, it must be able to predict to some extent `what data the CPU will want`
  - This is because cache performance depends on how much useful information that the CPU will reference later is contained in the small-capacity cache memory
- The `principle of data locality` is used to maximize the `hit rate`
  - The prerequisite for locality is based on the characteristic that programs do not access all code or data uniformly
  - In other words, `Locality` is the characteristic of `intensively referencing a specific portion at any given moment` rather than uniformly accessing information in storage
- Data locality is broadly divided into Temporal Locality and Spatial Locality
  - Temporal Locality: The characteristic where content at recently referenced addresses will be referenced again soon
  - Spatial Locality: The characteristic where most real programs reference content at addresses adjacent to previously referenced addresses

<br>

### Caching line

- Even if the cache is physically close, it would take a long time if you had to traverse all the data because you don't know where the desired data is stored
  - In other words, if the target data is stored in the cache, it should be accessible immediately for the cache to be meaningful.
- Therefore, when storing data in the cache, it is stored in `groups` using specific data structures, which is called a **caching line**
- Data stored in the cache needs to have `tags` that record information such as the `memory address of the data`
  - These collections of tags are called caching lines, and data is also fetched from memory based on caching line units
- Types of Caching lines
    1. Full Associative
    2. Set Associative
    3. Direct Map
