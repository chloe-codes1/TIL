# JavaScript Object

<br>

<br>

#### Terms

- `Constructor function`

  : A JavaScript function that creates an object through the new operator and creates and initializes properties and methods

- `Prototype`

  - A property of the constructor function
  - The place where properties and methods that are identically inherited by objects created by the constructor function are defined

- `Private member`

  : A property or method that cannot be modified from outside the object

<br>

<br>

### JavaScript Object

- All data types except Primitive data types are Objects

  - `Primitive Types`

    - **number**

    - **string**

    - **boolean**

    - **null**

      : no value

    - **undefined**

      : a declared variable, but hasn't been given a value

    - **symbol**

      : a unique value that's not equal to any other value

- Functions are also objects

<br>

<br>

### Object Creation

<br>

#### Object

: A collection of properties

<br>

#### Object Creation

- When using an object literal, the object is created by listing its properties

- Empty object

  : Used because properties can be easily added when creating functions with the literal method

- `namespace`

  : Minimizes the use of global variables by converting variables and functions into object properties

- Objects are created using the new operator and constructor functions

<br>

#### Constructor Functions and prototype

- `this`

  : Used in methods and refers to the calling object that invoked the method

- `Constructor function`

  - A function that defines what properties an object to be created will have and how those properties will be initialized
  - Similar to classes in typical object-oriented languages

- `prototype`

  - Means that the properties of an object are not copied to the created object but are referenced
  - If the prototype object of the constructor function is modified, the properties of objects created by this constructor function are changed!

  <br>
