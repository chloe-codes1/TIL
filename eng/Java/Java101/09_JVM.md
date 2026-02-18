# JVM

<br/>

### Role of the JVM

- It reads Java applications through the class loader and executes them together with the Java API
- The JVM acts as an `intermediary` between Java and the OS
  - It allows Java to be `reusable` regardless of the OS
- It performs the most important task: memory management, i.e., `Garbage Collection`

### Java Program Execution Process

- When a program is executed, the JVM `allocates memory` needed by the program from the OS
  - The JVM divides this memory into several areas according to their purpose and manages them
- The `Java compiler (javac)` reads the Java source code (.java) and converts it into Java bytecode (.class)
- Class files are loaded into the JVM through the `Class loader`
- The loaded class files are interpreted through the `Execution engine`
- The interpreted bytecode is placed in the `Runtime Data Areas` where actual execution takes place
  - `Runtime Data Areas`: Memory space allocated from the OS to execute the program

During this process, the JVM performs management tasks such as Thread Synchronization and GC as needed
