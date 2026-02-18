# Synchronous vs Asynchronous

> The difference between synchronous and asynchronous
>
>
> -> From the perspective of order and result (processing)
>

<br>

### Synchronous

- After making a request, it `waits for the result before processing`, waiting for the `readiness` of the I/O operation
  - The focus is on whether the preparation for a specific I/O operation is ready

<br>

### Asynchronous

- `Makes a request and continues with other work`, and when the task is completed, it receives a notification of completion and processes the corresponding work
- It is performed through asynchronous APIs at the operating system level, and when the I/O operation is completed, processing is done using an appropriate handler

<br>

### Synchronous vs Asynchronous

- If it `waits` for the system call to complete, it is synchronous
- If it `does not wait` for the system call to complete, it is asynchronous
