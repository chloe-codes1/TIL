# Multithread and Multiprocess

<br>

## Multithreading

### Advantages of Multithreading

- When tasks that were previously handled concurrently using processes are implemented with threads, memory space and system resource consumption are reduced
- When communication between threads is needed, instead of using separate resources, data can be exchanged using the global variable space or the dynamically allocated `Heap area`
  - Therefore, inter-thread communication methods are much simpler compared to inter-process communication methods
- A thread's `context switch` is faster than a process's `context switch` because there is no need to flush the cache memory
  - As a result, the system's throughput improves,
  - resource consumption decreases,
  - and the program's response time naturally shortens
- Because of these advantages, tasks are divided into threads within a single process

<br>

### Problems with Multithreading

- When programming based on `multi-process`, there are no shared resources between processes, so there is no situation where the same resource is accessed simultaneously. However, when programming based on `multi-threading`, this must be taken into account
  - Since different threads share data and heap areas, one thread may access variables or data structures being used by another thread and read or modify incorrect values
- Therefore, `synchronization` is necessary in a `multi-threading` environment
  - Synchronization controls the order of task processing and access to shared resources.
    - but, this can lead to `bottleneck` issues, which increases the likelihood of performance degradation
      - Therefore, bottlenecks caused by excessive `locks` should be reduced
- In a `multi-thread` environment, when multiple threads try to share a single resource, problems such as `Deadlock` can occur

<br>

## Multithread vs Multiprocess

- `Multi-thread`
  - Advantages
    - Multi-threading occupies less space than multi-process and has faster context switching,
  - Disadvantages
    - If one thread terminates due to an error, all threads may terminate, and
    - It has `synchronization issues`
- `Multi-process`
  - Advantages
    - In the multi-process approach, even if one process dies, other processes are not affected and continue to run normally,
  - Disadvantages
    - It requires more memory space and CPU time than multi-threading
- Summary
  - Multi-thread and multi-process are the same in that they perform multiple tasks simultaneously,
    - but they are suited or unsuited depending on the system they are applied to
  - Therefore, the appropriate operating method should be selected and applied based on the characteristics of the target system
