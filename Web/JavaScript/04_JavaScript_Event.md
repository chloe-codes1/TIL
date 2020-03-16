# JavaScript Event

<br><br>

### addEventListener

- EventTarget.addEventListener (type, listener, [, useCapture]);
  - type: 이벤트 유형
  - listener: 이벤트 발생 시 실행할 callback 함수 (event handler)
  - useCapture: 기본 값 (false), 상위 노드로 전파 (bubbling), 만약 true 인 경우 하위 node로 전파 (capturing)

<br>

<br>

### Event 전파

- Event는 해당 요소에서 전파되며, capturing과 bubbling으로 구분된다
- 항상 capturing 부터 시작하여 bubbling으로 종료된다
- addEventListener method의 세 번째 인자인 **userCapture** (false 가 default)를 통해 특정 상황에 대한 이벤트 관리가 가능하다

<br>

<br>

### Event 객체와 this

: Event listener의 callback 함수에서 this를 활용하는 경우 event listener에 binding 되어 있는 요소가 지정된다