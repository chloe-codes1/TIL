# Props & Event emit

> <https://kr.vuejs.org/v2/guide/components.html#Props>

<br>

<br>

## Props 로 데이터 전달하기

- 모든 component instance 에는 자체 격리 된 범위가 있다
  - 즉, 하위 component의 template에서 상위 데이터를 직접 참조 할 수 없으며, 그렇게 해서는 안 됨!
  - 데이터는 `props` option을 사용하여 하위 component로 전달 될 수 있다

<br>

### Prop

- 상위 component의 정보를 전달하기위한 사용자 지정 특성
- 하위 component는 `props` option을 사용하여 상위 component로부터 받을 것으로 기대되는 `props` 를 명시적으로 선언해야 함

<br>

ex)

> Parent.vue - 상위 컴포넌트

```vue
<template>
  <div class="parent">
      <h2>Parent Component</h2>
      <!-- 1. prop 이름="내용" -->
      <Child @hungry="onHungrySignal" :propFromParent="parentMsg" />
      <!-- 자식이 $emit 한 custom event 가 hungry임  -->
  </div>
</template>

<script>
// 1. import
import Child from '../components/Child.vue'

export default {
    name: 'Parent',
    data(){
        return {
            parentMsg: 'Message from parent',
        }
    },
    // 2. 등록
    components: {
        Child, // Child: Child 를 간소화 한 것임!
    },
    methods: {
        onHungrySignal(menu1, menu2){
            console.log(menu1, menu2)
        }
    }
}
</script>

<style>

</style>
```

<br>

> Child.vue - 하위 컴포넌트

```vue
<template>
  <div class="child">
      <h2>Child Component</h2>
      <!-- 3. 사용한다. -->
      {{ propFromParent}}

      <button @click="hungrySignal"> 배고파요!</button>
  </div>
</template>

<script>
export default {
    name: 'Child',
    // 2. props 등록 (반드시 object 를 써야 Validation 가능)
    props: {
        propFromParent: String, //넘어오는 data 의 validation 검사
    },
    methods: {
        hungrySignal () {
            // 1. 부모한테 이벤트 (시그널) 방출
            this.$emit('hungry', '피자 먹고싶다', '치킨도 먹고싶다') // Custom Event('이벤트이름', ...데이터)
        }
    }
}
</script>

<style>
    .parent {
        border: 3px solid gray;
        margin: 3px;
        padding: 3px;
    }

    .child {
        border: 3px solid blue;
        margin: 3px;
        padding: 3px;
    }
</style>
```

<br>

<br>

### `camelCase` vs `kebab-case`

- HTML 속성은 대소 문자를 구분하지 않으므로 문자열이 아닌 템플릿을 사용할 때 `camelCased` prop 이름에 해당하는 `kebab-case`를 사용해야 함

<br>

<br>

### `리터럴` vs `동적`

- 리터럴 prop은 숫자가 아닌 문자열로 전달됨

  ``` vue
  <comp some-prop="1"></comp>
  ```

- JavaScript 숫자를 전달하려면 값이 JavaScript 표현식으로 평가되도록 `v-bind`   or  `:`  를 사용해야 함!

  ```vue
  <comp v-bind:some-prop="1"></comp>
  ```

<br>

<br>

### 단방향 데이터 흐름

- 모든 props는 하위 속성과 상위 속성 사이의 **단방향** 바인딩을 형성함
  - 상위 속성이 업데이트 되면 하위로 흐르게 되지만, 그 반대는 안 됨!
  - 이렇게 하면 하위 컴포넌트가 실수로 **부모의 상태를 변경**하여 앱의 데이터 흐름을 추론하기 어렵게 만드는 것을 방지할 수 있음

- vue.js 는 양방향 가능
  - v-model 은 양방향
- emit 하지 않아도 가능
  - but, vue는 컴포넌트 간 양방향 가능하지만 단방향을 쓰는것을 권장!
    - **단방향 flow 를 만들어야 한다!**

<br>

<br>

## Event Emit

> 컴포넌트의 통신 방법 중 하위 컴포넌트에서 상위 컴포넌트로 통신하는 방식

<br>

### 이벤트 발생 코드 형식

- 하위 컴포넌트의 `method`나 `life-cycle hook` 과 같은 곳에 아래와 같은 코드를 추가한다

  ``` vue
  this.$emit('EVENT_NAME');
  ```

- 해당 이벤트를 수신하기 위해 상위 component의 템플릿에 아래와 같이 구현

  ``` vue
  <div id="app">
    <child-component v-on:이벤트 명="상위 컴포넌트의 실행할 메서드 명 또는 연산"></child-component>
  </div>
  ```

<br>

<br>

`+`

## Youtube-browser 만들기

<br>

### 1. Google Developer Console에서 Youtube API key 받기

<br>

### 2. `axios` 설치

```bash
npm i axios
```

<br>

### 3. 공식 문서로 사용법 파악하기

> <https://developers.google.com/youtube/v3/docs/search>

<br>

<br>

`+`

## vue-filter

> install

```bash
npm install @vuejs-community/vue-filter-date-parse
```

<br>

> register

```vue
import Vue from 'vue';
import VueFilterDateParse from '@vuejs-community/vue-filter-date-parse';

Vue.use(VueFilterDateParse);
```

<br>
