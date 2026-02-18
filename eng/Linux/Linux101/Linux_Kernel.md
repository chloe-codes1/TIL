# Linux Kernel

> Let's learn about the Linux Kernel

<br>

<br>

### What is the Linux Kernel?

- It is a **resource manager** that efficiently manages the resources in the system, and has the following key functions

  1. **Processor Management**
     - Multiple processes are connected in **parallel** to improve processing speed
     - Processes running in the system are also resources to be managed by the kernel, and it efficiently **allocates** and **executes** the required processors to each process according to the OS's processing demands

  2. **Process Management**
     - An OS has at least one or more processes running
       - A process is also called a **task**, and it is the basic unit that performs a given job
     - The kernel uses a **scheduler** to **create** and **remove** multiple processes, and **connects** and **manages** them with the external environment
  3. **Memory Management**
     - Provides **virtual address spaces** so that each process can run in an independent space
     - Provides the ability to overcome physical limitations based on `virtual memory`

- In addition, it also performs functions such as **File System Management**, **Device Control**, and **Network Management**

<br>

- The Linux Kernel is the most important part of the OS
  - It resides in the processor and system memory, managing hardware resources like devices and memory,
  - Manages process scheduling to implement **multiprocessing**, and
  - Performs the core role of the OS by processing I/O connected to the system!
