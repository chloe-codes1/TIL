# NPM

<br>

<br>

### NPM (Node Package Manager) 의 주요 기능

1. [NPMSearch](https://npmsearch.com/) 에서 탐색 가능한 Node.js 패키지/모듈 저장소
2. Node.js 패키지 설치 및 버전 / 호환성 관리를 할 수 있는 커맨드라인 유틸리티

<br>

<br>

> npm 설치 확인

```shell
$ npm --version
6.13.4
```

<br>

> npm version update

```shell
sudo npm install npm -g
```

<br>

<br>

### Installing Modules using NPM

<br>

> Syntax to install any Node.js module

```shell
npm install <Module Name>
```

<br>

> Install a famous Node.js web framework module called **express**

```shell
npm install express
```

<br>

> Now you can use this module in your js file as following

```shell
var express = require('express');
```

<br>

<br>

### Global vs Local Installation

<br>

기본적으로는 `npm` 은 module을 local mode로 설치

- **Local mode**

  : package를 명령어를 실행한 directory 안에 있는 `node_modules`에 설치하는 것을 의미

- **Global mode**

  : System directory에 설치하는 것을 의미

<br>

> express를 글로벌 mode로 설치하기

```shell
$ sudo npm install express -g
/usr/lib
└─┬ express@4.13.4
 ├─┬ accepts@1.2.13
 │ ├─┬ mime-types@2.1.9
 │ │ └── mime-db@1.21.0
 │ └── negotiator@0.5.3
 .... 길어서 생략....
 │ └── statuses@1.2.1
 ├── utils-merge@1.0.0
 └── vary@1.0.1
```

- 현재 경로가 아닌 /usr/lib/node_modules 에 모듈을 설치하는 것 확인 가능

- system에 저장하므로, root 계정이 아니라면 앞에 `sudo`를 붙여주어야 함!

- **Global mode** 로 설치하였을때는, node application에서 바로 `require` 할 수는 없음

  - but, `npm link` 명령어를 입력하여 해당 module을 불러올 수 있음

  ```shell
  npm install -g express
  cd [local path]/project
  npm link express
  ```

<br>

<br>

### package.json

: Node application / module의 경로에 위치해 있으며 pacakge의 속성을 정의함

<br>

> express로 project를 생성했을 때 생성되는 **package.json**

```shell
{
  "name": "myapp",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.13.2",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.13.1",
    "jade": "~1.11.0",
    "morgan": "~1.6.1",
    "serve-favicon": "~2.3.0"
  }
}
```

- **package.json**은 project가 의존하는 module과 module version의 정보를 담고있음

<br>

<br>

#### Uninstalling a Module

<br>

```shell
npm uninstall express
```

<br>

<br>

#### Updating a Module

<br>

```shell
npm update express
```

<br>

<br>

#### Search a Module

<br>

```shell
npm search express
```

- 이 명령어는 처음 이용할 때 memory 엄청 잡아먹음
  - Cloud IDE를 사용하거나 server에 ram이 1G 정도라면 매우 오래걸리거나 에러가 남
  - 그럴땐  [NPMSearch](https://npmsearch.com/) 에서 검색하기!

<br>
