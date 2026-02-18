# @property in Python

> References: [Book] Effective Python - <sub>by Brett Slatkin</sub>

<br>

## Access Modifier

<br>

- Python does not have keyword access modifiers such as `private`, `public`, `protected`, or `default`; instead, access is controlled through naming conventions.

- Since all variables and methods declared in Python are `public`, there are no `getter` or `setter` methods!

  - This was a new characteristic of Python for me, as my first language was Java!

  <br>

  | public             | protected               | private                  |
| ------------------ | ----------------------- | ------------------------ |
  | No underscore prefix | Single underscore prefix (_) | Double underscore prefix (__) |

   ex)

  ```python
  class AcessModifiers:

      def __init__(self):
          pass

      def public(self):
          print('Public called!')

      def _protected(self):
          print('Protected called~~')

      def __private(self):
          print('Private called!!!')
  ```

<br>

<br>

## Getters and Setters in Python

<br>

### 1. Creating Get and Set Methods Manually

> Manual implementation

ex)

```python
class Student:
    def __init__(self):
        self.__name = 'chloe'

    def get_name(self):
        return self.__name

    def set_name(self):
        return self.__name = name
```

- Simple, but not Pythonic!

<br>

<br>

### 2. Using `@property` and `@__.setter` Decorators

> More intuitive than manual implementation!

<br>

### What is the property class?

- A class that creates special descriptor objects

  - It has `getter`, `setter`, and `deleter` methods internally

    ex)

    ```python
    p = property()

    print(p)
    print(p.getter)
    print(p.setter)
    print(p.deleter)
    ```

    > Execution result

    ![image-20200726133346788](../../kor/images/image-20200726133346788.png)

<br>

#### Using the property decorator

- To restrict variable access of an Instance object through methods, you need to **wrap** the Instance object's variable with a **property object**

<br>

ex)

```python
class Student:
    def __init__(self):
        self.__name = 'chloe'

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, name):
        return self.__name = name
```

<br>

#### `@property`

- Acts as the getter
- When the `@property` decorator is placed above a method, an instance with that method name is created internally, and the method is registered as the **getter**

<br>

#### `@[getter_method_name].setter`

- Acts as the setter

<br>

#### @property must be above the setter

- If there is only @method_name.setter without `@property`, an error will occur
- However, it is possible to use only `@property` without a setter to declare just a getter
  - This makes the private data **read-only**

<br>

<br>

### 3. Why Use the `@property` Decorator

> I keep thinking about how I couldn't answer this properly, so I'm reorganizing it again... I wish I could turn back time

1. Used to prevent users from directly accessing attributes
   - Used for `Encapsulation`
     - When defining a Class, you can bundle internal attributes and methods into a single unit, and creating a class by bundling them into a single unit is called `Encapsulation`
     - It is meant to **protect** variables used inside a Class instance
       - Why?
         - If variables can be freely manipulated from outside, there is a high chance that the class won't work according to its intended logic and errors will occur
         - That's why in OOP, Encapsulation is used to distinguish between variables used internally and externally in functions!
2. When special behavior needs to occur when setting attributes later

3. Used to make parent class attributes immutable

    ex)

   ```python
   class FixedResistance(Resistor):
       # ...
       @property
       def data(self):
           return self.__data

       @data.setter
       def data(self, data):
           if hasattr(self, '__data'):
               raise AttributeError('You are not allowed to set attribute!')
           self.__data = data
   ```

   - You can verify that an error occurs when trying to assign to the property after creating the above object

<br>

<br>

### 4. Better way to use `@property`

- When implementing getters and setters with @property methods, be careful not to cause unexpected behavior
  - Do not set other attributes in the getter @property method
    - Only modify the state of related objects in the **@property.setter** method!

- **Reusability** is the biggest problem with Python's built-in @property

  - Methods decorated with @property cannot be used across multiple attributes within the same class

    `+` They also cannot be reused in unrelated classes

  - Therefore, for **reusable** @property methods, it is better to use the **descriptor protocol**

<br>

`+`

#### Descriptor Protocol

- **Descriptor classes** can provide `__get__` and `__set__` methods that allow method reuse without repetitive code
- The same logic can be reused across many different attributes of a single class
