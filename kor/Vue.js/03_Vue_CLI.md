# Vue CLI

<br>

<br>

## Getting started with Vue CLI

<br>

### Installation

```bash
npm install -g @vue/cli
```

<br>

### Start project

```bash
vue create [PROJECT_NAME]
```

<br>

### Compiles and hot-reloads for development

```bash
$ npm run serve

 INFO  Starting development server...
98% after emitting CopyPlugin

 DONE  Compiled successfully in 3520ms                                                               9:50:57 AM


  App running at:
  - Local:   http://localhost:8080/ 
  - Network: http://192.168.0.5:8080/

  Note that the development build is not optimized.
  To create a production build, run npm run build.
```

<br>

### Install `axios`

```bash
npm i axios
```

<br>

### Compiles and minifies for production

```bash
npm run build
```

<br>

### Lints and fixes files

```bash
npm run lint
```

<br>

<br>

`+`

### Component 를 만들었을 때 해야 할 틀 (에 박힌) 일

```vue
<template>
  <div>

  </div>
</template>

<script>
export default {
    name: 'HelloName',
    data: function() {
        return {
            
        }
    }
}
</script>

<style>

</style>
```
