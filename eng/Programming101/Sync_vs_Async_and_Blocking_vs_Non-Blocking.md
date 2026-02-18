# Sync vs Async and Blocking vs Non-Blocking

> Let's clarify these confusing concepts!

<br>

![image-20200827161039232](../kor/images/image-20200827161039232.png)

<br>

## Block vs Non-Block

: How to handle targets that cannot be controlled

<br>

### What is Block?

- The called function holds the `control` and returns it together with the **result value** when **returning**



<br>

<br>

## Sync vs Async

: Synchronous vs Asynchronous (abstract)

<br>

### What is Synchronous?

- Syn (together) + Chrono (time)
  - *Are the times of the targets aligned?*
    - Aligning the time
  - When the time of **returning** `control` and the time of **delivering** the `result value` are the same
    - Synchronous!

<br>

### What is Asynchronous?

- Not aligning the time

<br>

<br>

## `Block & Non-Block`  vs  `Sync & Async`

<br>

### Block & Non-Block

- About `control`
- *How do you handle targets that cannot be controlled?*

<br>

### Sync & Async

- About the **time** (**timing**) of **returning** `control`

- *Are the times of the targets aligned?*



<br>
