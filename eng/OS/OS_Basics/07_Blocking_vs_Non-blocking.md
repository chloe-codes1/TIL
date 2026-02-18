# Blocking vs Non-blocking

> Blocking and Non-blocking
>
>
> → From the perspective of control

<br>

### Blocking

- Waiting until I/O finishes
  - why?
    - Because the function does not return until it finishes
- The user process `suspends work and waits` until the kernel completes the task
- Since I/O operations barely use CPU resources, the blocking approach results in `significant CPU resource waste`
- `Blocking is done for synchronization`

<br>

### Blocking vs Synchronous

- If it is `not mandatory to stay in the wait queue` while waiting for the system's return, it is synchronous
- If it is `mandatory to stay in the wait queue` while waiting for the system's return, it is blocking

<br>

### Non-blocking

- Created to overcome the inefficiency of the blocking approach
- Does not suspend the user process's work while I/O operations are in progress
- When the user process makes a function call (`system call`) to the kernel for I/O processing, the kernel returns a result immediately regardless of the function's progress
  - The result returned at this point is the `data` that can be retrieved at that moment
  - Initially there may be no data to retrieve, but over time, data becomes available
- Problem
  - The client must continuously `check whether` the returned value has reached the desired size (`polling`)
    - In the process of checking whether the returned data is ready (whether it has reached the desired value), if numerous client requests occur simultaneously, it can place `a significant burden on the CPU`

<br>

### Non-blocking vs Asynchronous

- If the `result (data) is returned along with` the system call return, it is non-blocking
- If the `result (data) is not returned along with` the system call return, it is asynchronous
- Summary
  - The asynchronous approach delivers data through callback functions, events, or signals
  - The non-blocking approach includes data with every system call return, and checks whether the returned data has fully arrived as requested

<br>

### Blocking vs Non-blocking

- If the application `enters the OS wait queue` during execution and sends a response `after the system call for the request is completed`, it is `blocking`
- If the application `does not enter the OS wait queue` during execution and sends a `response immediately` regardless of execution status, it is `non-blocking`

<br>

### Summary

- Blocking vs Non-Blocking → `From the perspective of control`
- Sync vs Async → `From the perspective of order and result (processing)`
