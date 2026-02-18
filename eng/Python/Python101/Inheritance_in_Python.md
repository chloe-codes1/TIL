# Inheritance in Python

<br>

### How Methods Are Executed When a Class Is Inherited

- Assuming an instance's method is to be executed, the bound method is retrieved via `__getattribute__()` and then the method is executed
- The order in which methods are retrieved follows the `__mro__`
  - MRO (method resolution order) is the order in which methods are looked up
  - Whether it's single inheritance or multiple inheritance, the order in which methods are accessed is stored in that class's `__mro__`, with items further to the left having higher priority
