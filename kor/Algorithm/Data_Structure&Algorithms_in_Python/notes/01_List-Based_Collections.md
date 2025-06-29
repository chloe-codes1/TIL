# 01. List-Based Collections

<br/>

<br/>

## 1-1 Linked Lists

- stores a reference to the next element in the list
- next component is storing the memory address of the next element

<br/>

### Linked List & Array

Main distinction?

: each element stores different information

<br/>

<br/>

### Pros & Cons

- Pros

  : pretty easy to insert & delete elements

- Cons

  : need to be careful not to lose references when adding or removing elements

<br/>

### Linked List in Python

> There isn't a built-in data structure in Python that books like a linked list.
>
> But, it's easy to make classes that represent data structures in Python!

<br/>

ex) Linked List

```python
# single unit in a linked list example

class Element(object):
    def __init__(self, value):
        self.value = value
        self.next = None
        
    
    
# LinkedList example

class LinkedList(object):
    def __init__(self, head=None):
        self.head = head
        # The head of the list refers to the first node of the list!
        
    def append(self, new_element):
        current = self.head
        if self.head:
            while current.next:
                current = current.next
            current.next = new_element
        else:
            self.head = new_element

            
            
    # assume the first position is 1        
            
    # returns the element at a certian position        
    def get_position(self, position):
        counter = 1
        current = self.head
        if position < 1:
            return None
        while current and counter <= position:
            if counter == position:
                return current
            current = current.next
            counter += 1
        return None

    # add an element to a particular spot in the list
    def insert(self, new_element, position):
        counter = 1
        current = self.head
        if position > 1:
            while current and counter < position:
                if counter == position - 1:
                    new_element.next = current.next
                    current.next = new_element
                current = current.next
                counter += 1
        elif position == 1:
            new_element.next = self.head
            self.head = new_element
            
 # delete the first element with that particular value
    def delete(self, value):
        current = self.head
        previous = None
        while current.value != value and current.next:
            previous = current
            current = current.next
        if current.value == value:
            if previous:
                previous.next = current.next
            else:
                self.head = current.next
```

<br/>

<br/>

## Stack

: List-based data structure

​ -> has a bit of a different flair than arrays & linked lists

<br/>

#### How it works?

- You keep putting elements on top
- You have easy access to remove or look at the top element

<br/>

#### When to use?

- when you only care about the most recent elements
- the order in which you see & save elements actually matters

<br/>

#### Push & Pop

1. Push

   : when you add an element to a stack

      -> O(1)

2. Pop

   : when you taken an element off of the stack

      -> O(1)

​                => All you need here is to look at the top element of the stack!

<br/>

#### Stack == L.I.F.O

: Last In First Out Structure

<br/>

#### Stack in Python

- `pop()` is a given function
- `append()` is equivalent to a push function

<br/>

<br/>

Make your own code instead of using `append()` since it traverses the whole list, taking O(n)

  -> it will take a lot faster if we push/pop from the first element in a linked list!

<br/>

ex)

``` python
class Element(object):
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList(object):
    def __init__(self, head=None):
        self.head = head
    
    def append(self, new_element):
        current = self.head
        if self.head:
            while current.next:
                current = current.next
            current.next = new_element
        else:
            self.head = new_element
    
    # Insert new element as the head of the LinkedList
    def insert_first(self, new_element):
         new_element.next = self.head
         self.head = new_element
    
    # Delte the fist (head) element in the LinkedList as return it
    def delete_first(self):
        if self.head:
            deleted_element = self.head
            temp = deleted_element.next
            self.head = temp
            return deleted_element
        else:
            return None
    
    
class Stack(object):
    def __init__(self, top=None):
        self.ll = LinkedList(top)
    
    def push(self, new_element):
        self.ll.insert_first(new_element)
    
    def pop(self):
        return self.ll.delete_first()
            
```

<br/>

`+` alternative `delete_first()` method

ex)

```python
def delete_first(self):
    deleted = self.head
    if self.head:
        self.head = self.head.next
        deleted.next = None
    return deleted
```

<br/><br/>

## Queues

#### Queues == F.I.F.O

: First In First Out Structure

<br/>

#### Head & Tail

1. Head

   : the first (the oldest) element in the queue

2. Tail

   : the last element (the newest) in element in the queue

<br/>

#### Enqueue & Dequeue

1. Enqueue

   : add an element to the tail

2. Dequeue

   : remove the head element

3. Peek

   : look at the head element, but not removing it

<br/><br/>

### Deque

: a queue that goes both ways

   -> you can enqueue & dequeue from either end

   -> kind of a generalized version of both stacks & queues since you could represent either of them with it!

<br/>

### Priority Queue

- assign each element a numerical priority when you insert it into the queue

- remove the element with the highest priority when you dequeue

  -> if the elements have the same priority, the oldest element is the one that gets dequeue first

<br/>

### Queues in Python

ex)

```python
class Queue:
    def __init__(self, head=None):
        self.storage = [head]

    def enqueue(self, new_element):
        self.storage.append(new_element)

    def peek(self):
        return self.storage[0]

    def dequeue(self):
        self.storage.pop(0)
```
