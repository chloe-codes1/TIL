# Redux

> Reference: [redux docs](https://redux.js.org/introduction/getting-started), [velopert](https://react.vlpt.us/redux/)

<br>

<br>

## 1. Redux 란?

- React 생태계에서 가장 사용률이 높은 상태관리 라이브러리
- Redux를 사용하면
  - 컴포넌트들의 상태 관련 로직들을 다른 파일들로 분리시켜서 더욱 효율적으로 관리 할 수 있으며
  - 글로벌 상태 관리도 손쉽게 할 수 있다

<br>

<br>

## 2. Redux vs Context API

Redux를 사용하는 것과 Context API의 차이

<br>

### 2-1. Middleware

- Redux에는 **middleware**라는 개념이 존재한다
  - Redux의 middleware를 사용하면 action object가 **reducer**에서 처리되기 전에 원하는 작업을 수행할 수 있다
    - ex)
      - 특정 조건에 따라 action이 무시되게 만들기
      - action을 console에 출력하기
      - action이 dispatch 되었을 때, 이것을 수정해서 reducer에 전달되게 만들기
      - 특정 action이 발생했을 때
        - 이것에 기반하여 다른 action이 발생되게 하기
        - 특정 JavaScript 함수를 실행하기
- Middleware는 주로 **비동기 작업**을 처리할 때 많이 사용된다

<br>

### 2-2. Useful Functions & Hooks

- `connect` 함수를 사용하면 redux의 상태 또는 action 생성 함수를 component의 props로 받아올 수 있다
- `useSelector`, `useDispatch`, `useStore` 과 같은 [Hooks](https://react-redux.js.org/api/hooks)를 사용하면 손쉽게 상태를 조회하거나 action을 dispatch 할 수 있다

<br>

### 2-3. Global State

- **Context API**를 사용해서 global state 를 관리할 때에는 일반적으로 기능별로 `Context`를 만들어서 사용했다면,
  - **Redux**는 모든 Global state를 하나의 커다란 object에 넣어서 사용하는 것이 필수이다
    - 이것을 통해 매번 `Context` 를 새로 만드는 불편함을 피할 수 있다!

<br>

<br>

## 3. Key Concepts

<br>

### 3-1. Action

- State에 어떤 변화가 필요할 때, action을 발생시킨다

- Action은 하나의 객체로 표현된다

  - ex)

    ```json
    {
      type: "VALUE"
    }
    ```

- Action 객체는 `type`을 필수로 가져야 하고, 그 외의 값들은 원하는대로 넣을 수 있다

  - ex)

    ```json
    {
      type: "TODO",
      data: {
        id: 0,
        text: "집 가기"
      }
    }
    ```

  - ex)

    ```json
    {
      type: "CHANGE_INPUT",
      text: "집에 가세요"
    }
    ```

<br>

### 3-2. Action Creator

- Action 생성 함수는 말 그대로 **aciton을 만드는 함수**다

- Parameter를 받아와서 action 객체 형태로 만들어준다

- ex)

  ```javascript
  export function addTodo(data) {
    return {
      type: "ADD_TODO",
      data
    };
  }
  
  // Arrow function도 가능!
  export const changeInput = text => ({ 
    type: "CHANGE_INPUT",
    text
  });
  ```

- `Action Creater` 를 사용하는 이유는 나중에 component에서 action을 쉽게 발생시키기 위해서다
  - 그래서 보통 `export` keyword 붙여서 다른 file에서 해당 함수를 불러내서 사용한다
- Redux에서 `Action Creater` 사용이 필수는 아니다!
  - Action을 발생시킬 때마다 action 객체를 작성해서 쓸 수도 있다

<br>

### 3-3. Reducer

- Reducer는 **변화를 일으키는 함수**다

- 두 가지 parameter를 받아온다

  - `state`

  - `action`

    - ex)

      ```javascript
      function reducer(state, action) {
        // Update status
        return alteredState;
      }
      ```

- `Reducer`는 **현재 상태**와 전달 받은 action을 참고하여 **새로운 상태**를 만들어서 return한다

<br>

### 3-4. Store

- Rexux에서는 한 application당 하나의 **store**를 만들게 된다
- Store 안에는 **현재의 app 상태**와 **reducer**가 들어가있고, 거기에 몇가지 내장 함수들이 있다

<br>

### 3-5. Dispatch

- dispatch는 **store의 내장 함수** 중 하나다

- dispatch는 **action을 발생 시키는 역할**을 한다

  - dispatch 함수에는 action을 parameter로 전달한다

    - ex)

      ```javascript
      dispatch (action)
      ```

- dispatch를 호출하면 store는 reducer를 실행시켜서 해당 action을 처리하는 logic이 있다면, 그 action을 참고하여 새로운 상태를 만들어준다

<br>

### 3-6. Subscribe

- subscribe도 dispatch처럼 **store의 내장 함수** 중 하나이다
- subscribe 함수에 특정 함수를 전달해주면,  action이 dispatch 되었을 때 마다 **전달한 함수가 호출**된다
- `react-redux` 라는 library에서 제공하는 `connect` 함수 또는 `useSelector` Hook을 사용하여 redux store의 상태에 subscribe 한다

<br>

<br>

## 4. Three Principles

Redux를 사용할 때 3가지 fundamental principles를 지켜야한다

<br>

### 4-1. Single source of truth

- 하나의 application에는 단 한개의 store를 만들어서 사용한다
  - 여러개의 store를 사용하는 것도 가능은 하지만 권장되지 않는다!

<br>

### 4-2. State is read-only

- React에서 state를 update 해야 할 때, `setState`를 사용하고, array를 update 해야 할 때는 array 자체에 push하지 않고 `concat` 같은 함수를 사용하여 기존 array는 수정하지 않고 **새로운 array**를 만들어서 **교체**하는 방식으로 update한다
- Redux에서도 이와 마찬가지로, 기존의 state는 변경하지 않고 **새로운 state**를 생성하여 update해주는 방식으로 해주면,
  - 나중에 개발자 도구를 통해서 뒤로 돌릴 수도 있고, 다시 앞으로 돌릴 수도 있다
- Redux에서 **immutability**를 유지해야 하는 이유는 내부적으로 data가 변경되는 것을 감지하기 위하여 [shallow equality](https://redux.js.org/docs/faq/ImmutableData.html#how-redux-uses-shallow-checking)   검사를 하기 대문이다
  - 이것을 통해 객체의 변화를 감지 할 때 객체의 깊숙한 안쪽까지 비교를 하는 것이 아니라 **겉핥기 식**으로 비교를 하여 좋은 성능을 유지할 수 있다

<br>

### 4-3. Changes are made with pure functions

- 아래의 3가지 사항을 주의하여 `pure function`을 만들야 한다
  - Reducer 함수는 **이전 상태**와 **action 객체**를 parameter로 받는다
  - **이전의 상태**는 절대로 건들이지 않고, 변화를 일으킨 **새로운 상태 객체**를 만들어서 return한다
  - 똑같은 parameter로 호출된 reducer 함수는 **언제나** 똑같은 결과값을 return해야 한다
