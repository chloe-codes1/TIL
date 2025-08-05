# Graph

<br>

<br>

### Graph

- Components
  - Vertex
  - Edge

- |v|: number of vertices, |e|: number of edges included in the graph
  - A graph with |v| vertices can have at most |v| (|v|-1) /2 edges
    - ex) A graph with 5 vertices can have at most 5*4/2 = 10 edges
- Convenient for representing elements with `N:N` relationships that are difficult to express with linear data structures or tree data structures.

<br>

<br>

### Graph Types

- Undirected Graph

- Directed Graph

- Weighted Graph

- Directed Acyclic Graph (DAG)

  - Cycle

    : Path where start vertex and end vertex are the same

    - ex)
      - Course completion (prerequisite courses)

  - Simple Path

    : Path that passes through each vertex at most once

<br>

<br>

### Adjacent Vertices

<br>

#### Adjacency

- If an edge exists between two vertices (connected), they are said to be adjacent to each other.
- Any two vertices belonging to a complete graph are all adjacent

<br>

<br>

## Graph Representation

> Method to store edge information, decided considering memory or performance

<br>

### Adjacent Matrix

> Represent the presence or absence of edges connecting two vertices as a matrix

- Store edge information using a 2D array of size |v| x |v|
- Array of arrays
- Row numbers and column numbers correspond to graph vertices
- Represent with 1 if two vertices are adjacent, 0 otherwise
- `Undirected Graph`
  - Sum of ith row = Sum of ith column = degree of Vi
- `Directed Graph`
  - Sum of row i = out-degree of Vi
  - Sum of column i = in-degree of Vi
- **Disadvantages**
  - Need to secure V*V space even with few edges (sparse graph)
  - Need V operations to find adjacent vertices even when there are few adjacent vertices

<br>

### Adjacent List

> Sequentially represent adjacent vertices for each vertex

- Store adjacent vertices for one vertex as a linked list with each vertex as a node

<br>

### Edge Array

- Store edges (start vertex, end vertex) consecutively in an array

<br>

<br>

## Graph Traversal (Search)

> Means to search all data (vertices) implemented as a non-linear structure Graph without omission

<br>

- Two methods
  - Depth First Search (DFS)
  - Breadth First Search (BFS)

<br>

<br>

## DFS (Depth First Search)

- From the starting vertex, explore deeply in one direction as far as possible, and when there's nowhere else to go,

  return to the vertex with the last encountered branching edge and continue searching in other directions,

  eventually visiting all vertices through this traversal method

- Since you need to return to the last encountered branching vertex and repeat DFS, use **Last In First Out (LIFO)** structure `Stack`

<br>

### Stack

- A data structure that stacks data like stacking objects
- Linear structure
  - Data relationships have 1:1 relationships
    - Non-linear structure has 1:N relationships (trees)
- Remove the last inserted data first
  - Last In First Out (LIFO)

<br>

<br>

## BFS (Breadth First Search)

- A method of first visiting all adjacent vertices of the search starting point in order, then starting from the visited vertices and visiting adjacent vertices in order again
- Since you need to search adjacent vertices first and then proceed with BFS in order, use `Queue` which is a **First In First Out (FIFO)** data structure

<br>

### Queue

- Like Stack, a data structure with restricted insertion and deletion positions
  - Structure where only insertion occurs at the back of Queue and only deletion occurs at the front
- Elements are stored in the order they are inserted into Queue, so the first inserted element is deleted first
  - First In First Out (FIFO)
- Basic operations
  - Insertion
    - `enQueue`
  - Deletion
    - `deQueue`
- Empty state and full state check: `isEmpty()`, `isFull()`
  - Empty state
    - front = rear
  - Full state
    - rear = n-1 (n: array size, n-1: last index of array)

<br>

<br>

## Disjoint-sets

- Disjoint or mutually exclusive sets are sets that do not contain overlapping elements
  - No intersection!
- Distinguish each set through one specific member belonging to the set
  - This is called `representative`!
- Methods to represent disjoint sets
  - Linked list
  - Tree
- Disjoint set operations
  - `Make-Set(x)`
    - Create a set with element x as the only element
  - `Find-Set(x)`
    - Return the representative of the set containing x
  - `Union(x,y)`
    - Merge the set containing x and the set containing y

<br>

### Disjoint Set Representation - `Linked List`

- Elements of the same set are managed as one linked list
- The front element of the linked list is the representative element of the set
- Each element has a link pointing to the representative element of the set

<br>

### Disjoint Set Representation - `Tree`

- Represent one set (a disjoint set) as one tree
- Child nodes point to parent nodes, and the root node becomes the representative

<br> 
