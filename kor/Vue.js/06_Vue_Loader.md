# Vue Loader

> <https://vue-loader-v14.vuejs.org/kr/features/scoped-css.html>

<br>

<br>

## Scoped CSS

> `<style>` 태그가 scoped 속성을 가지고있을 때, CSS는 현재 컴포넌트의 엘리먼트에만 적용

<br>

### `scoped` option

- scoped option은 해당 컴포넌트에만 영향을 준다
  - 하지만, **class** 지정은 해야한다
    - 그렇게 해야 속도가 빠르다!
      - why?
        - browser 가  css select 를  rendering 하는 방식 때문에 class 를 지정하지 않으면 전체를 탐색함

<br>

### Local style 과 global style

- 하나의 컴포넌트 안에 `scoped` style과 그렇지 않은 style을 동시에 사용할 수 있다

  ex)

  ```html
  <style>
  /* global styles */
  </style>
  
  <style scoped>
  /* local styles */
  </style>
  ```

<br>

### Child component의 Root element

- `scoped` 속성을 사용하면 부모 컴포넌트의 style은 자식 component에 영향을 미치지 않는다
  - 하지만!
    - 자식 component의 root node 는 영향을 받는다!
      - 자식 component의 root element를 바꿈으로써 layout을 설정하기 위한 목적

<br>

### Deep Selectors

#### `>>>` Combinator

- `scoped` style을 사용하면서 자식 component에도 영향을 미치려면 `>>>` combinator 를 사용하면 된다

  ex)

  ```html
  <style scoped>
  .a >>> .b { /* ... */ }
  </style>
  ```

<br>

### `v-html` 과 `scoped` style

- `v-html` 은 `scoped` style의 영향을 받지 않는다
  - but, deep selector (ex. 바로 위에서 본 `>>>` combinator) 를 사용하면 style 할 수 있다

<br>

<br>

`+`

### `v-html` vs `v-text`

: **innerHTML**과 **innerText**의 차이 라고 생각하면 된다!

<br>

<br>

### lazy load 란?

- component 가 쓰일 때에만 call을 보낸다
  - 훨씬 경제적!
- 빠른 loading이 필요할 때 사용
- 잘 안가는 곳은 lazy로 설정하자!
  - ex) 고객센터
