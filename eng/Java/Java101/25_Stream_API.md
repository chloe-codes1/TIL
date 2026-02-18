# Stream API

<br>

### What is the Stream API?

- It abstracts data to provide a common way to read and write data stored in various ways
  - Using the Stream API, not only arrays and Collections but also data stored in files can all be handled in the same way
- It is a feature that allows stored elements of arrays, lists, and other collections to be referenced one by one and processed with lambda expressions
- It is needed when implementing sorting, filtering, duplicate removal, etc. of data within a Collection

<br>

### Characteristics of Streams

- Unlike collections that operate through external iteration, Streams operate through `internal iteration`
- Streams are `single-use`
  - Unlike Collections which are reusable, once a Stream is used it is closed and cannot be reused
  - If needed, sorted results can be stored in a Collection or array and returned
- Streams `do not modify the original data`
  - Streams only read data from the original data and do not modify the original data itself
- Stream operations use `filter-map` based APIs to optimize performance through `lazy evaluation`
- Streams support `easy parallel processing` through the `parallelStream()` method
- Streams process work through internal iteration
  - One of the reasons Stream-based work can be concise is internal iteration
  - Internal iteration means that loops can be hidden inside methods
    - Loops are not exposed in the code

<br>

### Stream API Operation Flow

1. Creation of the Stream
2. Intermediate operations of the Stream (transformation of the Stream)
3. Terminal operations of the Stream (consumption of the Stream)
