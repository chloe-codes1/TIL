# Introduction to Node.js

<br>

<br>

#### Reasons to learn Node.js

1. Allows you to build complex & powerful applications without writing complex code
2. Well suited to build **microservices**

3. Can be used for more than just web development
4. A robust project that won't be going anywhere

<br><br>

### What is Node.js?

> JavaScript runtime environment

<br>

- Google Chrome의 JavaScript Engine (V8 Engine) 에 기반해 만들어진 server side platform
  - Chrome V8 Engine으로 빌드된 JavaScript runtime
- Event based non-blocking I/O model을 사용해 가볍고 효율적
- Node.js의 패키지 생태계인 `npm` 은 세계에서 가장 큰 **open source library**

<br>

#### Node는 Web server가 아니다

- Node 자체로는 아무것도 하지 않음!
  
  - Apache web server 처럼 HTML file 경로를 지정해주고 Server를 열어주는 등의 설정이 없음!
  - but, **HTTP Server**를 직접 작성해야함! (library를 사용하여)
  
- Node.js는 그저 code를 실행할 수 있는 방법에 불과한 그저 **JavaScript Runtime** 일 뿐!

  ```javascript
  Node.js == Runtime Environment + JavaScript Library
  ```

<br>

<br>

### Features of Node.js

<br>

#### 1. 비동기 I/O 처리 & Event Driven

- Node.js library의 모든 API는 asynchronous, 즉 멈추지 않는다 (**Non-blocking**)
- Node.js based server는 API가 실행되었을 때, data를 return할 때까지 기다리지 않고 다음 API를 실행함
- 이전에 실행했던 API가 결과값을 return할 때까지 Node.js의 notification mechanism of Events 를 통해 결과값을 받아옴

<br>

#### 2. 빠른 속도

- Google Chrome의 V8 JavaScript engine을 사용하여 빠른 코드 실행을 제공함

<br>

#### 3. Single Threaded, but highly scalable

- Node.js는 event loop와 함께 single thread model을 사용함
- Event mechanism은 server가 멈추지않고 반응하도록 해주어 **server의 확장성**을 키워줌
  - 반면, Apache 같은 일반적인 web server는 요청을 처리하기 위하여 제한된 thread를 생성함
- Node.js 는 thread를 한 개만 사용하고 Apache와 같은 web server보다 훨씬 많은 요청을 처리할 수 있다!

<br>

#### 4. No buffering

- Node.js application엔 data buffering이 없고, data를 chunk로 출력함

#### 5. License

- MIT License가 적용되어 있음

<br>

<br>

### Who Uses Node.js?

Following is the link on github wiki containing an exhaustive list of projects, application and companies which are using Node.js. This list includes eBay, General Electric, GoDaddy, Microsoft, PayPal, Uber, Wikipins, Yahoo!, and Yammer to name a few.

- [Projects, Applications, and Companies Using Node](https://github.com/joyent/node/wiki/projects,-applications,-and-companies-using-node)

<br>

<br>

### Where to Use Node.js?

> 다음과 같은 분야에서 Node.js가 사용된다면 효율성이 뛰어나다!

<br>

- I/O가 잦은 application
- Data streaming application
- Data Intensive Real-time Applications (DIRT)
- JSON APIs based Applications
- Single Page Applications

<br>

<br>

### Where Not to Use Node.js?

- CPU 사용률이 높은 application에서는 Node.js 사용을 권장하지 않는다.

<br>
