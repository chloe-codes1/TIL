# this keyword in JavaScript

<br>

<br>

## `this` 란?

<br>

### JS는 OOP 언어이다

<br>

#### this

=> 무조건 어떤 object를 지칭

<br>

#### method

=> 객체 안에 정의된 함수 ( .methodName() 으로 실행하는 함수)

<br>

#### function

=> method가 아닌 모든 함수

<br> <br>

### function() {} 정의 할 때, this 가 window가 아닌 경우

<br>

1. #### method 안의 ths

​       -> 해당 method가 정의된 객체 (object)

2. #### 생성자 함수 안의 this

 <br>

*method 정의 할 때, 반드시 function(){} 으로 정의 한다!*

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
        oioMethod(){ // ES6 Syntatic sugar: 코드를 짧고 쉽게 쓰게 해줌! 함수를 이렇게 짧게 정의 하게 해줌!
            console.log(this) // this = objInObj
        }
    },
    arr: [0, 1, 2],
    newArr: [],
    method2 () {
        /*
                this.arr.forEach(

                    // 애는 method가 아니다! 그냥 내가 만든 익명함수임 
                    // -> this 사용 불가 
                    function(number){
                            this.newArr.push(number*100)
                    }.bind(this) // bind해서 사용 가능하다!
                                // -> 그런데 이렇게 길게 쓸거니...?
                                //    => 그게 싫어서 나온게 arrow funciton이다!

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

`this` 에는 eventListener가 불린 주어가 되는 애가 `this`에 들어온다!

- 수동적임!
  - 불려진 대상에 따라 달라진다
