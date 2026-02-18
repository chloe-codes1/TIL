# this keyword in JavaScript

<br>

<br>

## What is `this`?

<br>

### JS is an OOP Language

<br>

#### this

=> Always refers to some object

<br>

#### method

=> A function defined inside an object (a function executed with .methodName())

<br>

#### function

=> All functions that are not methods

<br> <br>

### Cases where this is NOT window when defining function() {}

<br>

1. #### this inside a method

          -> The object where the method is defined

2. #### this inside a constructor function

 <br>

*When defining a method, you must always define it with function(){}!*

<br>

ex)

```javascript
const obj = {
    name: 'obj',
    method1: function(){
        console.log(this) // this = obj
    },
    objInObj: {
        name: 'oio',
        oioMethod(){ // ES6 Syntactic sugar: makes code short and easy to write! Allows defining functions this short way!
            console.log(this) // this = objInObj
        }
    },
    arr: [0, 1, 2],
    newArr: [],
    method2 () {
        /*
                this.arr.forEach(

                    // This is NOT a method! It's just an anonymous function I created
                    // -> cannot use this
                    function(number){
                            this.newArr.push(number*100)
                    }.bind(this) // Can use it by binding!
                                // -> But are you going to write this long...?
                                //    => The arrow function was created because of this!

                    )//obj
                    */
        (number) => {
            this.newArr.push(number * 100)
        }
    }
}
```

<br>

<br>

The subject that called the eventListener becomes `this`!

- It is passive!
  - Changes depending on who called it
