# JavaScript Basic Syntax

<br>

## What is JavaScript?

> A language for manipulating the Browser

- Of the browser
- By the browser
- For the browser

<br>

*JavaScript is a war with standards!*

<br>

### JQuery

- Using JQuery may slow things down slightly, but it eliminates `cross-browsing` issues

<br>

<br>

## Vanilla JS

: A campaign saying let's stop using the JavaScript Libraries popping up everywhere!

- Vanilla == '**pure/original**'
- Using JavaScript without installing any library!

<br>

<br>

## JavaScript

<br>

> `window` is at the top

- window.document

![image-20200512104205991](../../../kor/Web/images/image-20200512104205991.png)

<br>

> Writing

- window.document.write()

![image-20200512104249854](../../../kor/Web/images/image-20200512104249854.png)

<br>

> Since the top is always `window`, it can be omitted

![image-20200512104840632](../../../kor/Web/images/image-20200512104840632.png)

<br>

<br>

### ASI (Automatic Semicolon Insertion)

: The principle of the feature is to provide a little leniency when evaluating the syntax of a JavaScript program by conceptually inserting missing semicolons

<br>

<br>

## 3 Core Components

1. #### BOM (Browser Object Model)

2. #### DOM (Document Object Model)

   - DOM manipulation
   - The reason JavaScript exists

3. #### ES (EcmaScript)

<br>

<br>

## ES (EcmaScript)

<br>

### let vs const

<br>

#### let

: Reassignment is possible

#### const

: Reassignment is not possible !== the value doesn't change

<br>

<br>

### Naming Convention

- Use lower camelCase!

- No snake_case!

  ```javascript
  const addOneToNumber // good
  const add_one_to_number //bad
  ```

  <br>

<br>

### Never use loose equality operators

- `==`, `!=`   =>  X
- `===`, `!==`   =>  O

<br>

<br>

### Function => `First-class Object`

1. Can be stored in a variable.

2. Can be a return value of a function.

3. Can be an argument to a function.

<br>

<br>

## DOM (Document Object Model) Manipulation

- Convert String-based HTML to Objects
- **Understand** and **interpret**
- Build a DOM Tree
- Render on screen (draw)

<br>

Summary:

- All data in the world is String (HTML)
- It must go through a parse/parsing process to be interpreted (DOM interprets)

<br>

<br>

### Selecting

### : `querySelector` ,  `querySelectorAll`

<br>

<br>

### Create

### : `.classList.add()`

```javascript
const myP = document.createElement('p')
myP.innerText = 'Greater'

const myPStr = '<p>Greate</p>'
myPStr.classList // undifined -> because it's a string
myP.classList.add('wow') // object can do this
```

<br>

<br>

<hr>

<br>

<br>

## I. Scope

> The youngest sibling shut-in rule

- When there are curly braces, a Scope is created!!
  1. In case of a function
  2. In case of control statements (if / while / switch (control)), etc.
- `var` was only scoped within functions
- `let` works the same way when there are curly braces (scope)

<br>

<br>

## II. `var`, `let`, `const`

- `var`
  - Free assignment
  - Free declaration
  - **Function** scope (never use this.)
- `let`
  - Free assignment
  - Can only be declared once
  - **Block** scope
- `const`
  - Assign once
  - Declare once
  - **Block** scope

<br>

<br>

### Identifier Convention

- **Variables, functions, objects**: camelCase (`camelCase`)
- **Classes, constructors**: PascalCase (`PascalCase`)
- **Constants**: uppercase snake case (`SNAKE_CASE`)

<br>

<br>

## III. Hoisting

> 1. Don't use var
> 2. Don't use function declaration form

<br>

- Using declaration form makes code not work as expected
  - Why?
    - It scans through once before execution, making references possible before declaration

<br>

```javascript
// Declaration form
function hello() {}

// Expression form
const hello = function() {}
```

<br>

<br>

## V. Data Types

<br>

### (1) Numbers

<br>

```js
const num1 = 123
const num2 = -2.88
const a = NaN // Not a Number
const b = Infinity
const c = -Infinity
```

<br>

### (2) Strings

- Concatenation
  - `+`
- Interpolation
  - `template literal ${}`

<br>

```js
const firstName = 'Chloe'
const lastName = 'Kim'
const middleName = 'Juhyun'

const fullName = firstName + lastName
const greeting = `Hello ${middleName}`
```

<br>

<br>

### (3) Boolean

- What is close to true and what is close to false
- `true`, `false`  (lowercase)

<br>

#### 1. Truthy

> All values that are not Falsy

- `[]` - emptyArray
- `{}` - emptyObject

<br>

#### 2. Falsy

> Non-existent or undefined things

- `null`
- `undefined`
- `""`
- `0`
- `[] == true`
- `![]`

<br>

<br>

## VI. Data Structures

> How to store and manipulate (CRUD) => look at methods

- Array (`list`)
  - array helper method
- Object (`dict`)

<br>

<br>

## VII. Functions

- Declaration (statement)
- Expression

<br>

### Arrow Function

> Use only where it is NOT a (Class) Method(OOP) function

1. Don't use arrow functions in Class definitions!
   - Why?
     - Because they don't bind `this`, `arguments`, `super`, `new.target`, etc.
2. Cannot be used as a constructor X
3. Cannot be used as an Event Listener Callback function X

<br>

ex)

```js
// 1. Declaration
function add (num1, num2){

    return num1 + num2
}

add(1,2)
// def add(num1, num2):


// 2. Expression
const sub = function(num1, num2){
    return num1 - num2
}

sub(2,1)
// sub = lambda input: output


// 3. Arrow Function
const arrow = function(name){
    return `hello ${name}`
}

const arrow = (name) => {
    return `hello!! ${name}`
}

// When there is one argument
const arrow = name => {
    return `hello!!! ${name}`
}

// Reduce to one line
const arrow = name => {return `hello!{name}`}

// Arrow function ultimate form
// (1) 1 argument
// (2) return exists & expression
const arrow = name => `hello!!!! ${name}`
```

<br>

<br>

## VIII. OOP

<br>

- Very flexible OOP through objects

- Forget about Classes for now!
  - Prototypal Inheritance
- `class` introduced from ES6+

ex)

```js
const chloe = {
    'name': 'Chloe',
    birth: '1995',
    'greeting': function(){
        return `Hi, This is ${name}`
    },
    farewell(){
        return `Bye~~ -${this.name}-`
    }
}

class Person {
    constructor(name, birth){
        this.name = name
        this.birth = birth
    }
    greeting() {
        return `Hi, This is ${this.name}`
    }
}

const camila = new Person('Camila', 1995)
const bella = new Person('Bella', 1993)


console.log(camila.name)
console.log(camila.greeting())
console.log(bella.name)
console.log(bella.greeting())

// Can add in the middle!! -> flexible
bella.money = 100000000
console.log(bella.money)

/*
In Python...

class Person:
    def __init__(self, name, birth):
        self.name = name
        self.birth = brith

    def greeting(self):
        return f'Hi, This is {self.name}'


*/
console.log(chloe.name)
console.log(chloe['birth'])
console.log(chloe.greeting())
console.log(chloe.farewell())
```
