# What is Hyper-Threading?
>
> Let's learn about Hyper Threading!
>
> Reference: [Intel Docs](https://www.intel.com/content/www/us/en/gaming/resources/hyper-threading.html)

<br>

This article explains the difference between `single-threaded` and `multithreaded` applications, what `Hyper-Threading` is, and how it differs from `multithreading`

<br>

### What Is `Multithreading`?

- Multithreading is a form of **parallel** or **divided** tasks for **concurrent processing**
- Instead of providing a large workload to a single core, a thread program divides the work into multiple software threads
- These threads are processed in parallel by different CPU cores to save time

<br>

### What Is `Hyper-Threading`?

- A simultaneous multithreading technology created by Intel that assigns two virtual execution units to a single physical execution unit to improve performance
- Since two threads are added per core, the operating system recognizes the number of cores as physical cores * 2
  - In other words, this means that a single **physical core** acts like two **logical cores** capable of processing different software threads
- Two **logical cores** can perform tasks more efficiently than a traditional single-threaded core
  - Intel's `Hyper-Threading` technology improves CPU throughput by utilizing idle time when a core is waiting for a previous task to complete

<br>

### What Benefits Will I See from `Hyper-Threading`?

- With CPU `Hyper-Threading`, a PC can process more information in less time and run more background tasks without interruption
- In the right environment, this technology allows a CPU core to effectively perform two tasks at once

<br>

### See if Mac OS has enabled `Hyper-Threading`

You can check the difference between the number of physical processors and logical processors using the `sysctl` command

```sh
sysctl hw.physicalcpu hw.logicalcpu
```

<br>

I am using a MacBook with an Intel Core i7 processor, so I can confirm that `Hyper-Threading` is enabled as shown below

<p align="center">
  <img src="../../kor/OS/images/physical-and-logical-cpu.png" width="300">
</p>

<br>
<br>

*Done!*
