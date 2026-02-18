# JavaScript Basics

<br>

<br>

### Functions of JavaScript

- HTML & CSS
  - Define the structure and appearance of Web documents
- JavaScript
  - Defines the **functionality** of documents

<br>

#### ES2015 (ES6)

- Having solved many of JavaScript's chronic problems in ES2015, the standard has now been published up to ES2019

<br>

#### Vanilla JS (Pure JavaScript)

- Many libraries emerged for cross-browsing and convenient usage (most notably jQuery)
- Recent standardized browsers and the emergence of various tools after ES6 have increased the use of pure JavaScript

<br>

#### What Browsers Can Do

- Global object window
  - DOM manipulation
  - BOM manipulation

<br>

*Node.js based on the V8 engine*

<br>

### Characteristics of JavaScript

<br>

1. #### It is a Script Language

   - Executed directly through an Interpreter
   - Easy Data type and type casting
   - Slower speed
   - Limited by the execution environment
     - Only works in programs that have a JavaScript Interpreter installed

<br>

2. #### It is a Functional Language

   - A method based on functions
   - Declarative programming
     - Can dynamically process HTML elements
   - First-class functions
     - Functions themselves can be used like data
   - Variable scope == Function scope

<br>

3. It is a completely different programming language from Java
   - Netscape licensed the Java name for marketing purposes
   - JavaScript == ECMA-262

<br>

4. It is not a beginner's language
   - While easy at the beginning of learning, it is powerful enough to build complex services

5. It is a Web standard
   - HTML5: HTML5 + CSS3 + JavaScript
   - HTML5 has a high dependency on JavaScript

<br>

*JavaScript is well-suited for functional programming!!!*

<br>

#### Pros of JavaScript

1. Programming is possible with just a text editor and a web browser
2. Easy to learn and use due to easy data types and type-casting
3. Testing written code is convenient because there is no compilation process

<br>

<br>

## Data Types & Variables

<br>

### JavaScript Syntax

<br>

#### JavaScript Basic Syntax

- Interpretation order

  - Interpreted and executed from top to bottom by the Interpreter

    - `Interpreter`

      : A program that converts a program written in a programming language into machine code

- Case sensitivity

  - Variables, methods, keywords, etc. must be entered with exact case distinction
  - HTML is not case-sensitive

- End of statement

- Whitespace and indentation

- Comments

<br>

<br>

### Data Type Classification (typeof)

<br>

#### 1. Primitive Types

> Immutable values

- boolean
- null
- undefined
- number  (*NaN* is also a number type)
- string
- symbol (ES6)

<br>

#### 2. Object Types

- object: plain object, function, array

<br>

<br>

### Data Type

<br>

#### Number

- It is not that the integer number system does not exist, but rather that there is no separate Integer Type

<br>

#### String

- Template strings

<br>

#### null vs undefined

- undefined
  -

- null
  - When declared but no value has been assigned
  - typeof null => shows as object

<br>

#### Object

- In JavaScript, everything except primitive types is an object
- JavaScript objects are collections of properties consisting of keys and values
- Value == Function?
  - Called a method

<br>

#### Variable Scope

- Has **function-level scope**
- Variables declared inside a function are local variables, and the rest are used as global variables
- If a keyword (var) is not used when declaring a variable, it is implicitly set to global
  - Note: Created as a property of the global object (window), not a variable
    - It is not assigned to a variable but becomes window.global!
  - Always use a keyword!

<br>

#### Hoisting and let, const (ES6)

- In JavaScript, all declarations are hoisted
- The `let` and `const` keywords newly introduced in ES6 can prevent this
  - It is not that hoisting itself does not occur; var declares and initializes (undefined) simultaneously,
  - while let and const have separated declaration and initialization stages
- Has block-level scope

<br>

<br>

### JavaScript Syntax

<br>

#### `==` vs `===`

- Equality operator (==)
  - Value comparison and unexpected conversions
- Strict equality operator (===)
  - Strict equality
  - Type comparison
  - Same as Python's ==!

<br>

#### Conditional Statements

- else if
- {}

<br>

#### Loops

- {}

<br><br>

### JavaScript Object

> An object is a collection of properties consisting of keys and values

<br>

#### Basic Object Creation Methods

1. Object literal

   ```javascript
   var cat1 = {}
   var cat2 = {name:'nero', age:3}
   ```

2. Object constructor function

   ```javascript
   var dog1 = new Object()
   dog1.name = 'cherry'
   dog1.name = 5
   ```

   <br>

#### Object Creation Methods

- When creating with an object literal, if the key can be expressed as a string, implicit type conversion occurs

  - If not, you must use quotes to make it a string!

  ```javascript
  var OBJ = {
      name: 'chloe',
      'e-mail': 'chloe@test.com'
  }
  ```

  - Here, name undergoes implicit type conversion to a string!

<br>

- If you create and use a constructor function, you can create objects with identical properties like a class

  ```javascript
  function Person(name, age){
      this.name = name;
      this.age = age
  }
  var p1 = new Person('chloe', 25)
  ```

<br>

<br>

### Object Property Access

- Properties can be accessed with . or []

  - However, there are cases where you must use []

    - ex) When the key is not composed of a simple string

      ```javascript
      var OBJ = {
          name: 'chloe',
          'e-mail': 'chloe@test.com'
      }

      OBJ['e-mail']
      ```
