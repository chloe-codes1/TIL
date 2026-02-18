# Programming Glossary

<br/>
<br/>

1. `Compiler`

   : A tool that translates code written in a programming language into machine language that the computer can understand

2. `Syntax`

   : Grammar

3. `Syntactic Sugar`

   - The internal workings remain fundamentally unchanged, but the external form is replaced to make coding more convenient
   - A syntactic feature that makes a programming language's grammar simpler and more convenient to use
   - It does not actually extend the language's functionality, but simply allows for more concise expression or makes code more intuitive
   - ex)
     - Using list comprehension in Python to express loops more concisely
     - Using object literals in JavaScript to easily create objects

4. `Syntax Parser`

   : The process of analyzing whether the code written by the developer is grammatically correct, like a Compiler or Interpreter, and converting it into a language the computer can understand

5. `Script Language`

   : A language that does not require a separate compilation step. Consequently, it is a language that does not require specifying a data type for each variable.

      -> HTML, CSS, PHP, etc. are representative script languages

6. `IDE (Integrated Development Environment)`

   : A software application interface that provides an integrated development environment for efficient software development.

   Includes code editors, debuggers, compilers, interpreters, etc. and provides them to developers. ex) Eclipse, JDE, Android Studio, Visual Studio, Delphi, RStudio, NetBeans, Code::Blocks

   ​    -> Most widely used: Eclipse (IBM), Visual Studio (Microsoft)

7. `Control Flow (Flow of Control)`

   : The order in which statements are executed

8. `Parameter`

   : The value inside the parentheses of a function. (The raw material going into the function machine)

9. `Argument`

   : The actual value assigned to the parameter

10. `API (Application Programming Interface)`

   : An interface through which programs communicate with each other. In object-oriented programming (OOP = Object Oriented Programming), instances of classes are typically created to communicate, so the properties and methods of a class are collectively referred to as an API

 -> a set of routines, protocols, and tools for building software applications. Basically, an API specifies how software components should interact. Additionally, APIs are used when programming graphical user interface (GUI) components.

11. `AJAX (Asynchronous Javascript and XML)`

    : Asynchronous JavaScript and XML

12. `Asynchronous`

    : A method where tasks are performed immediately without blocking or waiting for other tasks.

    ex) Allowing users to freely navigate the screen while an app loads a large video

      -> Multiple tasks proceed simultaneously without waiting for any one task to finish

13. `Multi-thread`

    : Multiple tasks proceeding simultaneously

14. `Imperative Programming`

    : A programming paradigm that emphasizes the procedures and methods of How a program achieves its goal. Uses statements to change the program's state

15. `Declarative Programming`

    : A programming paradigm that focuses more on What the program achieves as a result.

      -> The opposite concept of imperative programming. Expresses the logic of computation without describing control flow.

16. `Script Language`

    : A language that does not require a separate compilation step. Web browsers like Chrome or Edge handle the compilation work. The term itself originates from theatrical scripts.

17. `Javascript Engine (Google V8)`

    : An engine that converts JavaScript into machine-understandable language, with Google's V8 being the most representative. Such JavaScript engines are primarily built with languages like C++.

18. `ECMA`

    : One of the JavaScript standards.

     -> Since it would be confusing if different browsers applied different standards, it is a standard established for JavaScript authoring.

19. `Node.js`

    : An extension of JavaScript, originally used primarily for web frontend, to a backend language.

      -> The JavaScript engine V8 is built with C++, and Node.js extends V8's C++ so that JavaScript can also handle the server side!

20. `Rendering`

    : The process of transforming a logical document representation into a graphical representation

       => The process by which code written in HTML, CSS, etc. appears on a website - Rendering 2 stages: layout calculation based on DOM elements and styles; screen representation of calculated elements - In browsers, rendering performance is one of the important factors.

      -> Improving rendering performance can enhance the perceived speed experienced by users

     -> Rendering issues when executing dynamic tasks with JavaScript can be minimized to improve performance

21. `Business Logic`

    : The part of an application program that performs data processing necessary for business operations. It refers to the 'logic' of calculating, judging, processing, etc. by utilizing data to perform data processing. Most client programs consist of User Interface and Business Logic, and server programs mostly consist of Business Logic.

    -> In programming, since business logic is the area that directly solves requirements, if maintenance is neglected, productivity and quality will deteriorate

22. `Lombok`

    : A library in Java that uses annotation-based approach like @Getter, @Setter to automatically generate Getter/Setter methods, Equals(), hashCode(), ToString(), and constructors that set values for member variables when writing DTO, VO, Domain Classes

23. `CDATA <![CDATA[...]]>`

    : CDATA sections provide a way to tell the parser that there is no markup in the characters contained by the CDATA section.
    This makes it much easier to create documents containing sections where markup characters might appear, but where no markup is intended. ( by MS Developer Network)
    (Unparsed) Character Data.

     -> In other words, it refers to character data that is not parsed. It functions to prevent text inside tags from being parsed. When dealing with text that the parser might incorrectly parse, it tells the parser that the content inside the tag can be ignored, thus preventing incorrect parsing. Used to represent strings. ex) In RSS data, content containing HTML or XML tags is wrapped in CDATA to avoid confusion with RSS XML tags

24. `PCDATA`

    : Parsed character data

25. `Groovy`

    : A scripting language that runs on the JVM (= Java Virtual Machine). Like Java, source code is written and runs on the Java Virtual Machine, but unlike Java, there is no need to compile the source code. Groovy is a scripting language and executes the source code as-is. It is compatible with Java, and Java Class Files can be used directly as Groovy Classes. The syntax is very close to Java, making it feel like a more user-friendly version of Java.

26. `Gradle`

    : Writing and executing build processing using Groovy, which can be described as 'easy-to-use Java'.

    -> Using Gradle, you can manage build processing by writing code almost identical to Java

28. `Maven`

    : XML-based build processing. It's fine for simple content, but when writing complex content, XML-based descriptions become quite difficult.

29. `IOC (= Inversion of Control)`

    : A strategy of reducing what the client code needs to worry about by handing over control to a framework designed to do certain tasks

    -> Called inversion of control

    -> Generally, a library means that the client code written by the programmer calls and uses the library's methods. The defining characteristic of a framework is that the framework's methods call the user's code

    -> First method

    Registering my methods with the framework's events and delegates. As long as the passed arguments and return types match, the framework code does not consider the objects and types I wrote -> It only detects and invokes registered methods
    -> Second method

    Implementing or inheriting interfaces and abstract types defined in the framework in my code and then passing them to the framework. Since the framework knows about interfaces and abstract classes, it can process the series of tasks I want to do

       => Injecting objects into the framework     => DI (= Dependency Injection)

30. `JDBC, DBCP`

    : Libraries related to DB connections in Java Web Applications

31. `JDBC (= Java DataBase Connectivity)`

    : An interface for connecting to databases in Java

      -> Databases like Oracle, MySQL, MsSQL provide their respective drivers for using JDBC

      -> JDBC connects to the DB through these drivers

32. `DBCP (= DataBase Connection Pool)`

    : Used for efficient DB connections, responsible for managing objects that maintain connections with the DB. When using DBCP, a certain number of DB Connection objects are created in advance when the WAS starts, and stored in a space called a Pool. When a DB connection request comes in, a Connection object is taken from the Pool, used, and then returned.

    **[ DBCP Configuration Options ]**

    1) `maxActive` : Maximum number of connections that can be used simultaneously

    2) `maxIdle`: Maximum number of connections that can be maintained when returning to the Connection Pool

    3) `minIdle`: Minimum number of connections to maintain

    4) `initialSize` : Minimum number of connections to fill the connection pool with via the getConnection() method

32. `Fault tolerance`

     : The ability of a computer or operating system to prepare for emergencies such as power shortages or hardware failures so that data in the running system is not lost or work in progress is not damaged

33. `HA (= High Availability)`

     : The property of information systems such as servers, networks, and programs being able to operate normally and continuously for a long period

     -> To provide high availability, a method of linking 2 servers is mainly used

     -> If a failure occurs in 1 of the 2 linked servers, the other server immediately takes over the work, enabling system failure recovery in just a few seconds

34. `In-memory Database`

     : A DBMS installed and operated in the main memory of the data storage

     -> Faster than disk-optimized databases because disk access is slower than memory access

     -> Internal optimization algorithms are simpler, executing fewer CPU instructions

     -> Accessing data in memory reduces search time when querying data, providing faster and more predictable performance than disk

35. `Subnet`

     : A smaller network that is divided from a single network

     -> Dividing a network is called `Subnetting`

     -> Subnetting can be performed through `Subnet Mask`

36. `Subnetting`

     : A network administrator efficiently distributing resources to improve network performance

     -> Dividing the network area and host area

37. `SandBox`

     : A technology that prevents files and programs from external sources from adversely affecting internal systems by running them in a protected area first rather than executing them immediately

     -> Used to protect files or processes within the system from malicious code introduced from external sources

     -> Files or tasks that have been verified as safe by running in the SandBox can modify the system, but unauthorized ones cannot

38. `Information Silo`

     : An exclusive management system where one information system or subsystem cannot interoperate with other related systems

     -> Information is not properly shared and is isolated in each system or subsystem, metaphorically compared to grain being trapped in a silo (storage tower), trapped within containers

39. `Data lake`

     : A collection of repositories that gather various types of unprocessed data in one place

     -> The concept of collecting and managing raw data (unprocessed data) from various domains in one place for efficient analysis and use of big data

40. `Scale-up`

     : A method of improving hardware performance for a server to operate faster

41. `Scale-out`

     : A method where multiple servers divide the work rather than a single server

     -> **Pros**

     - The cost of adding servers is less than the cost of upgrading hardware
     - Thanks to multiple servers, uninterrupted service can be provided

42. `Load Balancing`

    : When an internet service generates heavy traffic, multiple servers perform distributed processing considering server load rate increase, load volume, speed reduction, etc.

43. `Load Balancer`

     : A system that distributes traffic evenly among multiple servers

44. `DevOps`

    : A software development methodology emphasizing communication, collaboration, and integration between software developers and IT professionals, and a product of the interdependence between software development and IT operations

    -> DevOps is an organizational structure and culture that aims to speed up the overall development cycle by combining operations and development teams into one team

    Source: <https://bcho.tistory.com/1325>

45. `CI (Continuous Integration)`

     : A technique to proactively resolve errors in integration and reduce time spent on these processes by periodically performing the integration build process of gathering source code developed by individual developers and building all at once, rather than at specific points in time

     -> Gained more attention as the Agile methodology emerged

     -> Demonstrates time-saving effects in the build stage, testing stage, etc. for deployment, enabling keeping up with the pace of market changes

     -> Achieves both speed and quality!

     - Components for building a CI system

       - `CI Server`

         : A server that manages the build process

         ex) Jenkins, Travis CI

       - `SCM (Source Code Management)`

         : Source code version control system

         ex) Git, Subversion

       - `Build Tool`

         : A tool that performs compilation, testing, static analysis, etc. to generate working software

         ex) Maven, Gradle, Ant

       - `Test Tool`

         : A tool that automatically runs tests according to written test code, executed from the build tool's script

         ex) JUnit, Mocha

46. `Parsing`

    : Extracting and processing desired data from pages like HTML in a specific pattern or order

    - `Parser`
      - As part of compilation, it takes input such as statements from source programs or markup tags from HTML documents and divides them into units and parts that can be parsed syntactically
    - The syntactic analysis process where a computer acting as a **Parser** reconstructs into a **parse tree**
    - During parsing, a series of characters that are merely symbols are translated into machine language and become meaningful units
    - **Types of Parsing**
      - Bottom-up parsing
      - Top-down parsing

    ![img](https://t1.daumcdn.net/cfile/tistory/992F5C475AE5C0572E)

47. `MIME types`

     : A **media type** (also known as a **Multipurpose Internet Mail Extensions or MIME type**) is a standard that indicates the nature and format of a document, file, or assortment of bytes.

     **Browsers use the MIME type, not the file extension**, to determine how to process a URL, so it's important that web servers send the correct MIME type in the response's `Content-Type` header. If this is not correctly configured, browsers are likely to misinterpret the contents of files and sites will not work correctly, and downloaded files may be mishandled.

48. `ping`

     : A command that uses the ICMP protocol to send response requests to the address specified in the command and receives responses to determine the network status

49. `TraceRoute` - Linux / `TRACERT` - Windows

     : A network command that traces the **route information** and **delay time** at each route until reaching the specified host, useful for identifying where bottlenecks occur when *a specific site is inaccessible or experiencing delays*.

     It can check which **route (routing)** is taken for connection, **which section** has **how much** speed delay, and **where** packets were stopped.

     However, since values can vary due to *time of day/internal traffic/server status* and many other factors, repeated verification is necessary!

     > Install traceroute

     ```bash
     sudo apt-get install traceroute
     ```

     > Use traceroute

     ```bash
     $ traceroute www.google.com
     traceroute to www.google.com (172.217.31.164), 30 hops max, 60 byte packets
      1  _gateway (172.30.1.254)  5.195 ms  5.127 ms  5.105 ms
      2  220.78.3.1 (220.78.3.1)  5.071 ms * *
      3  125.141.249.21 (125.141.249.21)  5.364 ms  5.308 ms  5.262 ms
      4  * * *
      5  * * *
      6  112.174.73.178 (112.174.73.178)  6.510 ms 112.174.47.162 (112.174.47.162)  5.301 ms 112.174.73.178 (112.174.73.178)  4.858 ms
      7  74.125.52.16 (74.125.52.16)  31.913 ms  31.801 ms  33.951 ms
      8  108.170.242.129 (108.170.242.129)  36.142 ms 108.170.242.97 (108.170.242.97)  34.386 ms  34.811 ms
      9  209.85.253.109 (209.85.253.109)  36.711 ms  36.555 ms  36.483 ms
     10  nrt12s22-in-f4.1e100.net (172.217.31.164)  34.998 ms  33.267 ms  32.844 ms
     ```

50. `SRE (Site Reliability Engineering)`

    : " class **SRE** implements **Devops** "

    DevOps is a methodology and a direction for organizational culture aimed at solving the *silo (division) phenomenon* between development and operations. SRE, then, can be thought of as the specific practices and guides that Google applies to DevOps.

    - What does an SRE Engineer do?
      ![img](https://t1.daumcdn.net/cfile/tistory/99A3E6375CD44F9721)

51. `SSH (Secure Shell Protocol)`

     : One of the network protocols used for secure communication when computers communicate with each other over public networks like the internet

     Usage examples)

     1. **Data transfer**
        - ex) Using SSH to transfer files when pushing to Github
     2. **Remote control**
        - ex) Connecting to an AWS instance server via SSH to issue commands to that machine

     - Why SSH enables secure communication
       - When connecting to a computer for communication, authentication is done through a pair of keys (`Private Key`, `Public Key`) rather than through a password

52. `POC (Proof Of Concept)`

     : Used for the purpose of **verifying** new technology that has not been used in the market before introducing it into a project

53. `Pilot project`

     : A trial project conducted on a small scale before proceeding with a large-scale project using already verified technology

54. `BMT (Bench Marking Test)`

     : Performance testing

55. `Meta Programming`

     : A method of having the **compiler** generate program code in another language based on templates

     **Pros**

     - Optimization occurs at compile time, and as a result, execution speed can be faster
     - `Generic Programming` is possible
       - Because developers focus on the structures and data to be processed, and the conversion to a specific language is done by the compiler!
     - Concepts that the resulting language does not possess can be defined and written in **templates** and appropriately expressed in the resulting language, providing good **extensibility**!

     **Cons**

     - Generally, `Template Metaprogramming` involves programming in yet another form, making the code itself more complex
       - There are **readability** issues
     - Since new code is generated by the compiler, the dependency on the compiler is quite high
       - **Portability** issues may arise..!

56. `gRPC - RPC made by Google!`

     - What is **RPC**?
       - Remote Procedure Call, a communication technology that calls functions or procedures on a remote machine
       - The **Interface** for Request and Response between communicating parties must be defined, and then converted to code matching each side's programming language
         - The term for defining this interface is `IDL (Interface Definition Language)`!
         - The result of converting IDL into specific language code using compilers, etc. is called:
           - **Skeleton (server side)**
           - **Stub (client side)**!
     - Characteristics of **gRPC**
       1. High productivity and efficient maintenance
          - Uses only `ProtoBuf` to define services and messages
          - Since the data itself is **binary**, it can be processed very quickly without computer conversion
            - Being binary, lightweight packets can also be created!
       2. Support for various languages and platforms
          - C, C++, C#, Dart, Go, Java, Node.js, Object-C, PHP, Python, Ruby
       3. `HTTP/2` based communication
          - Unlike conventional HTTP, server and client can exchange data via streaming
          - Higher header compression rates than conventional HTTP are guaranteed, and messages transmitted are dramatically reduced through `ProtoBuf` serialization
     - **gRPC vs REST**
       - **Payload** difference
         - `gRPC`: Self-serialized data in **Protobuf** format
         - `REST`: Exchanges **JSON** data
       - **HTTP version** difference
         - `gRPC`: HTTP/2 based communication
           - Secures various advantages of HTTP/2 such as streaming and header compression!
         - `REST`: Generally HTTP/1.1 communication
       - Calling method difference
         - `gRPC`: Messages and services defined in **proto** files are generated in the form needed for each language
           - When the client calls a service method
             - The corresponding server-implemented service is executed
             - Request/response payload uses the generated results for the respective language
         - `REST`: Endpoints are expressed as HTTP method + URI, and payload handling is handled separately by server/client

     <https://do-study.tistory.com/94>

57. `OpenStack`

     - A cloud operating system that manages computing, storage, and network resources ([openstack.org](https://www.openstack.org/software/))

       - Controlling servers used in cloud computing requires specialized hardware knowledge and knowledge of the operating systems running the servers
       - Since they differ depending on hardware and operating system type, there is the problem of having to acquire new knowledge every time the environment changes
         - To solve this problem, OpenStack provides standards for cloud computing development regardless of server hardware and operating system!

     - OpenStack Components   [Source](https://velog.io/@dojun527/%EC%98%A4%ED%94%88-%EC%8A%A4%ED%83%9D%EC%9D%B4%EB%9E%80)

       ![image-20200620205417417](../kor/images/image-20200620205417417.png)

58. `Hypervisor`

     - A logical platform for running multiple operating systems simultaneously on a host computer
       - Also called a virtual machine manager (VMM)

59. `NAS (Network Attached Storage)`

    - Network Attached Storage
    - An external hard disk connected via LAN
    - A storage device that exchanges data over the network without being directly connected to a computer
      - Has many similarities to cloud storage

- Structurally, it is a **simplified**, **miniaturized** version of a storage server

60. `CDN (Contents Delivery Network)`

    - Technology that helps quickly deliver massive amounts of information (data) from **cache servers** to users who are geographically and physically distant
      - **how?**
        - Install cache servers (servers that store web pages and internet content) around the origin server
        - Cache servers pre-store frequently used information to process and respond to user requests
      - **benefits?**
        - Users can receive the same service from a nearby cache server without going through the distant origin server!
    - A server network strategically distributed worldwide
      - Technology that can quickly deliver content to physically distant users
    - CDN works by providing **alternative server nodes** from which users can download resources
      - Because these nodes are spread worldwide, they provide **fast responses** and download times for content due to **reduced latency**!

61. `Kibana`
    - An open source frontend application built on top of **Elastic Stack**
    - Provides functionality to **search** and **visualize** data indexed in **ElasticSearch**

62. `ElasticSearch`
    - An open source **distributed search engine** based on Apache Lucene, written in Java
    - Can store, search, and analyze massive amounts of data **quickly** and in **near real time (Near Real Time)**
    - ElasticSearch can be used standalone for search, or as part of the **ELK (ElasticSearch / Logstash / Kibana) Stack**

63. `ELK Stack`
    - **Logstash**
      - **Collects** and **parses** **log** or **transaction data** from various sources (DB, CSV files, etc.) and delivers them to `ElasticSearch`
    - **ElasticSearch**
      - **Searches** and **aggregates** data received from `Logstash` to obtain necessary information
    - **Kibana**
      - **Visualizes** and **monitors** data through `ElasticSearch`'s fast search

64. `Grafana`
    - An open source toolkit that provides the most optimized **dashboard** for **visualizing** time-series metric data
    - Can **connect various databases** and retrieve and visualize data from them

65. `Spinnaker`

    - A **Continuous Delivery Platform** supporting **multi-cloud**, developed by Netflix and open-sourced
    - Supports most major clouds including Google Cloud, Amazon, Microsoft
      - Simultaneously supports open source-based clouds or container platforms like Kubernetes and OpenStack

66. `AWS ECR`
    - A secure, scalable, and reliable **managed AWS Docker registry service**
    - Amazon ECR supports **private Docker repositories** with **resource-based** permissions using `AWS IAM`, allowing specific `users` or `Amazon EC2 instances` to access **repositories** and **images**
    - Developers can use the Docker CLI to push, pull, and manage images

67. `Scouter`
    - Open source **APM (Application performance monitoring)**
    - Provides monitoring functionality for applications using **JVM (WAS, Standalone application)** and OS resources

68. `Redis`
    - In-Memory Data Structure Store
    - Open source
    - Supports data structures
      - String
      - Set
      - Sorted-set
      - Hashes
      - List
    - Cache architecture
      - **Look aside cache**
        - Return if in cache,
        - Otherwise store in cache and return
      - **Write Back**
        - Store all data in cache, save cache data to DB only at specific points
          - ex) Accumulate logs in cache and push to DB at specific intervals

69. `ELK - Filebeat`

    - A lightweight `Producer` for **delivering** and **centralizing** **log data**

    - `Filebeat`, installed as an agent on servers,

      1. **Monitors** specified log file locations,
      2. **Collects** log events,
      3. Delivers them to `ElasticSearch` or `Logstash` for **indexing**

      ![image-20200911180015752](../kor/images/image-20200911180015752.png)

70. `OOM (Out of Memory)`

    - A state in a computer system where the memory needed to perform a certain operation is insufficient or absent
    - **Causes**
      - The Linux kernel uses virtual memory for memory allocation, so it can allocate memory for programs larger than the actual available physical memory
        - That is, memory not immediately used by a program is allocated later, so processes exceeding the actually available memory can be loaded
          - This is called **overcommit**!
        - If something actually starts being written to overcommitted memory, OOM occurs because there is not enough memory

71. `OOM Killer`

    - A process in the Linux kernel that **secures memory** when memory is insufficient
      - When memory is insufficient during system operation, it kills processes based on an internal priority algorithm
      - The Linux kernel has an **OOM (Out of Memory) Killer** to handle situations where there is no remaining memory during process memory allocation
      - The OOM Killer scores processes and kills the one with the lowest priority (excluding init) to secure memory
      - Therefore, when operating servers, memory must be well managed so that service daemons are not killed by the OOM Killer!

72. `Jolokia`

    - Generally, only Java code can directly access the JMX API, but there are adapters that convert the JMX API to standard protocols
      - One of them is **Jolokia**, which converts the JMX API to HTTP
    - **Jolokia** is an **agent** that can be deployed in a JVM,
      - Exposing `MBeans` through REST-like `HTTP endpoints`,
      - Making all information easily available to non-Java applications running on the same host
        - Can be deployed as an agent in a `regular JVM`,
        - Or as a WAR, OSGI, or module agent in `Java EE`

73. `Sticky session`

    - A feature that distributes traffic using cookies or sessions
      - Sticking to the server that gave the response to the first request like glue
      - Sending requests from a specific session only to the server that first processed them
        - Managing sessions by fixing all requests after the first one to a specific server!
    - **Disadvantages**
      - Load balancing may not work well
      - If a **failure** occurs on a specific server, sessions attached to that server may be lost

74. `DNS (Domain Name System)`

    - Developed to convert a host's **domain name** to a host's **network address** or vice versa
    - Converts a human-readable domain name to a numerical identification number (**IP address**) to find the address of a specific computer (or any device connected to a network)
      - ex)
        - A **distributed database system** that converts a computer's domain name like `www.example.com` to an IP address like `192.168.1.0` and provides routing information
    - In other words, it plays the role of replacing hard-to-memorize web IP addresses with the internet addresses we commonly know

75. `Logrotate`

    - A tool for storing and managing logs
    - As **processes** on the server run, numerous logs such as httpd, mysqld, access are generated in the `/var/log` directory

      - If these logs are not managed, the file system can reach its limit and cause **load** on the server
        - To prevent this situation, previous logs should be **compressed** and old logs should be **deleted** after a certain period
          - The program that periodically manages this series of tasks is `logrotate`

      - Generally, logrotate is executed using the **cron** daemon
    - logrotate is automatically installed with Linux

76. `CPU Load`

    - A value showing the average number of tasks (**processes**) that are **running** or **waiting** on the CPU
      - ex) If 4 tasks are found when checking 100 times whether there are running or waiting tasks on the CPU, the CPU Load is 0.04
    - The CPU Load when there are always only running tasks and no waiting tasks on the CPU is 1
      - Therefore, CPU Load can be used as a means to check **how well the CPU is being utilized**!
    - CPU Load is **proportional** to **cores**, and if there are 4 CPU cores, theoretically the CPU Load when there are always only running tasks and no waiting tasks is 4
    - `CPU utilization` is shown only as a value up to 100% regardless of remaining tasks, but `CPU Load` is a metric that also displays **remaining tasks**

77. `Rsync (Remote Sync)`

    - A **tool** and **network protocol** used to **copy** and **synchronize** remote files and directories
      - A tool widely used for backup in Linux and Unix
      - Rsync is a CLI tool, making it easy to develop **batch programs** using command line options
    - **Pros of Rsync**
      1. Can **copy** or **synchronize** files from remote systems
      2. Can copy **supplementary information** such as file ownership and group permissions
      3. Faster than `scp`
         - rsync uses the **remote-update** protocol to copy only files with **differences**
           - Although it copies all files and directories the first time,
             - From then on, it copies only files with differences, operating **faster** and more **efficiently**
      4. **Compresses** data for **sending/receiving**, using **less bandwidth**
    - **Usage**
      - `rsync OPTIONS SOURCE DESTINATION`
      - options
        - -v : Show progress in detail
        - -r : Execute recursively including subdirectories of the specified directory
        - -o : Preserve ownership attributes (root)
        - -g : Preserve group attributes
        - -t : Preserve timestamps
        - -D : Preserve device files (root)
        - -z : Compress data for transfer
        - -u : Transfer only added files, do not update new files
        - --existing : Transfer only updated files, not added files
        - --delete : Delete files on the client that don't exist on the server
        - -a : Archive mode. Automatically sets rlptgoD
        - -c : Check file sizes between server and client in detail
        - --stats : Report results
        - -e ssh(rsh) : Encrypt transfer
        - **-av**
          - archive & verbose

78. `Selenium`

    - Selenium is a testing framework for web applications
      - It supports various features for automated testing!
      - It supports various browsers and various test authoring languages (Java, Ruby, Groovy, Python, PHP, and Perl.)

79. `Airflow`

    - A **workflow scheduling & monitoring platform** created by AirBnB
    - Advantages of Airflow over other workflow management tools
      1. **Dynamic workflow definition**
         - Workflows are defined in Python code and can be written **dynamically**
      2. **Extensibility**
         - New operators and executors can be **easily defined** and libraries can be **extended**
      3. **Conciseness**
         - Script parameters are passed cleanly through the Jinja template engine
      4. **Availability**
         - Has a module architecture and manages tasks through a scalable **message queue** as a cluster

80. `Halyard`

    - A CLI tool for managing the **Spinnaker** deployment lifecycle
      - A tool for quickly and reliably **releasing** software **changes**
        - Can be integrated with Jenkins
      - Used for **validation** of Spinnaker-related settings, **backup** of deployed environments, and **adding/modifying settings**
    - **Halyard Flow**
      - Developer pushes source code to a remote repo  ex) Github
      - Github triggers Jenkins
      - `Jenkins **builds** a Docker image, tags it, and pushes it to `ECR`
      - When a new image is pushed to ECR, the Spinnaker **pipeline** is triggered
      - Spinnaker starts working
        1. Uses `Helm` to generate Kubernetes deployment files
        2. Deploys Kubernetes to the development environment
        3. A verification process is performed before deploying to the production environment
        4. Deploys to the production environment

81. `Cerebro`

    - Open source ElasticSearch web admin tool

82. `CMDB (Configuration Management Database)`

    - A database containing all information about hardware and software components used for IT services

83. `Polyglot Programming`

    - Freely commanding multiple development languages with different paradigms

84. `IDL (Interface Description (or Definition) Language)`

    - A specification language for describing the interface of software components
    - By expressing interfaces in a language-neutral way that is not limited to any single language, it enables communication between software components that do not use the same language
      - ex) The concept of describing interfaces without being limited between a component written in C++ and a component using Java
    - Usually used in software using **RPC (Remote Procedure Call)**
      - In this case, the computers on both sides of the RPC connection can use different operating systems and programming languages
      - IDL serves as a bridge connecting two different systems
    - **Characteristics of IDL**
      1. An interface language independent of any specific language. Therefore, it is a definition language, not an implementation language, and supports mapping to implementation languages
      2. IDL is based on object-oriented concepts and supports multiple inheritance and dynamic invocation mechanisms

85. `Backend for Frontend (BFF)`

    - Refers to an intermediate layer between the frontend of a web or mobile application and specific backend services
    - Responsible for interacting with specific backends to meet the requirements of the frontend application
    - In complex applications, the frontend often needs to interact with various backend services, and directly communicating with each backend service can increase `complexity`
      - The BFF pattern is used to solve this
    - BFF sits between the frontend and backend services, interacting with specific backend services tailored to the frontend application's requirements
      - BFF receives requests from the frontend, handles communication with the backend services needed to process those requests, and can also handle data processing/transformation, authentication and authorization, etc.
        - This can reduce dependencies between frontend and backend, improving application performance and maintainability

86. `CDC (Change Data Capture)`

    - A proven data integration pattern that tracks when and what data changes and sends notifications to other systems and services that need to respond to these changes
      - A technology that selectively captures only data that has changed since the last extraction!
    - Change data capture ensures consistency and functionality across all systems using the data
    - When performing data backup or integration, massive amounts of data must be handled, but if only recently changed data from the original source is selectively moved to another system, system load can be reduced and overall work productivity can be improved
      - Especially for data integration or data warehouse tasks that regularly extract and move large amounts of data from one system to another, using CDC technology can greatly reduce the time to extract and move data

87. `Throttling` (in FE)

    - Preventing a function from being called again until a certain amount of time has passed since the last function call
    - Widely used due to performance concerns
      - Because it has the characteristic of limiting the number of executions
    - Used when scrolling up or down
      - If a complex operation is implemented to run on scroll events, since scroll events fire frequently, delays will occur
      - In such cases, throttling can be applied to limit execution to once per certain time interval
      - ex)

        ```javascript
        let timer;
        document.querySelector('#input').addEventListener('input', function (e) {
          if (!timer) {
            timer = setTimeout(function() {
              timer = null;
              console.log('ajax request here', e.target.value);
            }, 200);
          }
        });
        ```

88. `Debouncing` (in FE)

    - Making only the last (or the very first) of consecutively called functions actually execute
    - Mainly used in AJAX search
      - When implementing instant results as the search term is typed without clicking Enter, the input event must always be listened for, which means an AJAX request fires with every character typed
      - In such cases, debouncing can be applied to send the AJAX request only when the search term is fully entered
        - A timer is set each time a key is pressed (input event fires), and if no key press occurs for a certain period, it is considered that input has ended
        - If a key press occurs within the set time, the previous timer is cancelled and a new timer is set
      - ex)

        ```javascript
        let timer;
        document.querySelector('#input').addEventListener('input', function(e) {
          if (timer) {
            clearTimeout(timer);
          }
          timer = setTimeout(function() {
            // ajax request
          }, 200);
        });
        ```

89. `Path Traversal (Directory Traversal)`

    - Description
      - One of the security vulnerabilities that occur in web applications, referring to a situation where an attacker can traverse or access the directory structure of the file system
      - In this case, the attacker can manipulate input to navigate to parent directories and access sensitive information
    - Methods of defense
      - Do not trust user input and validate it
      - Thoroughly review permissions when accessing the file system

<br>
<br>

*To be continued...*
