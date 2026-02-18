# What is an OS?

> Reference: [Ewha Womans University OS Lecture - Professor Ban Hyo-kyung](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)
>

## What is an Operating System?

- It provides a `convenient` `environment` for users to use the computer system without knowing the hardware
- It `efficiently` manages the limited `resources` (CPU, Memory, I/O) of the computer system to achieve maximum performance
  - ex)
    - Allocating CPU to running programs in short time intervals alternately (`round robin`)
    - Appropriately distributing memory space to running programs
      - memory: the workspace of the CPU
- A `software layer` installed directly on top of computer hardware that connects users and all other software to the hardware
  - Narrow definition (Kernel)
    - The core part of the operating system that resides in memory
  - Broad definition
    - A concept that includes not only the kernel but also various peripheral system utilities

## Functions of the Operating System

- The computer boots up

    == the operating system is loaded into memory

- Kernel
  - Resides in memory when the computer is running
- CPU Management
  - Reads machine instructions from memory every clock cycle and performs computations
  - The CPU cannot directly access I/O devices
    - Each I/O device has its own small CPU-like `I/O controller`, and the CPU requests the controller to execute the necessary operations on the I/O device
  - CPU Scheduling
    - The most important function of the operating system!
    - Machine instructions within the operating system command the CPU to execute specific programs, i.e., scheduling
    - A specific program is allowed to use the CPU for a limited time only, and when the allotted time expires, the CPU is handed over to another program

      → The operating system cannot do this alone; it requires hardware assistance

- Memory Management
  - How to divide and use limited memory
- Disk Scheduling
  - Disks are slow!
  - While executing a long-running task (e.g., reading a file from disk), the CPU moves on to another task and executes it
  - Just like the CPU, `multiple requests` come into I/O devices simultaneously, and the operating system schedules the order in which to process them efficiently so resources can be used effectively
- Interrupt and Caching
  - Interrupts and Caching are used to buffer the speed difference between the fast CPU and slow I/O devices
  - Caching
    - Introducing an intermediate layer
    - Caching frequently accessed data in memory
  - Interrupt
    - The CPU assigns work to the I/O controller and `does not wait`; instead, it finds a task that can be executed immediately and runs it
      - The I/O controller notifies the CPU that the task is complete through an `Interrupt`
        - The CPU performs an `Interrupt check` after each task to verify whether executed tasks have finished
    - When an Interrupt arrives, the CPU is handed over to the operating system, and the completed task is made available for the CPU to execute again
    - Interrupts are a mechanism for slow devices (e.g., disk I/O) to notify the CPU that their tasks have been completed

## Purpose of the Operating System

- Provide a convenient environment for using the computer system
- Efficiently manage the resources of the computer system
  - The brain of the computer is not the CPU but the OS! (professor's opinion)
    - The CPU is an entity good at calculations
    - Memory is an entity that stores things
    - The OS is an entity that `decides` how to use them (the ruler)
      - e.g.) When memory needs to be appropriately divided among programs, the OS makes that decision

## Classification of Operating Systems

### Concurrent Task Capability

- Single tasking
  - Processes only one task at a time
- `Multi-tasking`
  - Processes two or more tasks simultaneously
  - e.g.) Another command or program can be executed before one command finishes

### Number of Users

- Single user
  - e.g.) MS-DOS, MS Windows
- `Multi-user`
  - e.g.) Unix, Linux
  - Security and permission issues need to be resolved to support multiple users

### Processing Method

- Batch processing
  - Collects a certain amount of work requests and processes them all at once
  - Must wait until the task is completely finished
  - e.g.) Early Punch Card processing systems
- `Time sharing`
  - When performing multiple tasks, the computer's processing power is divided into fixed time units
  - Has shorter response time compared to batch processing systems
  - An interactive method
  - A method of splitting time to use given resources as efficiently as possible
  - e.g.) Unix
- Realtime OS
  - An OS for real-time systems where certain tasks must be guaranteed to complete within a specified time
  - Extended concept of real-time systems
    - Hard realtime system
      - Missing a deadline causes serious problems
      - e.g.) Nuclear reactor / factory control, missile control, semiconductor equipment, robot control
    - Soft realtime system
      - Best effort → tries its best but cannot guarantee
      - e.g.) When playing a video, if frames are not rendered, the video stutters

### Terminology

The following 4 terms are fundamentally the same in meaning, but each emphasizes slightly different aspects

- Multi-tasking
- Multi-programming
  - Emphasizes that multiple programs are loaded in memory simultaneously
- Time sharing
  - Emphasizes the meaning of dividing CPU time and sharing it
- Multi-process

The following term has a completely different meaning

- Multi-processor
  - Means that multiple CPUs (processors) are attached to a single computer
  - A topic dealt with in high-performance computing and cloud computing

## Examples of Operating Systems

### UNIX

- Most of the code is written in the C language
  - To control hardware elements, the operating system needs to be written in assembly language, but since that is difficult, the C language was created for easier human understanding
  - Became easier for humans to understand
- High portability
  - C language is compatible across multiple architectures, providing high portability
- Minimal Kernel structure
- Easily extensible for complex systems
- Source code is open
- Suitable for program development
- Various versions
  - System V, FreeBSD, SunOS, Solaris
  - Linux

        → Source code is open and development continues based on it

### DOS (Disk Operating System)

- Developed by MS for IBM-PC in 1981
- Single-user operating system
- Limited memory management capability (main memory: 640KB)

### MS Windows

- MS's multi-tasking GUI-based operating system
- Plug and Play
- Enhanced networking environment
- Provides compatibility with DOS application programs
- Rich support software

## Structure of the Operating System

### Process Management

- Process creation and deletion
- Resource allocation and deallocation
- Cooperation between processes

### Others

- Protection system
- Networking
- Command line interpreter

## Process

- What is a process?
  - A running program
- CPU Queue
  - Programs that want to use the CPU are lined up in a queue

## CPU Scheduling

Determining the order in which tasks in the CPU queue are executed when multiple programs are waiting in the CPU queue to use the CPU

→ One of the important roles of the operating system

### FCFS (First-Come First-Served)

- Description
  - A method of processing in the order requests arrive

        → Good fairness

- Problem
  - If an earlier request occupies the CPU for a long time, the average waiting time for subsequent tasks increases

        → Not efficient

### SJF (Shortest-Job-First)

- Description
  - Schedules the process with the shortest CPU usage time first
  - Guarantees minimum average waiting time

        → Good efficiency

- Problem
  - Starvation may occur

        → Fairness issue

### Round Robin (RR)

- The most widely used method in modern systems
- Each process has an equal CPU allocation time
  - When the allocation time expires, an Interrupt occurs, the process loses the CPU, and it goes to the back of the CPU queue
- When n processes are in the CPU queue
  - No process waits more than `(n-1)*allocation time`
    - Total processes n - myself
- Advantages
  - Short tasks can complete quickly within the given allocation time, and long tasks can continue their unfinished work when their turn comes again

        → Waiting time is proportional to the process's CPU usage time

## Memory Management

- Swap area
  - The immediately needed space of a running process is loaded into memory, but the parts that cannot fit due to memory space limitations are placed in the swap area
  - Located on a persistent disk, but the data becomes useless when power is cut off
    - Because the corresponding process is no longer running

- What should be evicted from memory?
  - Pages likely to be used again in the future should not be evicted, and pages unlikely to be used in the near future should be evicted for efficient management!
- `LRU (Least Recently Used)`
  - Deletes the page that was referenced the longest time ago
- `LFU (Least Frequently Used)`
  - Deletes the least frequently referenced page

## Disk Scheduling

- The disk head movement time takes the most time among disk access times

    → Scheduling should be done to reduce head movement distance
- Seek time must be reduced!

    → Disk scheduling is needed for this purpose

### FCFS (First-Come First-Served)

Takes a long time (inefficient)

### SSTF (Shortest Seek Time First)

- Efficient due to short movement distance
- but, starvation problem occurs

### SCAN

- Current disk scheduling method
- The head moves regardless of requests in the queue
- Processes requests from the queue as it moves

    → Similar to how an elevator operates!

## Storage Hierarchy and Caching

- The CPU executes machine instructions using values in Registers
- Cache Memory is placed between the CPU and memory to overcome the speed difference
- Currently, `Flash memory` is positioned between Main Memory and Magnetic Disk
- Primary
  - Volatile
  - CPU can directly access it (executable)
- Secondary
  - Non-volatile
  - CPU cannot directly access it, so it must be loaded into Primary for execution
- A layered architecture is used to overcome (buffer) speed differences
  - Copying data to a faster layer and reading the copy is exactly what `Caching` is!
- Caching
  - copying information into faster storage system
  - The question is: what to evict!

## Flash Memory

### What is Flash Memory?

- A semiconductor device (hard disk: magnetic)
- NAND type (storage), NOR type (for embedded code storage)
  - What we use (for storage purposes) is all NAND type!

### Characteristics of Flash Memory

- Non-volatile
  - Data is preserved even when power is turned off
- Low power consumption
  - Consumes less power compared to hard disks
- Shock resistance
  - Resistant to physical impact
- Small size
- Lightweight
- Write count limitation
  - Cannot write anymore after a certain number of writes
- Data can degrade over time
  - Data is read based on the amount of charge in a cell, and charge leaks out of the cell over time
    - Eventually, the data may become unreadable

### Usage Forms of Flash Memory

- For embedded system configuration in mobile phones, PDAs, etc.
- USB memory sticks
- SD cards
- Not only for mobile devices but also attempting to replace hard disks in large-scale systems under the name SSD (Solid State Drive)
