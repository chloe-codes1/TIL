# Collection

<br>

## What is a Collection?

- Various implementations exist based on the `List`, `Map`, and `Set` interfaces
- `Reasons for use`
  - Because `standardized classes` are provided for handling large amounts of data, you can use them conveniently without directly implementing DataStructures
  - Unlike arrays, `you don't need to pre-define the space for storing objects`, so the `number of objects can be determined dynamically` based on the situation
    - This also improves the spatial efficiency of the program

<br>

## Types of Collections

### List

- The `List` interface can be directly defined and used by the user through `@Override`, and the representative implementation is `ArrayList`.
  - This is an improvement of the existing `Vector`
- `LinkedList`
  - A data structure that stores data in a manner where each node has data and a pointer, connected in a single line
  - Nodes containing data are connected, and the node's pointer is responsible for the connection to the next or previous node
  - `Advantages`
    - Adding/removing data at the middle of the lined-up nodes is possible in `O(1)` time
  - `Disadvantages`
    - Unlike arrays or tree structures, searching for data at a specific position takes `O(n)` time

<br>

### Map

- The representative implementation is `HashMap`
- It has a `key-value` structure, and the specific details about Map are consistent with the `hashtable` in the DataStructure section
- `Duplicate values are not stored` based on the key, and `order is not guaranteed`
- To guarantee order for keys, use `LinkedHashMap`

<br>

### Set

- The representative implementation is `HashSet`.
- Duplicate values for `value` are not stored
- In fact, the Set data structure is simply a data structure where the value is used as the key, replacing the key in the Map's key-value structure
- Likewise, order is not guaranteed, and `LinkedHashSet` is used to guarantee order
