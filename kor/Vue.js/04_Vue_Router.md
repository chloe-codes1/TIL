# Vue Router

> URL에 따른 다른 component rendering

<br>

<br>

### Router 가 필요한 이유

- SPA 의 특성을 살리되, URL을 달리 하기 위해
  - URL에 따른 다른 component rendering
- Route/view mapping

<br>

<br>

### Vue 의 특징

- 작고 가볍지만, 필요한 기능을 추가 할 수 있게 하자!
- 그래서 router 사용하려면 따로 추가해야함!

<br>

<br>

### Install Vue Router

> 일반 설치

```bash
npm install vue-router
```

> vue의 힘을 빌려 **add** 하기
>
> - Project 최상단에서 실행!

```bash
$ vue add router

WARN  There are uncommited changes in the current repository, it's recommended to commit or stash them first.
? Still proceed? Yes

📦  Installing @vue/cli-plugin-router...

+ @vue/cli-plugin-router@4.4.1
added 2 packages from 1 contributor, updated 1 package and audited 1283 packages in 5.023s

46 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

✔  Successfully installed plugin: @vue/cli-plugin-router

? Use history mode for router? (Requires proper server setup for index fall
back in production) Yes

🚀  Invoking generator for @vue/cli-plugin-router...
⚓  Running completion hooks...

✔  Successfully invoked generator for plugin: @vue/cli-plugin-router
```

- 가능한 project 생성하자 마자 **add** 하기!
  - 이런 메시지 뜨지 않게 해라~

<br>

<br>

ex)

### `App.vue`

```vue
<template>
  <div id="app">
    <div id="nav">
      <!-- 이렇게 a tag 쓰면 page reload 됨 -->
      <a href="/">Home</a> &nbsp;
      <a href="/about">About</a>
      <br>

      <!-- 그래서 router-link 를 써야 함! page reload 되면 우리가 vue를 쓸 이유가 없음! -->
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

<br>

### router > `index.js`

> router 안에 있는 `index.js` 는 Django 에서 `urls.py` 같은 것!

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
import About from '../views/About.vue'

Vue.use(VueRouter)

  // Django 에서 urls.py 같은 것!
  const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router

```

<br>

### `views/` directory

- URL(/) 과 mapping 될 **component**들이 들어가는 directory
- URL을 하사 받을 애들~!
- `views/` 에 있는 Component들은, router/index.js 로 가서 import 한다!

<br>

<br>

## variable routing

<br>

```vue
<template>
  <div>
      <h1>Hello, {{ name }}</h1>
  </div>
</template>

<script>
export default {
    name: 'HelloName',
    data: function() {
        return {
            name: this.$route.params.name,
        }
    }
}
</script>
```

<br>

### Ping - Pong 만들기

#### `Ping.vue`

```vue
<template>
  <div>
      <h1>Ping</h1>
      <input type="text" @keyup.enter="sendToPong" v-model="inputText"/>

  </div>
</template>

<script>
export default {
    name: 'Ping',
    data() {
        return {
            inputText: '',
        }
    },
    methods: {
        sendToPong: function() {
            // $router
            // ver1)
            // this.$router.push(`pong?message=${this.inputText}`)
            // ver2)
            this.$router.push({ name: 'Pong', query: {message: this.inputText}})
        }
    }
}
</script>

<style>

</style>
```

<br>

### `Pong.vue`

```vue
<template>
  <div>
      <h1>Pong</h1>
      <h3>{{messageFromPing}}</h3>
  </div>
</template>

<script>
export default {
    name: 'Pong',
    data(){
        return {
            messageFromPing: this.$route.query.message
        }
    }
}
</script>

<style>

</style>
```
