# Event Loop in Node.js

<br>

<br>

### Event Loop

- Node.js에선 Event를 매우 많이 사용하고, 이 때문에 다른 기술들보다 훨씬 속도가 빠름
- Node.js 기반으로 만들어진 server가 가동되면, 
  - 변수들을 initialize하고, 
  - 함수를 선언하고,
  - Event가 일어날 때 까지 기다림
- Event-Driven application에서는 event를 대기하는 main loop가 있음
  - 그리고 event가 감지되었을 시 **Callback 함수** 를 호출함

<br>

![ff](https://velopert.com/wp-content/uploads/2016/02/ff.png)

<br>

- 