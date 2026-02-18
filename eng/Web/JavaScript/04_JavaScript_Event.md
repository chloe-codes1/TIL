# JavaScript Event

<br><br>

### Understanding Events

<br>

#### Event model

: Defines Event handlers and Event APIs

- Three different event models exist depending on the web browser and time period

  - Why?
    - Changed and improved depending on the type of web browser

- Types of Event Models

  - Original event model

    - Old model
    - Not compatible with IE 8 and below
    - Technically insufficient
    - DOM Level 0 event model

  - Standard event model

    - Currently supported by IE 9 and above and all other web browsers
    - DOM Level 2 event model

  - Internet Explorer event model

    - A model that can only be used in IE 8 and below
    - Not supported by other web browsers
    - No longer in use



<br>

<br>

### `.addEventListener()`

: Applies an event handler function to a DOM object

- EventTarget.**addEventListener** (type, listener, [, useCapture]);
  - **type**: Event type
  - **listener**: Callback function to execute when the event occurs (event handler)
  - **useCapture**: Default value (false), propagates to parent nodes (bubbling), if true propagates to child nodes (capturing)

<br>

<br>

#### `preventDefault()`

: Prevents the default behavior of an Event



<br><br>

### `.removeEventListener()`

: Removes an Event handler

- Must have the same three arguments as the matching `addEventListener()`

<br>

<br>

### Event Propagation

<br>

#### Three Stages of Event Propagation

1. Event propagates downward from the document node to the event target node
2. Event target node
3. Event propagates upward from the event target node to the document node

<br>

#### `.stopPropagation()`

: An event API that stops event propagation

<br>



- Events propagate from the target element, divided into capturing and bubbling
- It always starts with capturing and ends with bubbling
- Through the third argument **useCapture** (false by default) of the addEventListener method, event management for specific situations is possible

<br>

<br>

### Event Object and this

: When using this in an event listener's callback function, this refers to the element bound to the event listener

<br>

#### this and target

- The role of this in the function called by the Event handler

  : The object where the event occurred

- **event.target == this**
