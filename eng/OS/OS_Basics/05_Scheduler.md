# Scheduler

<br>

## Types of Queues for Process Scheduling (3 types)

- `Job Queue`
  - The set of all processes currently in the system
- `Ready Queue`
  - The set of processes currently in memory waiting to acquire the CPU for execution
- `Device Queue`
  - The set of processes waiting for Device I/O operations

<br>

## Types of Schedulers

### Long-Term Scheduler (Job scheduler)

> Memory is limited, and when many processes try to load into memory at once, they are temporarily stored in large-capacity memory (typically disk)
>
>
> → Its role is to `determine which processes from this pool should be allocated memory and sent to the ready queue`
>
- Handles scheduling between `memory` and `disk`
- Allocates memory and various resources to processes (admit)
- Controls the number of running processes
- Changes a process's state from new → ready (in memory)
- Note)
  - Having too many or too few programs loaded in memory both result in poor performance.
  - For reference, in time sharing systems, there is no long-term scheduler
    - Processes are immediately loaded into memory and become ready

<br>

### Short-Term Scheduler (CPU scheduler)

- Handles scheduling between `CPU` and `memory`
- Determines which process from the `Ready Queue` to run
- `Allocates CPU` to a process
  - scheduler dispatch
- Changes a process's state: ready → running → waiting → ready

<br>

### Medium-Term Scheduler

> Swapping!
>

- Evicts entire processes from memory to disk to free up space (`swapping`)
- Deallocates memory from processes
  - Releases memory allocation from a process!!
- A scheduler that controls too many programs being loaded into memory simultaneously in the current system
- Changes a process's state from ready → suspended
  - `Process state - What is suspended?`
    - A state where process execution is halted for external reasons, meaning the process has been removed from memory
    - The entire process is `swapped out` to disk
    - A `Blocked` state is waiting for other I/O operations, so it can return to ready on its own,
      - but this state is suspended for external reasons, so it cannot return on its own
