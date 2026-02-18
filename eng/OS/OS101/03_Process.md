# Process

> Reference: [Ewha Womans University OS Lecture - Professor Ban Hyo-kyung](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)
>

<br>

## Program Execution (Memory load)

- A program is stored as an executable file in the file system,
- When executed, the program is loaded into memory and becomes a process
- At this point, the OS Kernel is already loaded into memory
- When a program is executed, it has its own independent Address Space in `Virtual Memory`
  - The immediately needed parts are loaded into `Physical memory`,
  - Parts not loaded into Physical memory go into the `Swap area`
  - Some of these exist as files in the file system

### Address Translation

Translation from the address in virtual memory to the physical memory address is needed

### Virtual Memory

- stack
  - Local variables within functions are located here

      → Related to function calls and returns

- data
  - Global variables / values that exist from program start to termination are located here
- code
  - Code from the executable file is loaded here
  - Machine instructions to be executed by the CPU are located here

      → Compiled machine code

- `Kernel Address Space`
  - Since the Kernel also makes function calls, it is similarly composed of stack, data, and code

## Contents of the Kernel Address Space

### Structure

- The Kernel is a program consisting of a function structure
- Each Process's Address Space is composed of Code, Data, and Stack

### Components

- The OS's `Code`

    > The tasks performed by the OS are mainly contained in the Kernel Code
    >
  - System call, Interrupt handling code
  - Code for resource management
  - Code for providing convenient services
- The OS's `Data`
  - Contains data structures for managing all hardware and processes

      → This is called `PCB (Process Control Block)`

- The OS's `Stack`
  - To know what is currently running, each process's kernel stack is stored separately

      → Stored separately depending on which process was executing before entering the kernel (before the kernel was called)

  - Since it is the Kernel's stack, it is related to kernel functions

## Functions Used by User Programs

- User-defined functions

    > Located within the corresponding process address space
    >
  - Functions defined in one's own program
  - Only need to change the program counter value to execute machine instructions at a different location
- Library functions

    > Located within the corresponding process address space
    >
  - Functions not defined in one's own program but imported for use
  - Included in one's own program's executable file
- Kernel functions

    > Located within the kernel address space
    >
  - Functions of the operating system program

      → Functions contained in the kernel's code

  - Crossing the virtual memory address space to switch to another program's area

      → Executed after transferring CPU control to the OS

  - Calling a kernel function == `System call`

## Program Execution

### User-Defined & Library Function Call

- user mode (mode bit: 1)
- Code in the address space is executed in user mode

### System Call

- kernel mode (mode bit: 0)
- CPU control is transferred to the OS, and code in the OS address space is executed in Kernel mode

## Concept of a Process

### What is a Process?

A running program

→ *Process is a program in execution*

### Context of a Process

> Represents the current state of a Process
→ A concept that changes over time
>
- Hardware context representing CPU execution state

    > How far has the CPU executed?
    >
  - Program Counter

      → Where is execution currently happening

  - Various registers

      → What values were stored in the Registers

- Process's address space

    > What is in its own memory space?
    >
  - code, data, stack
- Kernel data structures related to the Process
  - `PCB (Process Control Block)`
    - A data structure containing information about how much CPU, memory, etc. has been used
    - Since the context can be known by looking at the PCB, it can be called a data structure for managing processes
  - Kernel Stack
    - Each process has a different kernel stack

## Process States

> A Process is executed as its state changes
>

### `Running`

- A state where the process holds the CPU and is executing instructions
- Only 1 process executes machine instructions on the CPU at any given moment
  - The process holding the CPU is said to be in the running state

### `Ready`

- A process waiting for the CPU

    (All other conditions such as memory are satisfied)

### `Blocked (wait, sleep)`

- A state where the process cannot execute instructions even if given the CPU
- A state where the process is waiting for an event (e.g. I/O) it requested to be satisfied
  - e.g. When a file needs to be read from disk
- When interrupted, it means the ongoing event has completed, so the state is changed to Ready

### New

A state where the process is being created

### Terminated

A state where execution has finished

## Process State Transition Diagram

<p align="center" width="100%">
  <img width="713" alt="process state" src="https://github.com/chloe-codes1/TIL/assets/53922851/8f7c73db-972e-48cc-8388-52315c0a050e">
</p>

- new
  - A state being created

      → If creation has not started, it is not a process!

- ready
  - A state ready to execute immediately once CPU is allocated
  - The parts that need the CPU must be loaded into memory
- running
  - Becomes running state when the CPU scheduler dispatches
  - Cases when running state ends
    - Timer interrupt
      - Allocation time expired
      - Must go to the back of the ready queue and wait in line
    - I/O or event wait
      - Enters blocked state due to a long-running task
    - Exit
      - Termination
- waiting (blocked)
  - When the long-running task finishes (usually an interrupt occurs), the process's state is changed to ready, preparing it for CPU execution again
- terminated
  - A state being terminated

      → Once termination is complete, it is no longer a process!

## PCB (Process Control Block)

<p align="center" width="100%">
  <img width="230" alt="pcb" src="https://github.com/chloe-codes1/TIL/assets/53922851/85034d50-fde4-4960-ace3-d8c07fe7357a" >
</pr>

### Description

A data structure maintained by the OS to manage each process, representing the information maintained per process

### Components

> Maintained as a struct
>
- Information used by the OS for management
  - Process State, Process ID
  - Scheduling Information, Priority (CPU is allocated to the process with the highest priority)
- Hardware values related to CPU execution

    > Values saved in preparation for Context Switching
    >
  - Program Counter, Registers
- Memory related
  - Location information of code, data, stack
- File related
  - Open file descriptors
    - Used to uniquely identify a file or I/O resource (allocated sequentially starting from 0)
    - A process can read or write files using open file descriptors
      - Can perform I/O on files, and used when opening or closing files

## Context Switching

<p align="center" width="100%">
  <img width="470" alt="context switch" src="https://github.com/chloe-codes1/TIL/assets/53922851/92eca9fc-8723-4504-b944-322acbae5088">
</p>

### Description

The process of handing the CPU from one process to another process

### Why It Is Needed

- The CPU is not simply taken away from another program; the Process Context must be set so that when the CPU is allocated again, the process knows where to resume
- e.g. To have the CPU switch from process A to process B, information such as where the current machine instruction is being executed must be saved to process A's PCB before handing the CPU to process B

### Operation

> When the CPU is handed over to another process, the OS performs the following operations
>
- Save the state of the process giving up the CPU to that process's PCB
  - Save to the PCB where execution was in the current machine instructions and what values were placed in the registers
- Read the state of the process newly acquiring the CPU from its PCB

### Distinguishing Context Switches

> A context switch does not necessarily occur when a System Call or Interrupt happens
>

### What is a context switch

User process A ↔ User process B

### What is not a context switch

User process A → OS → (back to) User process A

### Relationship between context switch and overhead

- Going from user mode to kernel mode is a relatively lower overhead operation compared to a context switch
- While some context information such as CPU execution information must be saved to the PCB, the burden is much greater in the case of a context switch (e.g. cache memory flush)

## Queues for Process Scheduling

> Processes move between various queues during execution
>

### Job queue

The set of all processes currently in the system

### Ready queue

The set of processes currently in memory waiting to acquire the CPU for execution

### Device queues (I/O Queue)

- Long-running tasks
- The set of processes waiting for I/O device processing

### Appearance of the Process Scheduling Queue

<p align="center" width="100%">
  <img width="473" alt="process scheduling queue" src="https://github.com/chloe-codes1/TIL/assets/53922851/9fac457b-febe-4267-ab3c-11fafb653744">
</p>

- `fork a child`
  - Creating a child process

      → Creates by duplication

  - Usually allocated to the child since it is more effective to hand the CPU to the child

## Scheduler

> A part of the code within the OS
>

### Long-Term Scheduler (job scheduler)

> Responsible for memory scheduling within the OS
>
- Determines which of the starting processes to send to the ready queue
- Concerns the problem of giving memory (and various resources) to a process
  - Responsible for loading processes into `memory` when they are executed
- Controls `Degree of Multi-programming`
  - What is Degree of Multi-programming?
    - Refers to the number of programs loaded in memory
  - The long-term scheduler is responsible for controlling how many programs are loaded in memory
- Time sharing systems usually do not have a long-term scheduler (unconditionally ready status)

### Short-Term Scheduler (CPU scheduler)

> Responsible for CPU scheduling
>
- Determines which process to run next
- Concerns the problem of giving `CPU` to a process
- Must be sufficiently fast (millisecond scale)

### Medium-Term Scheduler (Swapper)

> Time sharing systems use a medium-term scheduler instead of a long-term scheduler
>
- Evicts an entire process from memory to disk to free up space
- Concerns the problem of taking `memory` away from a process

  → Give everything first, and if memory becomes insufficient and overall system performance drops, evict from memory

- Controls `Degree of Multi-programming`

## Process States

### Suspended (stopped)

- A state where process execution is halted for external reasons
- The process is entirely `swapped out` to disk
- e.g.)
  - When the user pauses the program (by break key)
  - When the system suspends the process for various reasons

      (When too many processes are loaded in memory)

      → The medium-term scheduler evicts the entire process from memory to disk to free up space

### Blocked vs Suspended

- Blocked
  - Becomes Ready when the event it requested is satisfied
- Suspended
  - Must be resumed externally to become Active

## Process State Diagram

> State diagram including Suspended
>

<p align="center" width="100%">
  <img width="754" alt="process status" src="https://github.com/chloe-codes1/TIL/assets/53922851/3ed6f386-fd98-40e5-b692-6013748dc4e9">
</p>

### Suspended Blocked

- If the process enters suspended while performing I/O,
  - The I/O operation continues as is and the process enters Suspended Blocked
  - When the I/O operation finishes, it goes to Suspended Ready
    - Just as a process goes from Blocked → Ready when a long-running task finishes, it goes from Suspended Blocked → Suspended Ready

### Swap Out / Swap In

- Swap out
  - Being entirely evicted from memory
- Swap in
  - Being loaded back into memory

### Running (User mode / Monitor mode)

<p align="center" width="100%">
  <img width="753" alt="running status" src="https://github.com/chloe-codes1/TIL/assets/53922851/2ac2c638-823d-4ff1-9b5d-6c634e96c554">
</p>

- `Running (User mode)`
  - When a process is executing its own code
- `Running (Monitor mode)`
  - When OS code is being executed due to a system call to the OS
  - Since the program has not lost the CPU, it is considered to be using the CPU
    - In the case of a System call
      - The process is running in kernel mode
    - In the case of receiving an Interrupt
      - e.g. While the CPU is running, an I/O controller generates another interrupt and the CPU is handed to the OS
      - Even though the interrupt was received for reasons unrelated to the program, it is still considered to be Running

          → It is not expressed as the OS is Running

          → The process before receiving the Interrupt is considered to be Running

## Thread

> *"A `thread` (or `lightweight process`) is basic unit of CPU utilization"*
→ It is the unit of CPU execution
>
- A Thread is the part of a Process that holds only what is necessary for CPU execution
- The Process is shared, while Threads each have their own according to the task

<p align="center" width="100%">
  <img width="956" alt="thread address space" src="https://github.com/chloe-codes1/TIL/assets/53922851/2774cb24-80b7-4b65-8cc0-fd9ef2e97c8e">
</p>

### Components of a Thread

<p align="center" width="100%">
 <img width="959" alt="component of thread" src="https://github.com/chloe-codes1/TIL/assets/53922851/779cb0da-ea79-48e8-8200-ef21d04ddc69">
</p>

- program counter
- register set
- stack space
  - In the address space, a thread only has the stack related to function calls
  - Everything else is shared with other threads within the process

### Parts shared with peer threads (= `task`)

- code section
- data section
- OS resources

→ A traditional heavyweight process can be viewed as a task with a single thread

### Advantages of Threads

- `Responsiveness`
  - In a task structure composed of multiple threads, even while one server thread is in a blocked (waiting) state, another thread within the same task can run, enabling `faster processing`
- `Resource Sharing`
  - Multiple threads can share the process's binary code, data, and resources
- `Economy`
  - creating & CPU switching thread (rather than a process)
  - In the case of Solaris, the overhead for these two is 30x and 5x respectively
- `Throughput & Performance`
  - Multiple threads performing the same task can cooperate to achieve `high throughput` and `performance improvement`
- `Utilization of Multi-Programming Architectures`
  - Using threads can increase `parallelism`

### Implementation of Threads

- `Kernel Threads`

    > supported by kernel
    >
  - When the OS is aware of the existence of threads
  - The OS can hand the CPU between different threads (like processes)
- `User Threads`

    > supported by library
    >
  - When the OS is not aware of the existence of threads
    - When the OS sees it as a single process without threads
  - The OS cannot hand the CPU between threads
    - This means management at the user program level, such as requesting asynchronous I/O from the OS within the process and immediately receiving control back to hand the CPU to another thread

## Process Creation

- A parent process creates a child process
  - Creates the child by duplicating an identical copy of the parent process
  - Cannot create directly; requests the OS to create it through a system call

      → fork()

- Forms a tree (hierarchical structure) of processes
- A process requires resources
  - Received from the OS
  - Can share with the parent process
    - but, since parent and child processes are actually separate processes, they `compete` for resource allocation
- Resource sharing
  - Model where parent and child share all resources
  - Model where they share some
  - Model where they share nothing
- Execution
  - Model where parent and child coexist and execute
  - Model where parent waits until child terminates
- Address space
  - Child copies the parent's space (binary & OS data)
  - Child loads a new program into that space
- Unix example
  - `fork()` system call creates a new process
    - Copies the parent exactly (OS data except for PID + binary)
    - Allocates address space
  - A new program is loaded into memory through the `exec()` system call following fork

## Process Termination

- A process notifies the OS after executing its last instruction → `exit`
  - The child sends output data to the parent (via `wait`)
  - The process's various resources are returned to the OS
- A parent process terminates a child's execution → `abort`
  - The child exceeds its allocated resource limit
  - The task assigned to the child is no longer needed
  - When the parent exits
    - The OS does not allow the child to continue running when the parent process terminates
    - Terminates step by step from the lowest level of the tree

## fork() system call

- A Process is created by the fork() system call
  - Creates a new address space by duplicating the caller

### Distinguishing Parent process and Child process

<p align="center" width="100%">
 <img width="938" alt="parent process and child process" src="https://github.com/chloe-codes1/TIL/assets/53922851/6e44b7db-213b-46b3-95c3-cb9103b1b79d">
</p>

- When fork() is executed, the parent process receives the child process's pid as the return value
  - The child process returns 0

## exec() system call

- A process can execute several different programs through the exec() system call
- Replaces the caller's memory image with a new program
- Overwrites one process completely with a new process and executes it

<p align="center" width="100%">
 <img width="932" alt="exec() system call" src="https://github.com/chloe-codes1/TIL/assets/53922851/53618845-c495-4da2-854b-9c2509a1e715">
</p>

- execlp()
  - Calls the exec system call within this function
  - parameter
    - 1st: program name
    - 2nd: argument to pass to the program

### fork() and exec()

When you want to create a child process to run a different program,

- Execute fork() to duplicate, then
- Execute exec() in the child process so that
  - The parent process continues executing the original program
  - The child can execute a new program

## wait() system call

- When Process A calls the wait() system call,
  - The kernel puts process A to sleep until the child terminates → `block state`
    - In addition to blocked state for waiting on long-running tasks, for shared resources with child processes
  - When the child process terminates, the kernel wakes up process A → `ready state`

<p align="center" width="100%">
  <img width="951" alt="wait() system call" src="https://github.com/chloe-codes1/TIL/assets/53922851/08767a9b-eba3-4d6c-8f1a-7428f3acc143">
</p>

- In Linux, when entering a command, each line that accepts input is a process
  - A shell process is running!
- When a command is executed, it runs as a child process of that command
  - The parent process is in blocked status, so it goes into sleep state
    - e.g.) When opening an editor with the vi command, the terminal enters a blocked state
  - The parent process enters a wait state until the child process terminates

<p align="center" width="100%">
 <img width="667" alt="parent & child process" src="https://github.com/chloe-codes1/TIL/assets/53922851/e9b14d76-a744-4a10-bf41-5bdfdf2b350c">
</p>

## exit() system call

### Process Termination

- `Voluntary termination`
  - Terminates through exit() system call after executing the last statement
  - Even if not explicitly written in the program, the compiler inserts it at the position where the main function returns
- `Involuntary termination`
  - Parent process forcefully terminates the child process
    - Child process requests resources exceeding the limit
    - Task assigned to the child is no longer needed
  - Typing kill, break, etc. on the keyboard → interrupt
  - When the parent terminates
    - Children are terminated before the parent process terminates

## System calls related to Process

- fork()
  - create a child (copy)
- exec()
  - overlay new image
- wait()
  - sleep util child is done
- exit()
  - frees all the resources, notify parent

## Cooperation between Processes

### Independent Process

Since processes execute with their own address spaces, in principle, one process cannot affect the execution of another process

→ They are independent!

### Cooperating Process

Through process cooperation mechanisms, one process can affect the execution of another process

### IPC: Interprocess Communication

<p align="center" width="100%">
 <img width="953" alt="message passing vs shared memory" src="https://github.com/chloe-codes1/TIL/assets/53922851/9b8b479e-ece9-418d-8f13-6018f15482b5">
</p>

- `message passing`
  - Description
    - A method of passing messages
    - Messages are passed through the kernel
  - `Message System`
    - A system that communicates without using any shared variables between processes
  - `Direct Communication`
    - Explicitly specifies the name of the process to communicate with
    - An explicit message delivery method agreed upon between both parties specifying who to send the message to
  - `Indirect Communication`
    - Indirect delivery of messages through a mailbox (or port)
    - A method where the message is delivered without specifying a target, and one of the cooperating processes picks it up
- `shared memory`
  - A method of sharing address space
  - There is a shared memory mechanism that allows even different processes to share some address space
  - However, sharing should only be done when the processes can trust each other
- Note) `thread`
  - Since threads are effectively within a single process, it is difficult to consider them as inter-process cooperation, but since threads composing the same process `share address space`, cooperation is possible
