# JavaScript Arrays and Functions

<br><br>

## JavaScript Arrays

<br>

### Array

> In JavaScript, arrays consist only of values

<br>

- Array literal

  ```javascript
  var a = [1,2,3]
  ```

  <br>

- Array constructor function

  ```javascript
  var b = new Array(1,2,3)
  ```

  <br>

  <br>

### Array Iteration

- `for`

  ```javascript
  var a = [1,2,3]

  for (var i=0 ; i <a.length; i++){
      console.log(i, a[i])
  }
  ```

  <br>

- `for .. of`

  : Outputs element values one by one

  ```javascript
  for (var elem of a){
      console.log(elem)
  }
  ```

  <br>

- `forEach`

  : Takes a function itself as an argument

  ```javascript
  a.forEach( function(elem, idx) {
      console.log(idx, elem)
  })
  ```

  <br>

- `for .. in`

  - Not only accesses array elements but properties can also be output
    - Since arrays in JavaScript are also objects, property settings are possible, but they become properties of the Object, not the list

  ```javascript
  var a = [1,2,3]

  a.name = 'myarr'

  for (var i in a){
      console.log(i, a[i])
  }

  //0 1
  //1 2
  //2 3
  //name myarr   => iterates through properties as well
  ```

  - *Be careful when using the for ... in form!*
    - for ...in iterates through all properties of the Object itself

<br>

<br>

### Array methods

<br>

- `sort`
  - If there is no comparison function (argument), it sorts **based on strings**
    - If you don't want that, pass a comparison function as an argument
  - If there is a comparison function, it sorts based on the return value being less than 0

<br>

- String-related
  - `join`
    - array.**join**('haha')
- `toString`

- Array merging

  - `concat`

    : Merges two arrays

- Element insertion/deletion

  - `push`
  - `pop`
  - `unshift`
    - Insert at the left end
  - `shift`
    - Remove from the left end

- Index search

  - `indexOf`

- Array manipulation

  - `splice(start[, deleteCount[, item1[, item2[, ...]]]])`

    - Modifies the original array itself

    - Can also modify/delete elements

      ```javascript
      var a = [1,2,3]
      a.splice(1,2, "first", "second") // Delete two from position 1 + append "first", "second"
      // [1, "first", "second"]

      var a = [1,2,3]
      a.splice(1,2, "first") // Delete two from position 1 + append "first"
      // [1, "first"]
      ```

- Array slicing

  - `slice`

    : Returns the result

<br>

<br>

## JavaScript Functions

<br>

### Function Declaration

<br>

#### 1. Function Declaration Statement

```javascript
function sum(a,b) {
    return a+b;
}
sum(1,2) //3
```

<br>

#### 2. Function Expression

```javascript
// Assign an anonymous function to a variable
var sub = function(a,b) {
    return a - b;
}
sub(1,2) //-1
```

<br>

#### 3. Immediately Invoked Function Expression (IIFE)

```javascript
(function(a,b){return a*b})(1,2) //2
```

<br>

#### 4. Arrow Function (ES6)

```javascript
var sum = (a,b) => a+b  // Single line a+b so curly braces {} are omitted
sum(3,4) //7

var area = (r) => {
    const PI = 3.14;
    return r*r*PI;
}
area(1) //3.14
```

<br>

<br>

### Function Arguments

- In JavaScript, there are no restrictions on passing parameters to functions

- The `arguments` object contains all information about the parameters passed

  ```javascript
  function foo(a) {
      console.log(arguments); // Print arguments to check
      return a
  }
  ```

  - If no arguments are passed, it shows undefined

    - `undefined`

      : The value JavaScript assigns when initializing a variable

<br>

<br>
