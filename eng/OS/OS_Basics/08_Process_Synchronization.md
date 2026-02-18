# Process Synchronization

<br>

## Critical Section & Critical Section Problem

### Critical Section

As mentioned in the problems of multithreading, the code region that performs operations accessing the same resource simultaneously (e.g., using shared variables, using the same file) is called the Critical Section

<br>

### Critical Section Problem

- It refers to designing a protocol that allows processes to use the critical section together
- Requirements (basic conditions for resolution)
  - `Mutual Exclusion`
    - If process p1 is executing in the critical section, other processes cannot execute in p1's critical section
  - `Progress`
    - If no process is executing in the critical section, only processes that are not performing any separate operations can participate as candidates for entering the critical section
  - `Bounded waiting`
    - After p1 applies for entry to the critical section, there must be a limit on the number of times other processes are allowed to enter the critical section before p1 is admitted

<br>

## Solution

### Mutex Lock

- To prevent simultaneous access to shared resources, `a process entering the Critical Section acquires a lock`, and `releases the lock when exiting` the critical section, preventing simultaneous access
- Limitation
  - Cannot be applied in multi-processor environments from a time efficiency perspective

<br>

### Semaphores

> A synchronization tool for solving the critical section problem at the software level
>
- Description
  - A synchronization technique used as a method to limit access by multiple processes or threads to n shared resources in a multiprogramming environment
- Types
  - `Counting Semaphore`
    - Used for `access control` of resources with a limited number of available units, and the semaphore is initialized to the number of available resources
    - The semaphore decreases when a resource is used and increases when released
  - `Binary Semaphore`
    - Also called `MUTEX`, named after the initials of Mutual Exclusion
    - As the name suggests, it can only have values between 0 and 1, and is used to solve the Critical Section problem among multiple processes
- Disadvantages
  - `Busy waiting`
    - In the initial version of Semaphore called `Spin lock`, a process that needed to enter the Critical Section had to repeatedly execute the entry code, wasting CPU time
      - This is called Busy Waiting and is inefficient unless in special circumstances.
    - Generally, a Semaphore `blocks processes that attempted to enter the Critical Section but failed`, and then `wakes them up again` when a spot opens in the Critical Section.
      - In this case, the time waste problem caused by busy waiting is resolved.
  - `Deadlock`
    - The Semaphore has a Ready Queue,
    - Two or more processes are waiting indefinitely to enter the critical section, and
    - A situation where the process executing in the critical section can only exit if a process waiting to enter executes

<br>

### Monitor

- A design construct of high-level languages, an `abstracted data type` that makes developer's code `mutually exclusive`
- Handles both key acquisition for accessing shared resources and release after resource use
  - Semaphore requires direct handling of key release and shared resource access!
