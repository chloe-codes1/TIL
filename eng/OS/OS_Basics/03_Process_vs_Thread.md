# Process vs Thread

<br>

- A `Process` is simply a running program
  - When you run a program, it receives the resources (memory) needed for execution from the OS and becomes a `process`
  - In other words, a `process` refers to a running program that has been loaded from Disk into memory and can receive CPU allocation.
- A `Process` consists of an address space, files, memory, and other resources needed to run the program, as well as `threads`,
  - and the `thread` is what actually performs the work using the `Process`'s resources
- A `Process` includes a **process stack** that holds temporary data such as function parameters, return addresses, and local variables, as well as a **data section** that stores global variables
  - Additionally, a `process` includes a **Heap**, which is **dynamically allocated memory** during execution
- Every `process` has at least one `thread`, and a `process` with two or more `threads` is called a **multi-threaded process**
  - Tip) It is easy to understand if you think of a Thread as a worker in a workspace (factory) called a process!
- There is no limit to the number of `threads` a single `process` can have, but since each `thread` requires its own memory space (`call stack`) to perform work, the number of `threads` that can be created is determined by the `process`'s memory limit
