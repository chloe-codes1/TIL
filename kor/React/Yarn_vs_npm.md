# Yarn vs npm

> 정확하게 설명하지 못하던 내용을 정리해봐요!
> Reference: [npm-vs-yarn-choosing-the-right-package-manager](https://medium.com/javascript-in-plain-english/npm-vs-yarn-choosing-the-right-package-manager-a5f04256a93f#:~:text=npm%20automatically%20executes%20a%20code,lock%20or%20package.)

<br>

<br>

### Before getting started

- npm과 Yarn은 모두 훌륭한 Node.js, JavaScript package manager다
- 그렇다면 npm이 이미 있는데 Yarn이 개발된 이유는 무엇일까?
  - Yarn은 npm의 느린 package 설치 속도와 보안 이슈들을 해결하고자 Facebook에 의해 만들어졌다
- 이 글에서는 이 두 package maganger를 비교해서 어떤 것을 사용할지 결정하는 것을 도와주도록 하겠다

<br>

<br>

### 1. Parallel installation of packages

- 하나의 package가 설치될 때, 일련의 과정이 따라서 수행되게 된다
- 여러개의 package들을 동시에 설치할 때, 
  - npm은 하나의 package가 완전히 설치되고 나서 그 다음 package를 설치한다
    - 즉, npm은 각각의 package들을 순서대로 설치한다
  - 반면에 Yarn은 이러한 과정을 **병렬적**으로 처리하기 때문에 **효율성**과 **속도**가 더 좋다

<br>

예시로 react를 각각의 package를 설치했을 때, 아래와 같은 결과가 나옴을 확인할 수 있었다

- **npm** - 3.572초 소요
- **Yarn** - 1.44초 소요

참고:[Yarn & npm benchmarks](https://github.com/pnpm/benchmarks-of-javascript-package-managers)

<br>

<br>

### 2. Automatic Lock file generation

- npm과 Yarn모두 **package.json** file을 통해 의존성을 관리한다
- 새로운 dependency를 설치할 때마다 해당 dependency의 version이 **caret (^)** 기호로 시작하는 것을 확인 할 수 있다
  - 이것은 우리가 package를 Install 할 때마다 package manager는 더 최신 version을 찾는다는 것을 의미한다
    - 더 최신 버전이 있으면, `package.json` file에 명시된 version이 아닌 최신 버전으로 설치한다
  - 만약 위의 동작을 원하지 않는다면,
    1. **lock file** 을 생성하여 특정 version을 설치하도록 하거나
    2. **carret (^)** 기호를 지우는 방법이 있다
- Yarn은 새로운 dependency가 추가될 때마다 자동적으로 `yarn.lock` file을 생성한다
  - package 설치 시점 당시 동일한 version 정보를 `yarn.lock` file에 저장해둠으로써 새로운 혼경을 구축할 때도 동일한 verson 정보를 가진 package로 설치할 수 있도록 도와준다
- npm도 `npm shrinkwwrap` 명령어를 사용하여 의존성 버전을 고정시키는 lock file을 생성할 수 있다
  - 하지만, 이 둘의 차이점은 Yarn은 언제나 `yarn.lock` file을 생성하고 update 하는 것에 반해 npm은 lock file을 default로 생성하지 않고, `npm-shrinkwrap.json` file이 존재할 때만 내용을 update 한다
  - npm v5.0 이후로는 **의존성 트리에 대한 정보**를 가지고 있는 `package-lock.json` 을 도입하여 npm을 사용하여 `package.json` file 또는 `node_modules` tree를 수정하면 `package-lock.json` file 에 기록하도록 하였다
    - 이것으로 npm의 package 설치 과정과 성능을 향상시킬 수 있었지만, 여전히 yarn의 속도를 따라잡지는 못하고 있다

<br>

<br>

### 3. Security

- npm은 package들을 설치하는 도중에 코드를 즉각 실행시키는 것을 허용하고, 이것으로 인해 보안적 취약성이 발생할 수 있다
  - 반면에, Yarn은 `yarn.lock` 또는 `package.json`에 명시되어 있는 file들만 설치하고, `yarn.lock`을 통해 고정된 의존성 버전을 설치하기 때문에 모든 device에 같은 package를 설치하기 때문에 npm보다 안전하다
- Yarn은 코드가 실행되기 전에 **checksum**을 사용하여 설치된 package들의 무결성 검사를 진행한다

<br>

<br>

#### Wrap-up

- 빠르고, 안전성, 신뢰성을 갖고있는 Yarn을 쓰자