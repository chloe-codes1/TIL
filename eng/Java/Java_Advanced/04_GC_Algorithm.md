# Garbage Collection Algorithm

<br>

### Parallel GC

> Applied as the default GC in Java 8
>

- Performs minor collection in `parallel`
  - Can significantly reduce GC overhead
- A GC designed for applications that handle `medium to large-scale datasets` running on multi-processor or multi-thread hardware
- `Parallel Compaction`
  - A feature that allows the Parallel Collector to perform major collection in `parallel`
  - When the `-XX:+UseParallelGC` option is specified, Parallel Compaction is used by default
- However, the use of multi-threaded collection is limited to the `Young` generation only
  - Young Generation Collection algorithm: `Parallel Scavenge`
  - Old Generation Collection algorithm: `Serial Mark-Sweep-Compact`

<br>

### G1 (Garbage First Collector)

> Applied as the default GC in Java 11
>

- A Collector designed for multi-processor machines with large memory
- The G1 Collector can be enabled with the `-XX:+UseG1GC` option
- Note that G1 GC is the only one that is not a Generational GC
  - The G1 collector is a unique collector that does not divide the heap into Young and Old regions
  - G1 eliminates the physical generation distinction and treats the entire heap as 1MB-sized regions
    - It is organized in a `grid pattern` and uses approximately `2000 regions`
  - The name G1 means that collection starts from the region most filled with garbage
    - When a region full of garbage is found, the collector runs immediately
- Live objects in Old regions are moved to other Old regions, and compaction occurs
- In G1, the concepts of Young and Old generations are `not fixed`
  - The set of regions where objects are `newly allocated` is the `Young` generation
  - The set of regions where `promotion` occurs is the `Old` generation

<br>

### ZGC

> Applied as the default GC in Java 17
>

ZGC is a scalable low-latency GC that can handle heaps ranging from 8MB to 16TB in size, and can be enabled using the `-XX:+UseZGC` option

- `Low-latency`
  - ZGC increases responsiveness by minimizing pauses for memory collection
  - It is a concurrent GC where application threads continue to run during collection operations, and pause times are very short
    - This allows maintaining high responsiveness even in large-scale memory environments
    - Maximum latency is less than 1 millisecond
- `Very Large Heap Support`
  - ZGC can handle heaps as large as 16TB
    - This makes it suitable for applications that perform large-scale data processing or memory-intensive tasks
- `Non-contiguous Collection`
  - Instead of collecting the entire heap at once, ZGC divides it into small region units and performs garbage collection
  - By processing only portions of the collection work, it can distribute pause times
- `Parallel Processing`
  - ZGC utilizes multi-threads to process GC operations in parallel
  - This efficiently distributes GC operations and reduces overall collection time
- `Efficiency`
  - It is efficient because there is no need to clean up the heap during collection
    - Typical GCs trigger `stop-the-world` events to perform memory collection operations
      - During this time, all application threads are paused for GC operations
      - These pause times can affect application responsiveness and performance
    - In contrast, ZGC maintains very short pause times during the heap cleanup process
  - ZGC continues to run application threads during collection operations and only triggers very short pauses when necessary
    - ZGC focuses on increasing application responsiveness by minimizing pause times
