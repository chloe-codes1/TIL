# Props & Event emit

> <https://kr.vuejs.org/v2/guide/components.html#Props>

<br>

<br>

## Passing Data with Props

- Every component instance has its own isolated scope
  - This means you cannot (and should not) directly reference parent data in a child component's template!
  - Data can be passed down to child components using the `props` option

<br>

### Prop

- A custom attribute for passing information from a parent component
- The child component must explicitly declare the `props` it expects to receive from the parent component using the `props` option

<br>

ex)

> Parent.vue - Parent component

```vue
<template>
  <div class="parent">
      <h2>Parent Component</h2>
      <!-- 1. prop name="content" -->
      <Child @hungry="onHungrySignal" :propFromParent="parentMsg" />
      <!-- The custom event that the child $emit-ted is 'hungry' -->
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
    // 2. Register
    components: {
        Child, // This is a shorthand for Child: Child!
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

> Child.vue - Child component

```vue
<template>
  <div class="child">
      <h2>Child Component</h2>
      <!-- 3. Use it. -->
      {{ propFromParent}}

      <button @click="hungrySignal"> I'm hungry!</button>
  </div>
</template>

<script>
export default {
    name: 'Child',
    // 2. Register props (must use object for validation)
    props: {
        propFromParent: String, // Validation check for incoming data
    },
    methods: {
        hungrySignal () {
            // 1. Emit event (signal) to parent
            this.$emit('hungry', 'I want pizza', 'I want chicken too') // Custom Event('eventName', ...data)
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

- Since HTML attributes are case-insensitive, when using non-string templates you need to use the `kebab-case` equivalent of `camelCased` prop names

<br>

<br>

### `Literal` vs `Dynamic`

- A literal prop passes a string, not a number

  ``` vue
  <comp some-prop="1"></comp>
  ```

- To pass an actual JavaScript number, you need to use `v-bind` or `:` so the value is evaluated as a JavaScript expression!

  ```vue
  <comp v-bind:some-prop="1"></comp>
  ```

<br>

<br>

### One-way Data Flow

- All props form a **one-way** binding between the child property and the parent one
  - When the parent property updates, it will flow down to the child, but not the other way around!
  - This prevents child components from accidentally **mutating the parent's state**, which would make your app's data flow harder to reason about

- Vue.js supports two-way binding
  - v-model is two-way
- It is possible without emit
  - but, Vue recommends using one-way binding even though two-way binding between components is possible!
    - **You should create a one-way flow!**

<br>

<br>

## Event Emit

> A communication method from child components to parent components

<br>

### Event Emission Code Format

- Add code like the following in the child component's `method` or `life-cycle hook`

  ``` vue
  this.$emit('EVENT_NAME');
  ```

- To receive the event, implement the following in the parent component's template

  ``` vue
  <div id="app">
    <child-component v-on:event-name="method name of the parent component to execute or expression"></child-component>
  </div>
  ```

<br>

<br>

`+`

## Building a Youtube Browser

<br>

### 1. Get Youtube API key from Google Developer Console

<br>

### 2. Install `axios`

```bash
npm i axios
```

<br>

### 3. Understand usage through official documentation

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
