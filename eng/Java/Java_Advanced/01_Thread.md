# Java Thread

<br><br>

### Concurrency

<br>

- Concurrency
  - Logical
  - Single Core / Multi Core
- Parallel
  - Physical
  - Multi Core

<br>

*Since Java runs on the **JVM (Java Virtual Machine)**, you don't need to worry about the physical aspects!*

<br>

<br>

### What is a Java Thread?

<br>

- `Process`

  : A program that operates independently (Eclipse, Messenger, etc)

- `Thread`

  : A small unit of execution that constitutes a Process (Messenger = chat + file transfer)

- `Multi-process`

  : Running multiple processes simultaneously

- `Multi-thread`

  : Multiple threads operating simultaneously within a single process

<br>

<br>

### Creating a Java Thread

<br>

#### Method 1) Implementing the Runnable interface

- Runnable interface

  ex)

  ```java
  package virus;

  public class CoronaRunnable implements Runnable{

  	int num;
  	public CoronaRunnable() {}
  	public CoronaRunnable(int num) {
  		this.num = num;
  	}
  	@Override
  	public void run() {
  		for (int i =0 ; i< 10000 ; i++) {
  			int j = i*100;
  		}
  		System.out.println(num);
  	}
  }
  ```

  <br>

- Test

  ```java
  package app;

  import virus.CoronaRunnable;

  public class CoronaThreadTest {
  	public static void main(String[] args) {
  		for (int i = 0 ; i <1000 ; i++) {
  			CoronaRunnable cr = new CoronaRunnable(i);
  			Thread t = new Thread(cr);
  			// Start the Thread
  			t.start();
  		}
  	}
  }
  ```

<br>

#### Method 2) Extending the Thread class

- Thread class

  ex)

  ```java
package virus;

  public class CoronaThread extends Thread{
  	int num;

  	public CoronaThread() {}
  	public CoronaThread(int num) {
  		this.num = num;
  	}

  	@Override
  	public void run() {
  		for (int i = 0 ; i < 10000 ; i++) {
  			int j = i*100;
  		}
  		System.out.println(num);
  	}
  }
  ```

  <br>

- Test

  ```java
  import virus.CoronaRunnable;
  import virus.CoronaThread;

  public class CoronaThreadTest {
  	public static void main(String[] args) {
  		for (int i = 0 ; i <1000 ; i++) {
  			CoronaThread ct = new CoronaThread(i);
  			ct.start();
  		}
  	}
  }
  ```

  <br>

  <br>

  ### Memory Structure When Running a Thread

  ![](../../kor/images/thread.jpg)

<br>

<br>
