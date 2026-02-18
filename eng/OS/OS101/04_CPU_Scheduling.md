# CPU Scheduling

## CPU and I/O Bursts in Program Execution

<p align="center" width="100%">
  <img width="330" alt="CPU and I/O Bursts in Program Execution" src="https://github.com/chloe-codes1/TIL/assets/53922851/e3d3bdbc-5d81-4016-9090-cc3974ec6edc">
</p>

## Distribution of CPU-burst Time

<p align="center" width="100%">
  <img width="426" alt="CPU-burst Time" src="https://github.com/chloe-codes1/TIL/assets/53922851/d95a74c6-60fc-41f7-84b1-3adba67fbd97">
</p>

## Classification of Process Characteristics

Processes are classified into the following two types based on their characteristics

- `CPU bound job`
  - Tasks that use the CPU for long periods and I/O for short periods
    - few very log CPU bursts
  - Computation-intensive jobs
  - e.g.) Cases where long computations are performed such as scientific calculations
- `I/O bound job`
  - Tasks that use the CPU for short periods and I/O for long periods
    - many short CPU bursts
  - Jobs that require more time for I/O than for CPU computation
  - e.g.) Cases with heavy interaction with humans

### The Need for CPU Scheduling

- CPU Scheduling is needed because various kinds of jobs (=processes) are mixed together
  - Appropriate response should be provided for interactive jobs
    - Jobs that interact with humans
  - System resources such as CPU and I/O devices should be used evenly and efficiently
- The goal is to allow I/O bound jobs to acquire the CPU quickly
  - Because they need to get the CPU first to use it quickly and move on
  - Fast response is needed since they interact with humans
  - If the CPU cannot be given while I/O work is pending after CPU usage

## CPU Scheduler & Dispatcher

### CPU Scheduler

- The code within the operating system that performs CPU scheduling
- Selects which process to give the CPU to from among the Ready state processes

### Dispatcher

- Hands CPU control to the process selected by the CPU Scheduler
- This process is called a context switch

### Cases When CPU Scheduling is Needed

When the following state changes occur for a process

1. Running → Blocked (e.g. system call requesting I/O)
2. Running → Ready (e.g. timer interrupt due to allocation time expiry)
3. Blocked → Ready (e.g. interrupt after I/O completion)
4. Terminate

→ Scheduling in cases 1 and 4 is `nonpreemptive` (= voluntarily surrendered, not forcefully taken)

→ All other scheduling is preemptive (= forcefully taken)

## Scheduling Criteria

> Performance Index (= Performance Measure)
>
- **CPU Utilization**
  - keep the `CPU as busy as possible`
  - Higher CPU utilization is better, without leaving the CPU idle
- **Throughput**
  - `number of processes` that `complete` their execution per time unit
  - Higher throughput is better
- **Turnaround Time**
  - amount of time to `execute a particular process`
  - Total time from starting a CPU burst until going out for an I/O burst
    - Time waited in the ready queue + actual CPU usage time
- **Waiting Time**
  - amount of time a process has been `waiting in the ready queue`
  - Not just the first waiting time, but the total sum of all waiting times when coming to use the CPU
- **Response Time**
  - amount of time it takes `from when a request was submitted until the first response is produced`, not output

      (for time-sharing environment)

  - The time from when a process comes to use the CPU until it first uses it
    - NOT the time from when the process starts until it first uses the CPU!!

## Scheduling Algorithms

### FCFS (First-Come First-Served)

- Description
  - Executes processes in the order they arrive in the ready queue
- Problem
  - `Convoy effect`
    - short process behind long process
    - Short processes take a long time because a long-running process arrived first and uses the CPU for an extended period

### SJF (Shortest Job First)

- Description
  - Uses the next CPU burst time of each process for scheduling
  - Schedules the process with the shortest CPU burst time first
    - Gives the CPU first to the job that wants to use it the shortest
- Types

    > Two schemes
    >
  - `Non-preemptive`
    - Once the CPU is acquired, it is not preempted until the CPU burst is completed
  - `Preemptive`
    - If a new process arrives with a shorter CPU burst time than the remaining burst time of the currently executing process, the CPU is taken away
    - This method is also called `Shortest-Remaining-Time-First (SRTF)`
- Characteristics
  - SJF is `optional`
    - Guarantees `minimum average waiting time` for the given processes
    - Optimal in terms of waiting time
  - A priority number (integer) is associated with each process
    - CPU allocated to the process with high priority
      - (smallest integer = high priority)
  - SJF is a type of priority scheduling
    - `priority = predicated next CPU burst time`
- Problems
  - `Starvation`
    - low priority processes may never executed
  - `Aging`
    - as time progresses increase the priority of the process
- Predicting the next CPU Burst Time

    > How can we know the next CPU burst time? (input data, branch, user ...)
    >
  - Only estimation is possible
  - Estimated using past CPU burst times (exponential averaging)

### Priority Scheduling

> A priority number (integer) is associated with each process
>
- Characteristics
  - CPU is allocated to the process with the `highest priority`
    - smallest integer == highest priority
  - SJF is a type of priority scheduling
- Problem
  - `Starvation` : low priority process may never execute
- Solution
  - `Aging` : as time progresses, increase the priority of the process

### Round Robin (RR)

- Characteristics
  - Each process has an equal allocation time (time quantum)
    - Generally 10 - 100 ms
  - When the allocation time expires, the process is preempted and goes to the back of the ready queue to wait again
  - If n processes are in the ready queue with an allocation time of q time units, each process gets 1/n of the CPU time in units of at most q time units

        → No process waits more than (n-1)q time units

- Performance
  - q large → FCFS
  - q small → `context switch` overhead increases
- Advantages
  - Generally has longer average turnaround time than SJF, but `response time` is shorter

### Multilevel Queue

- Ready queue is split into multiple queues
  - `foreground`
    - interactive job
  - `background`
    - batch job (no human interaction)
- Each queue has an independent scheduling algorithm
  - `foreground`
    - RR
  - `background`
    - FCFS
- Scheduling for the queues is needed

    > Assigning wait to each queue
    >
  - **Fixed priority scheduling**
    - Divides into two priority groups (foreground, background)
    - serve all from foreground then from background
      - All processes in the foreground are executed first, then processes in the background group are executed
    - possibility of starvation
  - **Time slice**
    - Allocates CPU time to each queue in appropriate proportions
    - e.g.
      - 80% to foreground in RR
      - 20% to background in FCFS
- Queue distribution by Priority

  <img width="939" alt="image" src="https://github.com/chloe-codes1/TIL/assets/53922851/b0d90c74-43d8-4df6-8213-868c5e588afc">

  Once a queue is assigned, it does not change

### Multilevel Feedback Queue

- Processes can move to different queues
  - Higher queues have higher priority
  - Lower queues are filled only when upper queues are empty
- Aging can be implemented in this manner
  - Sending aged jobs to upper queues
- Parameters that define a Multilevel feedback queue scheduler
    1. Number of queues
    2. Scheduling algorithm for each queue
    3. Criteria for sending a process to an upper queue
    4. Criteria for demoting a process to a lower queue
    5. Criteria for determining which queue a process enters when it comes for CPU service
- e.g.

  <img width="882" alt="image" src="https://github.com/chloe-codes1/TIL/assets/53922851/bb011162-f164-4187-9a4a-659f51793655">

- Three queues
  - Q0 - time quantum 8 ms
  - Q1 - time quantum 16 ms
  - Q2 - FCFS
- Scheduling Flow
  - A new job enters queue Q0
  - It acquires the CPU and runs for the allocation time of 8ms
  - If it cannot finish within 8ms, it is demoted to Q1
  - It waits in line at Q1, acquires the CPU, and runs for 16ms
  - If it cannot finish within 16ms, it is demoted to Q2

### Multiple-Processor Scheduling

- Scheduling becomes more complex when there are multiple CPUs
- In the case of `Homogeneous processes`

    > CPUs where everyone has the same processing capability
    >
  - Can line up in a single queue and have processors pick from it
  - but, if there are processes that must be executed on a specific processor, the problem becomes more complex
- `Load sharing` (= Load balancing)
  - A mechanism is needed to appropriately share the load to prevent jobs from being concentrated on some processors
  - Separate queues vs shared queue approach
- `Symmetric Multiprocessing (SMP)`
  - Each processor makes its own scheduling decisions
  - For uniform tasks across multiple processors, it may be more efficient not to have a coordinating processor
- `Asymmetric multiprocessing`
  - One processor takes responsibility for system data access and sharing, and the other processors follow it

### Real-Time Scheduling

- `Hard real-time systems`
  - Must be scheduled to finish within a specified time
  - For this purpose, there are cases where the CPU arrival times of processes are known in advance for scheduling (off-line scheduling)
    - ↔ online scheduling
      - The system dynamically schedules processes during execution
      - Since decisions are made at the point when tasks arrive, only information available at execution time can be used
- `Soft real-time computing`
  - Must ensure higher priority compared to general processes
  - e.g. Raising the priority of the video playback process so it can acquire the CPU first and prevent video stuttering

### Thread Scheduling

> Multiple CPU execution units within a single process
>
- `Local Scheduling`
  - In the case of **User level threads**, the user-level thread library determines which thread to schedule
- `Global Scheduling`
  - In the case of **Kernel level threads**, the kernel's short-term scheduler determines which thread to schedule, just like regular processes

## Algorithm Evaluation

- `Queueing models`
  - Calculates various performance index values using arrival rate and service rate given as probability distributions
- `Implementation & Measurement`
  - `Implements` the algorithm in an actual system and `measures` performance against actual workloads for comparison
- `Simulation`
  - Writes the algorithm as a simulation program and compares results using `trace` as input
  - What is trace?
    - Data that serves as input for the simulation
    - Must be credible (should be representative of actual program behavior)
