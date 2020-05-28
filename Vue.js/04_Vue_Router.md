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

-  작고 가볍지만, 필요한 기능을 추가 할 수 있게 하자!
  - 그래서 router 사용하려면 따로 추가해야함!

<br>

<br>

### Install Vue Router

> 일반 설치

```bash
$ npm install vue-router
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

