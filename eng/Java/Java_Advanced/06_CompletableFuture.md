# CompletableFuture

<br>

### What is CompletableFuture?

- Supports asynchronous programming in Java
- A class that implements Future and CompletionStage
  - What is `Future`?
    - A class that represents the result of an asynchronous operation
      - It allows you to know the result of a scheduled task
    - It can pass processed data to another thread in a multi-thread environment
    - Since it is implemented as `Thread-Safe` internally, there is no need to use `synchronized blocks`
- It makes the following tasks, which were difficult with Future, much easier
  - A Future cannot be completed externally
    - You cannot cancel it or set a timeout on get()
  - Without using blocking code (get()), you cannot execute a callback when the task finishes
    - Any work that creates a result value through a Future and does something with it must come after get()
  - Multiple Futures cannot be combined
    - ex) Fetching event information and then fetching the list of members who participated in the event
  - It does not provide an API for exception handling
