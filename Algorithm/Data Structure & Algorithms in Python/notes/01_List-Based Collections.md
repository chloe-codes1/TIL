# 01. List-Based Collections



## 1-1 Linked Lists in Depth





### Linked List & Array



Main distinction?

: each element stores different information



#### I. Linked List

- stores a reference to the next element in the list

- next component is storing the memory address of the next element

- Pros

  - pretty easy to insert & delete elements

    -> but, need to be careful not to lose references when adding or removing elements



<br/>



#### Linked List in Python

There isn't a built-in data structure in Python that books like a linked list.

But, it's easy to make classes that represent data structures in Python!



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

​	-> has a bit of a different flair than arrays & linked lists

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



​    => All you need here is to look at the top element of the stack!





#### L.I.F.O

: Last In First Out





#### Stack in Python

- `pop()` is a given function
- `append()` is equivalent to a push function













ex) alternative delete_first method 

```python
def delete_first(self):
    deleted = self.head
    if self.head:
        self.head = slef.head.next
        deleted.next = None
    return deleted
```

