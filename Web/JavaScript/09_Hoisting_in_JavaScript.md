# Hoisting in JavaScript

> <https://scotch.io/tutorials/understanding-hoisting-in-javascript>

<br>

<br>

## What is Hoisting?

- JavaScript mechanism where variables and function declarations are **moved to the top of their scope** before code execution.
  - no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

<br>

<br>

## undefined vs ReferenceError

<br>

### `undefined`

- In JavaScript, an undeclared variables is assigned the value `undefined` at execution and is also of type of undefined.

<br>

### `ReferenceError`

- In JavaScript, a ReferenceError is thrown when trying to access a previously undeclared variable.

<br>

*The behavior of JavaScript when handling variables becomes nuanced because of hoisting!*

<br>

<br>

## Hoisting variables

- all `undeclared variables` are **global variables**

ex)

```javascript
function hoist() {
  a = 20;
  var b = 100;
}

hoist();

console.log(a); 
/* 
Accessible as a global variable outside hoist() function
Output: 20
*/

console.log(b); 
/*
Since it was declared, it is confined to the hoist() function scope.
We can't print it out outside the confines of the hoist() function.
Output: ReferenceError: b is not defined
*/
```

<br>

### `var`

> function scoped

ex)

```javascript
console.log(hoist); // Output: undefined

var hoist = 'The variable has been hoisted.';
```

- JavaScript has hoisted the variable declaration

<br>

### `let`

> block scope

ex1)

```javascript
console.log(hoist); // Output: ReferenceError: hoist is not defined ...

let hoist = 'The variable has been hoisted.';
```

ex2)

```javascript
let hoist;

console.log(hoist); // Output: undefined
hoist = 'Hoisted'
```

- We should **declare** then **assign** our variables to a value before using them!

<br>

### `const`

> Introduced in ES6 to allow **immutable variables**

ex1)

```javascript
const PI = 3.142;

PI = 22/7; // Let's reassign the value of PI

console.log(PI); // Output: TypeError: Assignment to constant variable.
```

ex2)

```javascript
console.log(hoist); // Output: ReferenceError: hoist is not defined

const hoist = 'The variable has been hoisted.';
```

ex3)

```javascript
const PI;
console.log(PI); // Ouput: SyntaxError: Missing initializer in const declaration
PI=3.142;
```

- the variable is hoisted to the top of the block
- must be both declared and initialized before use.

<br>

<br>

## Hoisting functions

<br>

#### JavaScript functions

1. Function declarations
2. Function expressions

<br>

### Function declarations

> Hoisted completely to the top

ex)

```javascript
hoisted(); // Output: "This function has been hoisted."

function hoisted() {
  console.log('This function has been hoisted.');
};

```

<br>

### Function expressions

> Not hoisted

ex)

```javascript
expression(); //Output: "TypeError: expression is not a function

var expression = function() {
  console.log('Will this work?');
};
```

<br>

<br>

## Order of precedence

1. `Variable` assignment takes precedence over `function` declaration

   ```javascript
   var double = 22;
   
   function double(num) {
     return (num*2);
   }
   
   console.log(typeof double); // Output: number
   ```

   <br>

2. `Function` declarations take precedence over variable declarations

   ```javascript
   var double;
   
   function double(num) {
     return (num*2);
   }
   
   console.log(typeof double); // Output: function
   ```

<br>

*Function declarations are hoisted over variable declarations but not over variable assignments!*

<br>

<br>

## Hoisting classes

<br>

#### JavaScript Classes

1. Class declartions
2. Class expressions

<br>

### Class declarations

> Hoisted like function declarations

ex)

```javascript
var Frodo = new Hobbit();
Frodo.height = 100;
Frodo.weight = 300;
console.log(Frodo); // Output: ReferenceError: Hobbit is not defined

class Hobbit {
  constructor(height, weight) {
    this.height = height;
    this.weight = weight;
  }
}
```

- you have to declare a class before you can use it

<br>

### Class expressions

> Not hoisted like function expressions

ex)

```javascript
var Square = new Polygon();
Square.height = 10;
Square.width = 10;
console.log(Square); // Output: TypeError: Polygon is not a constructor

var Polygon = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```
