# Vue Router

> Rendering different components based on URL

<br>

<br>

### Why Router is Needed

- To maintain SPA characteristics while having different URLs
  - Rendering different components based on URL
- Route/view mapping

<br>

<br>

### Characteristics of Vue

- Keep it small and lightweight, but allow adding necessary features!
- That's why you need to add the router separately if you want to use it!

<br>

<br>

### Install Vue Router

> Standard installation

```bash
npm install vue-router
```

> **Add** using vue's power
>
> - Run from the project root!

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

- Try to **add** it as soon as possible after creating the project!
  - So that this message doesn't appear~

<br>

<br>

ex)

### `App.vue`

```vue
<template>
  <div id="app">
    <div id="nav">
      <!-- Using an a tag like this causes a page reload -->
      <a href="/">Home</a> &nbsp;
      <a href="/about">About</a>
      <br>

      <!-- So you should use router-link! There's no reason to use Vue if the page reloads! -->
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

<br>

### router > `index.js`

> The `index.js` inside router is like `urls.py` in Django!

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'
import About from '../views/About.vue'

Vue.use(VueRouter)

  // Like urls.py in Django!
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

- The directory where **components** that will be mapped to URLs(/) go
- The ones that will be assigned a URL~!
- Components in `views/` are imported in router/index.js!

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

### Building Ping - Pong

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
