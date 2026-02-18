# TreeSet, TreeMap vs HashSet, HashMap
>
> Which data structure should be used in which situation!

<br>

### TL;DR

- Unless there is a special reason, use `HashMap` which has good `search performance`
- If you want to `guarantee order`, use LinkedHashMap
- If you want to `iterate` over key values in a consistent manner, use `TreeMap`

<br>

### Differences Between TreeMap and HashMap

- TreeMap is a data structure similar to HashMap, but the difference is that TreeMap's data is sorted
- Since HashMap's data is not sorted, it may be slower than TreeMap for data searching
- However, HashMap uses less memory than TreeMap

<br>

### Order Guarantee Aspect

- `HashMap` does not guarantee order
  - `LinkedHashMap` guarantees the order of insertion!
- `TreeMap` guarantees order using the comparison operation of the class used as the Key value
  - It automatically `sorts` based on the key value

<br>

### Speed Aspect

- The time complexity of `HashMap` is `O(1)`
  - Because it uses `hash values`
- The time complexity of `TreeMap` is `O(log n)`
  - In return, you can get a `sorted order`

<br>

### Whether `null` is Allowed as a Key

- `HashMap` `allows` null as a key
- `TreeMap` does `not allow` null as a key

<br>

### When to Use TreeMap?

- When you need to store and search ordered data
  - It has synchronization handling, making it `Thread-safe`
- When you need to search data in sorted order
- When insertion, deletion, and search operations on data are frequently performed

<br>

### Cases Where TreeMap is Not Efficient

- When the data size is very large
- When insertion, deletion, and search operations on data are not frequently performed
