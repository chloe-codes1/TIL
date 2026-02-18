# JavaScript Array Helper Methods

<br>

## Callback function

<br>

### What is a Callback function? - MDN

: A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

<br>

A callback function (A) is a function passed as an argument to another function (B),

and is a function (A) that is executed inside the other function (B).

<br>

<br>

### 1. map()

> Returns a new array containing the results of calling `callbackFn` on every element in this array.

ex)

```javascript
['1', '2','3'].map(Number)

const numbers = [0, 9, 99]

function addOne(number) {
    return number + 1
}
const newNumbers1 = numbers.map(addOne)
console.log(newNumbers1)

const newNumbers2 = numbers.map(function(number) {
    // Iterates through [0, 9, 99], placing each element in the (number) position.
    // Then returns the value to a new array and returns it at the end.
    return number + 1
})
console.log(newNumbers2)
```

<br>

### 2. forEach()

> Calls a callback function for each element in the array.

 ex)

```javascript
// 2. forEach
//   : There is no return value!

let sum = 0
nums = [1,2,3]
nums.forEach(function(number){
    // Places each element of numbers in the number position,
    // and does the rest on its own! No return!
    sum += number
})

console.log('huh?'+nums)
```

<br>

### 3. filter()

> Returns the found element in the array, if some element in the array satisfies the testing callback function, or undefined if not found.

ex)

```javascript
// 3. filter
const odds = [1,2,3].filter(function(number) {
    // Places each element in the number position,
    // and collects only elements where return is true into a new array and returns it
    return number %2
})

console.log(odds)
```

<br>

### 4. find()

> Returns the found element in the array, if some element in the array satisfies the testing callback function, or undefined if not found.

ex)

```javascript
// 4. find
const evens = [1,2,3,4].find(function(number) {
 // Unlike filter(), find() terminates as soon as the function returns true
    return !(number & 1)
})
console.log('Find the even number~ ', evens)
```

<br>

### 5. every()

> Returns true if every element in this array satisfies the testing callback function

ex)

```javascript
// 5. every
const pass = [50,60,70,80,90].every(function(number){
    // Returns true if all elements pass the condition, otherwise returns false
    return number > 40
})
console.log('Did it pass? ',pass)
```

<br>

<br>
