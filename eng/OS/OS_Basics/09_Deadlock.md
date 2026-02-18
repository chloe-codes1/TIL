# Deadlock

<br>

### What is Deadlock?

- A state where a `Process` cannot proceed to the next step because it cannot obtain resources
  - e.g.) A state where two processes wait indefinitely because the resources each wants are allocated to the other
- In a multiprogramming environment, situations can arise where limited resources are competed for
  - When a process requests a resource and that resource is unavailable at that time, the process enters a `waiting state`
  - When processes that have entered the waiting state can never change to the running state, it is called a deadlock

<br>

### Conditions for Deadlock Occurrence

> Deadlock occurs when the following `four` conditions hold simultaneously within a system
>
1. `Mutual Exclusion`
    - A resource can only be used by one process at a time
2. `Hold and Wait`
    - A process that is holding at least one resource must be waiting to acquire additional resources that are being used by other processes
3. `No Preemption`
    - Resources allocated to other processes cannot be forcibly taken until their use is complete
4. `Circular Wait`
    - In a set of processes {P0, P1, ...Pn}, P0 waits for a resource held by P1, P1 waits for a resource held by P2, P2...Pn-1 waits for a resource held by Pn, and Pn waits for a resource held by P0

<br>

### Deadlock Detection and Recovery

- `Deadlock detection`
  - Deadlock can be detected through a resource allocation graph
  - Running the detection algorithm every time a resource is requested incurs `overhead`
- `Recovery from deadlock`

    > Recover by terminating the process that caused the deadlock or releasing the allocated resources
    >
  - Process termination methods
    1. Abort all deadlocked processes
    2. Abort one process at a time until the deadlock is eliminated
  - Resource preemption methods
    1. `Preempt` resources held by deadlocked processes and allocate them to other processes, while suspending the affected process
    2. Preempt resources primarily from processes with lower `priority` and fewer execution counts
