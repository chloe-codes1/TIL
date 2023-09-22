# Event Loop and EventEmitter Class

<br>

<br>

### Event Loop

- Node.js에선 Event를 매우 많이 사용하고, 이 때문에 다른 기술들보다 훨씬 속도가 빠름
- Node.js 기반으로 만들어진 server가 가동되면,
  - **변수**들을 initialize하고,
  - **함수**를 **선언**하고,
  - **Event**가 일어날 때 까지 기다림
- `Event-Driven application`에서는 event를 대기하는 **main loop**가 있음
  - 그리고 event가 감지되었을 시 **Callback 함수** 를 호출함

<br>

![ff](https://velopert.com/wp-content/uploads/2016/02/ff.png)

<br>

#### Event vs Callback Function

- `Callback function`은 비동기식 함수에서 결과를 반환할 때 호출
- `Event Handling`은 **observer pattern**에 의해 작동됨

<br>

##### `Observer pattern`

- object의 상태 변화를 관찰하는 **관찰자**들, 즉 observer들의 목록을 object에 등록하여 상태 변화가 있을 때마다 method 등을 통해 객체가 직접 목록의 각 observer에게 통지하도록 하는 **design pattern**
- 주로 **Distributed event handling system** 을 구현하는 데 사용됨

<br>

이벤트를 대기하는 `EventListeners` 함수들이 **observer** 역할을 함!

-> Observer들이 event를 기다리다가, event가 실행되면 event를 처리하는 함수가 실행됨!

<br>

<br>

### events module & EventEmitter Class

: Node.js의 `event module`과 `EventEmitter Class` 를 사용하여 **event**와 **event handler**를 bind 할 수 있다

<br>

#### 사용 방법

```javascript
// events module 사용
var events = require('events')

// EventEmitter object 생성
var eventEmitter = new events.EventEmitter();

// Bind event & EventHandler
eventEmitter.on('eventName', eventHandler);

// Program 안에서 event를 발생시키기
eventEmtter.emit('eventName');
```

<br>

ex)

> event_handle.js

```javascript
// events module 사용
var events = require('events');

// EventEmitter object 생성
var eventEmitter = new events.EventEmitter();

// EventHandler 함수 생성
var connectHandler = function connected(){
    console.log("You've connected");

    // data_received event 발생시키기
    eventEmitter.emit('data_received');
}

// connection event와 connectHandler 를 연동
eventEmitter.on('connection', connectHandler);

// data_received event와 anonymous function 연동
// -> 함수를 변수안에 담는 대신에, .on() method의 인자로 직접 함수를 전달
eventEmitter.on('data_received', function() {
    console.log('Data received');
}) 

// connection event 발생 시키기
eventEmitter.emit('connection');

console.log('Program has ended');
```

<br>

> Result

```shell
$ node event_handle.js 
You've connected
Data received
Program has ended
```

<br>

<br>

## EventEmitter Class

- Many objects in a Node emit events
  - Server emits an event each time a peer connects to it
  - An `fs.readStream` emits an event when the file is opened
- All objects which emit events are instance of `events.EventEmitter`

<br>

### Methods

| Sr.No. | Method & Description                                         |
| :----: | :----------------------------------------------------------- |
|   1    | **`addListener(event, listener)`** <br />Adds a listener at the end of the listeners array for the specified event. No checks are made to see if the listener has already been added. <br/>Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. <br/>Returns emitter, so calls can be chained. |
|   2    | **`on(event, listener)`**<br>Adds a listener **at the end of the listeners array** for the specified event. No checks are made to see if the listener has already been added. <br/>Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls can be chained. |
|   3    | **`once(event, listener)`**<br>Adds a one time listener to the event. <br/>This listener is invoked only the next time the event is fired, after which it is removed. <br/>Returns emitter, so calls can be chained. |
|   4    | **`removeListener(event, listener)`**<br>Removes a listener from the listener array for the specified event. <br>**Caution −** It changes the array indices in the listener array behind the listener. removeListener will remove, at most, one instance of a listener from the listener array. <br/>If any single listener has been added multiple times to the listener array for the specified event, then removeListener must be called multiple times to remove each instance. <br/>Returns emitter, so calls can be chained. |
|   5    | **`removeAllListeners([event])`**<br/>Removes all listeners, or those of the specified event. <br/>It's not a good idea to remove listeners that were added elsewhere in the code, especially when it's on an emitter that you didn't create (e.g. sockets or file streams). <br/>Returns emitter, so calls can be chained. |
|   6    | **`setMaxListeners(n)`**<br/>By default, EventEmitters will print a warning if more than 10 listeners are added for a particular event. <br/>This is a useful default which helps finding memory leaks. <br/>Obviously not all Emitters should be limited to 10. <br/>This function allows that to be increased. Set to zero for unlimited. |
|   7    | **`listeners(event)`**<br/>Returns an array of listeners for the specified event. |
|   8    | **`emit(event, [arg1], [arg2], [...])`**<br/>Execute each of the listeners in order with the supplied arguments. <br/>Returns true if the event had listeners, false otherwise. |

<br>

### Class Methods

| Sr.No. | Method & Description                                         |
| :----: | :----------------------------------------------------------- |
|   1    | **`listenerCount(emitter, event)`**<br/>Returns the number of listeners for a given event. |

<br>

### Events

| Sr.No. | Events & Description                                         |
| :----: | :----------------------------------------------------------- |
|   1    | **`newListener`**<br/>**event** − String<br/>: the event name<br/>**listener** − Function<br/>: the event handler functionThis event is emitted any time a listener is added. <br/>When this event is triggered, the listener may not yet have been added to the array of listeners for the event. |
|   2    | **`removeListener`**<br/>**event** − String The event name<br/>**listener** − Function The event handler function<br/>This event is emitted any time someone removes a listener. <br/>When this event is triggered, the listener may not yet have been removed from the array of listeners for the event. |

<br>

ex)

> EventEmitter.js

```javascript
var events = require('events');
var eventEmitter = new events.EventEmitter();

// listener #1
var listner1 = function listner1() {
   console.log('listner1 executed.');
}

// listener #2
var listner2 = function listner2() {
   console.log('listner2 executed.');
}

// Bind the connection event with the listner1 function
eventEmitter.addListener('connection', listner1);

// Bind the connection event with the listner2 function
eventEmitter.on('connection', listner2);

var eventListeners = require('events').EventEmitter.listenerCount
   (eventEmitter,'connection');
console.log(eventListeners + " Listner(s) listening to connection event");

// Fire the connection event 
eventEmitter.emit('connection');

// Remove the binding of listner1 function
eventEmitter.removeListener('connection', listner1);
console.log("Listner1 will not listen now.");

// Fire the connection event 
eventEmitter.emit('connection');

eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
console.log(eventListeners + " Listner(s) listening to connection event");

console.log("Program Ended.");
```

<br>

> Result

```shell
$ node EventEmitter.js 
2 Listner(s) listening to connection event
listner1 executed.
listner2 executed.
Listner1 will not listen now.
listner2 executed.
1 Listner(s) listening to connection event
Program Ended.
```
