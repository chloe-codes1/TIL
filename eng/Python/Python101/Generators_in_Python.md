# Generators in Python

> References: [Python Wiki](https://wiki.python.org/moin/Generators), [WikiDocs](https://wikidocs.net/16069), [Book] Effective Python

<br>

<br>

## What is Generator in Python?

<br>

### 1. What is a Generator?

> A construct used to create iterators directly
>
> If a function contains the `yield` keyword, that function becomes a Generator

- A type of iterator returned when a `generator function` is called
- A generator function looks similar to a regular function, but uses `yield statements` to `return data at a desired point and resume processing`
- While a regular function has a single entry point, a generator can be thought of as having multiple entry points
  - Using generators allows you to receive desired data at desired points in time

- An **Iterator** requires implementing `__iter__`, `__next__`, or `__getitem__` methods in a class, but
  - A **Generator** only requires using the `yield` keyword inside a function
- Generators can be written much more simply than Iterators
- Generators are sometimes called "producers"
- Calling a Generator function returns a Generator object

  ex)

  ```python
  def generator_example():
      print('Print 1')
      print('Print 2')
      yield

  g = generator_example()
  print(g)
  next(g)
  ```

  > Result

  ![image-20200726165007727](../../kor/images/image-20200726165007727.png)

- When `yield` is used inside a function, the function becomes a Generator, and a value (variable) is specified with `yield`

  ex)

  ```python
  def number_generator():
      yield 0
      yield 1
      yield 2

  for number in number_generator():
      print(number)
  ```

  > Result

  ![image-20200726162511720](../../kor/images/image-20200726162511720.png)

<br>

- Iterators can be simply implemented using just `yield` in a function
- While an Iterator directly returns values via return in the `__next__` method,
  - In a Generator, the value specified with `yield` becomes the return value of the `__next__` method
- While an Iterator explicitly raises a **StopIteration** exception using raise,
  - A Generator automatically raises a **StopIteration** exception when the end of the function is reached
- Each time the built-in `__next__` method is called on a generator object, the `yield` code inside the function is executed, producing a value at yield
  - That's why it's called a Generator!

- The value passed to `yield` in a **generator** is returned to the calling side of the **iterator**
  - The **iterator** returned from a Generator is a set of values passed to the `yield` expressions inside the generator function
- A **Generator** can pass values outside the function using `yield` without ending the function
  - **return** ends the function immediately upon returning,
  - **yield** temporarily **yields** control so that code outside the function can execute and take the value, then resumes executing the code inside the Generator

<br>

### 2. How Generators Work

1. When a generator function containing a yield statement is executed, a generator object is returned, but the function's content is not executed at this point.
2. The generator can be executed through the built-in method `next()`, which internally takes an iterator as an argument and calls the iterator's `__next__()` method.
3. When `__next__()` is called for the first time, the function's content is executed until it encounters a yield statement, at which point processing is suspended.
4. At this time, all local state is preserved, including variable states, instruction pointers, internal stack, and exception handling state.
5. Control is then yielded to the upper context, and when `__next__()` is called again, the generator resumes from the point where it was suspended.

<br>

### 3. Advantages of Generators

- Using generators is clearer to understand than returning a list of accumulated results
- Since generators don't store all inputs and outputs in memory, they can produce **continuous output** even when **the amount of input is hard to determine**
- Using generators, only the values needed at that moment are received through yield, so there is no need to keep all values in memory

<br>

### 4. Disadvantages of Generators

- However, since generators produce values on demand and don't remember them, while `list a` can be used multiple times, `generator b` is exhausted after a single use
- This is true for all iterators - Lists and Sets are iterable but are not iterators, so they are not exhausted
