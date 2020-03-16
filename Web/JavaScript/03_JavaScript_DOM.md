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

#### querySelector()



#### querySelectorAll()

<br>

<br>

### DOM 조작

<br>

#### `innerHTML`, `insertAdjacentHTML`

- DOM 조작 시 사용 가능한 method들
- 사용방법
  - element.innerHTML(text)
  - element.insertAdjacentHTML(positon, text)
    - position으로 삽입 위치 지정도 가능함

<br>

<br>