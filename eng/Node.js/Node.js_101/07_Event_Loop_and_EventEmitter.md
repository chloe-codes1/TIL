# Event Loop and EventEmitter Class

<br>

<br>

### Event Loop

- Node.js uses Events extensively, which is why it is much faster than other technologies
- When a Node.js-based server starts,
  - it **initializes** variables,
  - **declares** functions,
  - and waits for **Events** to occur
- In `Event-Driven applications`, there is a **main loop** that waits for events
  - And when an event is detected, it calls a **Callback function**

<br>

![ff](https://velopert.com/wp-content/uploads/2016/02/ff.png)

<br>

#### Event vs Callback Function

- A `Callback function` is called when an asynchronous function returns a result
- `Event Handling` works based on the **observer pattern**

<br>

##### `Observer pattern`

- A **design pattern** that registers a list of **observers** - those who observe state changes of an object - on the object, and notifies each observer in the list through methods whenever a state change occurs
- It is mainly used to implement **Distributed event handling systems**

<br>

`EventListeners` functions that wait for events serve as the **observers**!

-> Observers wait for events, and when an event fires, the function that handles the event is executed!

<br>

<br>

### events module & EventEmitter Class

: You can bind **events** and **event handlers** using Node.js's `event module` and `EventEmitter Class`

<br>

#### How to Use

```javascript
// Use the events module
var events = require('events')

// Create an EventEmitter object
var eventEmitter = new events.EventEmitter();

// Bind event & EventHandler
eventEmitter.on('eventName', eventHandler);

// Trigger an event within the program
eventEmtter.emit('eventName');
```

<br>

ex)

> event_handle.js

```javascript
// Use the events module
var events = require('events');

// Create an EventEmitter object
var eventEmitter = new events.EventEmitter();

// Create an EventHandler function
var connectHandler = function connected(){
    console.log("You've connected");

    // Trigger the data_received event
    eventEmitter.emit('data_received');
}

// Bind the connection event with connectHandler
eventEmitter.on('connection', connectHandler);

// Bind the data_received event with an anonymous function
// -> Instead of storing the function in a variable, pass the function directly as an argument to the .on() method
eventEmitter.on('data_received', function() {
    console.log('Data received');
})

// Trigger the connection event
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
