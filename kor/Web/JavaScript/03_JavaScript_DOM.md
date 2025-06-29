# JavaScript DOM (Document Object Model)

<br>

<br>

### DOM

: Client side JavaScript의 핵심

- web browser와 web 문서의 내용 객체화
  - 각가의 객체는 property로 정보를 읽거나 설정 가능
- web browser창의 위치를 앍고 싶다면?
  - window 객체의 창의 위치를 알려주는 property를 읽어오면 됨

<br>

#### DOM 레벨과 혼란

- 최근 DOM은 정리되고, 표준화됨
  - 레벨 0부터 최신 레벨까지 있음

<br>

<br>

### DOM 의 구성

: 객체화 -> 구조화 -> 계층으로 구성됨

- 현재 web browser window

  - #### `Window 객체`

    - DOM 문서를 표현하는 창
    - 가상 최상위 객체
    - window 객체는 전역 객체
    - 다양한 함수, 이름공간, 객체 등이 포함

  - #### `Document 객체`

    - 페이지 콘텐츠의 진입점 역할
    - `<body>` 등 다른 요소들을 포함

- Web browser는 web 문서를 보여주는 창이 DOM의 기준

  - Window 객체 이외의 객체는 Window 객체의 property로 접근한다!

- Document 객체에 접근하고자 한다면

  - window 객채의 document property 이용
  - window 객체의 document property는 Document 객체를 가리킴
    - Document 객체는 web 문서, web 문서상의 HTML 요소 일부에 접근 가능함!

<br>

<br>

### Window의 생성

- 생성
  - window 객체의 `open method` 사용
- 창 닫기
  - window 객체의 `close method` 사용

<br>

#### `alert`

- 경고 상자 생성

- debugging용으로 주로 사용

<br>

<br>

### Web 문서 접근

<br>

#### getElementByID(id)

- 하나의 node로 return
- 이것 외에는 다 유사 배열 형태로 return 

<br>

#### querySelector()

- CSS Selector를 이용하여 node를 선택하지만, 일치되는 첫 번째 node 만을 return 함

<br>

#### querySelectorAll()

- CSS Selector를 이용하여 node를 선택함
- 일치하는 모든 node를 array로 return

<br>

<br>

### DOM 조작

<br>

#### Node의 종류에 따라 할 수 있는 것들

- 요소 속성이나 CSS 속성 변경
- 입력 폼의 값을 읽거나 변경
- 문서 내에 새로운 HTML 요소와 content 삽입

<br>

#### `document.write()`

- 함수 내부에 사용하여 이벤트로 호출 했을 때
  - 기존 문서 전체를 지워버리고, content를 출력함

<br>

#### `appendChild()`

: 특정 node의 자식으로 node를 삽입하기 위해 사용

- 자식 요소들 중 기존 요소들 끝에 삽입됨

<br>

#### `insertBefore()`

: 특정 요소 앞에 삽입하기 위해 사용

- 사용 방법
  - 부모 node.**insertBefore**(삽입할 node, reference node)

<br>

#### `replaceChild()`

: 자식 node 중 특정 node를 새로운 node로 치환하는 역할

- 사용 방법
  - 부모 node.**replaceChild**(새로운 node, 바뀔 node)

<br>

#### `getAttribute()`, `setAttribute()`

: node의 속성 값을 가져오고, node의 속성을 속성 값으로 설정

- 사용 방법
  - node.**getAttribute**("속성명")
  - node.**setAttribute**("속성명", "속성값")

<br>

#### `innerHTML`, `insertAdjacentHTML`

- DOM 조작 시 사용 가능한 method들
- `createElement()`, `createTextNode()`, `appendChild()`를 한꺼번에 처리하는 효과
- 사용방법
  - element.**innerHTML**(text)
  - element.**insertAdjacentHTML**(positon, text)
    - position으로 삽입 위치 지정도 가능함

<br>

<br>