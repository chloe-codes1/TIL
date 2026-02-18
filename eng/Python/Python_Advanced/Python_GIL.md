# Python GIL (Global Interpreter Lock)

### What is GIL?

- GIL is a concept that extends the lock used in threads to the interpreter level
- It prevents multiple threads from executing simultaneously
  - It enforces that only one Bytecode is executed at any given point in time
- Each thread can only execute after waiting for the GIL to be released by another thread
  - Even if implemented with multi-threading, it essentially operates as single-threaded

### Advantages

: Multi-threading using GIL is easier to implement than multi-threading without it, and in memory management approaches that use reference counting, GIL results in less overhead, providing better performance than the fine-grained lock approach in single-threaded scenarios

### Disadvantages

Performance issues

- Cases where performance issues arise due to GIL include when tasks that are heavily `CPU-bound` (such as compression, sorting, encoding) are performed using `multi-threading`
- In these cases, even with multi-threaded execution, there is barely any difference compared to single-threaded execution due to GIL
- To solve this, `multi-threading` should be used for `IO-bound programs` such as file and network IO, while `multi-processing` should be utilized for CPU-bound tasks
