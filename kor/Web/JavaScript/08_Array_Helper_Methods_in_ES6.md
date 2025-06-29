# JavaScript Array Helper Methods

<br>

## Callback function

<br>

### Callback function 이란? - MDN

: A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of rotine or action.

<br>

콜백 함수(A)는 다른 함수(B)의 인자로 넘겨지는 함수로,

다른 함수(B)의 내부에서 실행되는 함수(A)를 말한다.

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
    // [0, 9, 99] 를 순회하며, 각 요소를 (number) 자리에 넣는다.
    // 그리고 리턴된 값을 새로운 배열에 넣고 마지막에 리턴한다.
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
//   : return 값이 없다!

let sum = 0
nums = [1,2,3]
nums.forEach(function(number){
    // numbers의 각 요소를 number 자리에 넣고,
    // 나머지는 알아서 해라! return 없다!
    sum += number
})

console.log('밍?'+nums)
```

<br>

### 3. filter()

> Returns the found element in the array, if some element in the array satisfies the testing callback function, or undefined if not found.

ex)

```javascript
// 3. filter
const odds = [1,2,3].filter(function(number) {
    // 각 요소를 number 자리에 넣고,
    // return이 true인 요소들만 모아서 새로운 배열로 return
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
 // filter()와는 다르게 find()는 함수가 true를 return하면 바로 종료됨
    return !(number & 1)
})
console.log('짝수 찾아라~ ', evens)
```

<br>

### 5. every()

> Returns true if every element in this array satisfies the testing callback function

ex)

```javascript
// 5. every
const pass = [50,60,70,80,90].every(function(number){
    // 모든 원소들이 조건을 통과하면 true, 아니면 false return
    return number > 40
})
console.log('통과입니까? ',pass)
```

<br>

<br>
