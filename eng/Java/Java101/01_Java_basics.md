# Java Basics & Environment Setting

<br/>

### Features of Java

- `Simple`

  > Simpler than C++ -> but slower
  - Java's concise yet clear object-oriented design has allowed users to understand and utilize object-oriented concepts more easily, greatly contributing to the widespread adoption of object-oriented programming.

- `Object-Oriented`

  - It is one of the **object-oriented programming languages**, and it is a language that well applies the characteristics of object-oriented concepts: **inheritance**, **encapsulation**, and **polymorphism**.

- `Memory`

  > Garbage Collection => GC handles memory management!
  - When a program written in Java is executed, the **Garbage Collector** automatically manages memory, so the programmer does not need to manage memory separately.
    - Without a Garbage Collector, the programmer would have to manually check and release unused memory.
    - Although automatic memory management can be somewhat inefficient, it helps the programmer focus more on programming.

- `Robust` (==sturdy)

  - Whether this code will run safely without touching the System.

- `Platform Independent`

  > Independent of the operating system (JVM)
  >
  > -> The **Java Virtual Machine** operates on top of the OS
  - With conventional languages, significant effort was required to adapt a program developed for one OS to another, but with Java, such effort is no longer necessary.
    - This is made possible through a kind of emulator called the **Java Virtual Machine (JVM)**:
      - Java applications communicate only with the **JVM**, not with the OS or hardware,
      - and the **JVM** **translates** the commands received from Java applications so that the corresponding OS can understand them.
  - Although programs written in Java are OS-independent, the **JVM** itself is OS-dependent, so Sun provides different versions of the **JVM** that can be installed on various operating systems.
    - Therefore, programs written in Java can run regardless of the OS and hardware, which is also expressed as "`Write once, run anywhere`".

- `Multi-Threaded`

  > In Java, multi-threading is implemented at the programming language level without the help of the OS
  - In general, multi-thread support varies in implementation and handling depending on the OS being used.
  - However, **multi-thread** programs developed in Java can be implemented regardless of the system, and related libraries (**Java API**) are provided, making implementation easy.
  - **Scheduling** of multiple threads is handled by the **Java interpreter**.

- `Secured`

  : Java is pretty much "safe" unleses a third party is trying to exploit the JVM

- `Dynamic`

  > Supports Dynamic Loading
  - Typically, applications written in Java consist of multiple classes.
  - Since Java supports **dynamic loading**, not all classes are loaded at execution time; instead, classes can be loaded and used at the point when they are needed.
  - Even if some classes are modified, the entire application does not need to be recompiled, and even when changes occur in the application, a **flexible application** can be written with relatively little work.

<br>

<br>

### API (Application Programing Interface)

: Commands provided by Java to control the Java System

 ex) java. (= initial version -> core API), javaX. (extension API), etc.

- a list of all classes that are part of the Java development kit (JDK). It includes all Java packages, classes, and interfaces, along with their methods, fields, and constructors

<br>

<br>

### JVM (Java Virtual Machine)

> Java provides a JVM for each operating system
>
> => All compiled Java programs can be used anywhere without modification through the JVM!

#### JVM and Speed

- While the code of a typical application passes through only the `OS` before being delivered to the hardware,
  - Java applications pass through the `JVM` one more time, and since they are not fully compiled for the hardware but are **interpreted at runtime**, they have the disadvantage of being **slower**.
- However, nowadays the `JIT compiler`, which directly converts bytecode (compiled Java code) to the machine language of the hardware, along with improved optimization techniques, has significantly narrowed the speed gap.

<br>

#### Two Functions of the JVM

1. to allow Java programs to run on any device or operating system
2. to manage and optimize program memory

<br>
<br>

### Lambda Expression

: Expressing a method as a single 'expression'.

  -> Since expressing a method as a lambda expression removes the method's name and return value, lambda expressions are also called 'anonymous functions'.

<br>
<br>

### Java Platforms

1. `J2SE`  -> General desktop PCs

​              (The standard environment for JAVA programming)

2. `J2EE`  -> Server computers

   (Supports distributed environments / Very difficult, and the server environment required to run it is expensive)

3. `J2ME`  -> Small devices ex) mobile phones, PDAs, set-top boxes

<br>

-> (more info from Google)

#### **JAVA SE (Java Platform Standard Edition)**

A standard Java platform for desktops, servers, and embedded systems. It includes the Java Virtual Machine specification and API set. JAVA EE and ME are configured by selecting parts of SE or adding APIs depending on the purpose. SE is the most commonly used. Since it includes JDBC and all basic features, SE is mainly used for Android development.

#### **JAVA EE (Java Platform EnterPrise Edition)**

A platform for server-side development using Java. It is a server platform that adds Java features for providing distributed multimedia running on web application servers to the existing SE. Since server-side features were added to JAVA SE, it includes all SE features.

#### **JAVA ME (Java Platform Micro Edition)**

As the name suggests, this is a Java platform for embedded systems. It stands for Java Platform, Micro Edition. Also called Java ME or J2ME, it is a platform created to support the Java programming language on devices with limited resources such as mobile phones, PDAs, and set-top boxes.

<br>
<br>

### Setting Up the Java Development Environment

<br>

#### Configuring Environment Variables

<br>

`JAVA_HOME`

`Path`               -> Path to find executable files

​                           => Only indicates the location of executable programs

`Classpath`    -> Path to find classes

​                            => Indicates the location of libraries used by executable programs

  => If you enter .; in the Classpath variable value, it means to search based on the current location!

<br>
<br>

*Java is all about designing Classes!*

*Java is case-sensitive!*

<br>

#### `public` keyword

```java
public Class  [class name] { }
```

-> Adding Public means anyone can use it

<br>
<br>

#### Main Method

``` java
public static void main(String[] args) {}
```

 => Main function

 -> It becomes the entry point (=start point) that starts the Java Application

 -> Parentheses ( ) always follow after a method name => if there are parentheses, it's a function; if not, it's a variable!

- `static` keyword: A keyword that loads the method into memory just by declaring it, without the need for the new keyword

- `String`: data type -> it is a string

- `args`: local variable (variable name)

- `void`: means there is no return value at the calling position -> it means this statement just executes!

<br>
<br>

### Access Modifiers

  `public` : allows all access
  `protected` : allows access to the same package and subclasses
  `default` : allows access within the same package
  `private` : allows access only within the current object

<br><br>

### Delimiter

- Names that distinguish class, variable, and method

- Must not be duplicated

- First character can be a letter, _, or $

- `Keywords` cannot be used

  ex) class, import, new, public, void, etc.

### Two Things That Can Go Inside a Class

1. Data (= Variable)

   : Nouns are Data!

2. Functionality (= Method / Function)

   : Verbs are methods!     => If it makes sense to add "to do" to it, it's a verb...

    -> In other languages, it's called a Function!

<br>
<br>

### CLI vs GUI

<br>

#### CLI(Command Line Interface)

: A method where the computer and user exchange commands through text (an environment where processing is done through commands)

 ex) dos

- A user interface where displayed content and input content are character-based

- Compared to GUI, which displays with icons and accepts input through pointer devices like a mouse, it consumes fewer resources (software size, RAM capacity, CPU performance)

- How it works

  : It starts from main and executes sequentially in order

<br>

#### GUI (Graphical User Interface)

: A method of making the computer work by pressing buttons on a graphical screen

- An environment where icons are double-clicked instead of commands

- Working in a graphical environment

- How it works

  : It waits until the user presses a button or issues a command

 and then processes the corresponding task when a command is received

<br>
<br>

### Cmd (Command Prompt)

 : Command Prompt
      -> CLI(Command Line Interface): only operates when commands are entered

<br>
<br>

#### Compile Command

: `javac` in the cmd window

 (For this command to execute properly, environment variables must be configured)

<br>

ex 1)

```powershell
*javac = java compile command

E: -> go to E drive

E:\data>javac -d        -> compiles the created source file into a language the computer can understand
 => Javac -> Compile! command
 => -d  -> compile based on package structure


E:\data>javac -d . Sample.java    => Compile the Sample.java file!

E:\data>dir             -> view files in the directory

E:\data directory

E:\data>java Sample

Hello World!


```

 ex 2)

``` powershell
E:\data>javac -d . Sample.java

E:\data>javac -d ./bin  Sample.java  -> placed in the bin folder for separate management

E:\data>cd bin   -> cd: shows or changes the current directory name

E:\data\bin>java Sample  -> write the class name that has the main method

​                                           => But!! If there is no main function in that class, an error occurs!



(If an error occurs, this is displayed)

E:\data\bin>java Sample

Error: Main method not found in class Sample, please define the main method as:

  public static void main(String[] args)

or a JavaFX application class must extend javafx.application.Application.

```

=> That's why! To run a `Java App`, you need the `Main Method`!!!!!

<br>
<br>

  \* . : current directory

  \* .. : parent directory

<br>
<br>

#### Determining the Encoding Type

**`UTF-8`** -> An encoding type that can encompass all languages worldwide

 : In Eclipse window - preference-general-appearance-workspace

<br>
<br>

#### Changing Perspective

Hover the mouse on the right side of the Eclipse window

It shows JAVA EE (Enterprise Edition) -> This is server-side (too much for us)

 -> You can change to Java in the open perspective next to it

<br>
<br>

#### Creating a Project

Eclipse requires creating a project first

File - new - java project

<br>
<br>

### Java Source Code and Class Code Are Managed Separately

  However! Eclipse automatically compiles and saves to the bin folder

<br>

- Src is where the source is saved

- Bin is where the compiled source is saved -> bytecode files are saved here

<br>

#### Moving or Renaming a Project, Package, or Class

: Right-click -> refactor -> move or rename

<br>

#### Checking Source Code

1. Go to JRE System Library - rt.jar - Java.util - Date.class, or

2. In the Eclipse window, place the mouse over a class (ex. Date class) and Ctrl + click - attach source to view the source code

<br>
<br>

#### Class

- System Class
- Date Class
- String Class
