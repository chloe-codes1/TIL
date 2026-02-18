# Redux

> Reference: [redux docs](https://redux.js.org/introduction/getting-started), [velopert](https://react.vlpt.us/redux/)

<br>

<br>

## 1. What is Redux?

- The most widely used state management library in the React ecosystem
- By using Redux
  - You can separate state-related logic of components into different files for more efficient management
  - You can also easily manage global state

<br>

<br>

## 2. Redux vs Context API

The difference between using Redux and Context API

<br>

### 2-1. Middleware

- Redux has the concept of **middleware**
  - Using Redux middleware, you can perform desired tasks before an action object is processed by the **reducer**
    - ex)
      - Making an action be ignored based on specific conditions
      - Logging an action to the console
      - Modifying an action when it is dispatched so it is passed to the reducer in a different form
      - When a specific action occurs
        - Triggering other actions based on it
        - Executing specific JavaScript functions
- Middleware is primarily used for handling **asynchronous operations**

<br>

### 2-2. Useful Functions & Hooks

- Using the `connect` function, you can receive Redux state or action creator functions as component props
- Using [Hooks](https://react-redux.js.org/api/hooks) like `useSelector`, `useDispatch`, `useStore`, you can easily query state or dispatch actions

<br>

### 2-3. Global State

- When managing global state using **Context API**, you typically create a separate `Context` for each feature,
  - With **Redux**, it is mandatory to put all global state into one large object
    - This helps avoid the inconvenience of creating a new `Context` every time!

<br>

<br>

## 3. Key Concepts

<br>

### 3-1. Action

- When a change in state is needed, an action is triggered

- An action is represented as a single object

  - ex)

    ```json
    {
      type: "VALUE"
    }
    ```

- An action object must have a `type` as a required field, and other values can be added as desired

  - ex)

    ```json
    {
      type: "TODO",
      data: {
        id: 0,
        text: "Go home"
      }
    }
    ```

  - ex)

    ```json
    {
      type: "CHANGE_INPUT",
      text: "Please go home"
    }
    ```

<br>

### 3-2. Action Creator

- An action creator is literally **a function that creates actions**

- It takes parameters and creates them in the form of an action object

- ex)

  ```javascript
  export function addTodo(data) {
    return {
      type: "ADD_TODO",
      data
    };
  }

  // Arrow function is also possible!
  export const changeInput = text => ({
    type: "CHANGE_INPUT",
    text
  });
  ```

- The reason for using `Action Creators` is to make it easier to trigger actions from components later
  - That's why the `export` keyword is typically attached to use the function from other files
- Using `Action Creators` is not mandatory in Redux!
  - You can also write action objects directly each time you trigger an action

<br>

### 3-3. Reducer

- A Reducer is **a function that produces changes**

- It takes two parameters

  - `state`

  - `action`

    - ex)

      ```javascript
      function reducer(state, action) {
        // Update status
        return alteredState;
      }
      ```

- A `Reducer` takes the **current state** and the received action, creates and returns a **new state** based on them

<br>

### 3-4. Store

- In Redux, you create one **store** per application
- The store contains the **current app state** and the **reducer**, along with several built-in functions

<br>

### 3-5. Dispatch

- dispatch is one of the **built-in functions of the store**

- dispatch serves the role of **triggering an action**

  - An action is passed as a parameter to the dispatch function

    - ex)

      ```javascript
      dispatch (action)
      ```

- When dispatch is called, the store executes the reducer, and if there is logic to handle that action, it creates a new state based on that action

<br>

### 3-6. Subscribe

- subscribe is also one of the **built-in functions of the store**, like dispatch
- If you pass a specific function to the subscribe function, that **passed function is called** every time an action is dispatched
- You can subscribe to the redux store's state using the `connect` function or `useSelector` Hook provided by the `react-redux` library

<br>

<br>

## 4. Three Principles

You must follow these 3 fundamental principles when using Redux

<br>

### 4-1. Single source of truth

- One application should create and use only one store
  - It is possible to use multiple stores, but it is not recommended!

<br>

### 4-2. State is read-only

- In React, when you need to update state, you use `setState`, and when you need to update an array, instead of pushing directly to the array, you use functions like `concat` to create a **new array** and **replace** it without modifying the existing array
- Similarly in Redux, by creating a **new state** to update rather than changing the existing state,
  - Later, you can go back or forward using developer tools
- The reason **immutability** must be maintained in Redux is that internally it performs [shallow equality](https://redux.js.org/docs/faq/ImmutableData.html#how-redux-uses-shallow-checking) checks to detect data changes
  - This allows detecting changes in objects by performing a **surface-level** comparison rather than comparing deep inside the objects, enabling good performance

<br>

### 4-3. Changes are made with pure functions

- You should create `pure functions` while keeping the following 3 points in mind
  - Reducer functions take the **previous state** and **action object** as parameters
  - The **previous state** should never be touched; instead, create a **new state object** with the changes and return it
  - A reducer function called with the same parameters must **always** return the same result
