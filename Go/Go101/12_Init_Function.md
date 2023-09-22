# Init Function

> Go의 init() function에 대해 알아보아요

<br>

<br>

### init() function

- `init()` function은 main function과 비슷해 보이지만, 인자를 받거나 값을 return하지 않는다
- `init()` function은 package가 load 될 때 가장 먼저 호출되는 함수이다
  - Package의 초기화 logic이 필요할 때 사용하면 된다!

<br>

<br>

### When is the `init()` function run?

`import` --> `const` --> `var` --> `init()` 순으로 실행된다

![](../../images/go_init_function.png)
