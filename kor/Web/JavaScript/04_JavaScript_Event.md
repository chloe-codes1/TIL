# JavaScript Event

<br><br>

### Event 의 이해

<br>

#### Event model

: Event handler와 event API 정의

- Web browser와 시기별로 3가지의 다른 event model 존재

  - why? 
    - web browser의 종류에 따라 변화되고 개선

- Event model의 종류

  - 기본 이벤트 모델 (Original event model)

    - 오래된 모델 
    - IE 8 이하와 호환 안됨
    - 기술적으로 부족 
    - DOM Level 0 event model

  - 표준 이벤트 모델 (Standard event model)

    - 현재 IE 9 이상과 다른 모든 web browser에서 지원
    - DOM Level 2 event model

  - 인터넷 익스플로러 이벤트 모델 (Internet Explorer event model)

    - IE 8 이하에서만 사용 가능한 모델
    - 다른 web browser에서 지원하지 않음
    - 더 이상 사용 안함

    

<br>

<br>

### `.addEventListener()`

: DOM 객체에 event handler 함수를 적용

- EventTarget.**addEventListener** (type, listener, [, useCapture]);
  - **type**: 이벤트 유형
  - **listener**: 이벤트 발생 시 실행할 callback 함수 (event handler)
  - **useCapture**: 기본 값 (false), 상위 노드로 전파 (bubbling), 만약 true 인 경우 하위 node로 전파 (capturing)

<br>

<br>

#### `preventDefault()`

: Event 기본 기능 작동을 막음



<br><br>

### `.removeEventListener()`

: Event handler 제거

- 짝이되는 `addEventListener()` 와 똑같은 세가지 인자를 가지고 있어야함

<br>

<br>

### Event 전파

<br>

#### Event 전파의 3단계

1. document node에서 event 발생 node까지 내려가면서 event 전파
2. event 발생 node
3. event 발생 node에서 document node까지 올라가면서 event 전파

<br>

#### `.stopPropagation()`

: 이벤트 전파를 막는 이벤트 API

<br>



- Event는 해당 요소에서 전파되며, capturing과 bubbling으로 구분된다
- 항상 capturing 부터 시작하여 bubbling으로 종료된다
- addEventListener method의 세 번째 인자인 **userCapture** (false 가 default)를 통해 특정 상황에 대한 이벤트 관리가 가능하다

<br>

<br>

### Event 객체와 this

: Event listener의 callback 함수에서 this를 활용하는 경우 event listener에 binding 되어 있는 요소가 지정된다

<br>

#### this와 target

- Event handler가 호출하는 함수의 this의 역할

  : 이벤트가 발생한 객체

- **event.target == this**
