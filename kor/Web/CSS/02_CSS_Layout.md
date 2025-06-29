# CSS Layout

<br>

<br>

#### Table of Contents

- 다단 레이아웃
  - position
  - display
  - float
- 네비게이션
  - 이미지 버튼
  - 텍스트 네비게이션
- animation, transition
  - 요소의 변형
  - 요소 클리핑

### CSS Position

<br>

#### static

: default 값 (기준 위치)

- 기본적인 요소의 배치 순서에 따름 (좌측 상단)
- 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치된다

ex)

```css
div { 
    height: 100px;
    width: 100px;
    background-color: #9775fa;
    line-alight: center;
    display: inline-block;
}
```

- div 는 block 속성
  - width 가 100px이므로  화면에서 100px가 뺀 만큼 margin으로 붙는다!!

<br>

#### relative

: 상대위치

```css

```

<br>

#### absolute

: 절대위치

- 기준
  - 부모 (조상요소) 중에 static이 아닌 것을 기준으로 한다
  - 본인 뿐만 아니라 다른 형제들의 위치에도 영향을 미친다!
    - 사용 시 주의할 것!

```css

```

<br>

#### fixed

: 절대위치

```css
.fixed {
    position: fixed;
    bottom: 0;
    right: 0;
}
```

<br>

<br>

### CSS Float

<br>

#### CSS float 속성

- float은 요소를 일반적인 흐름 (normal flow)에서 벗어나도록 하는 속성 중 하나
  - 반드시 clear 속성을 통해 초기화가 필요하며, 예상치 못한 상황이 발생할 수 있음
- `float`을 사용하는 경우 `block` 사용을 뜻하며 `display` 값이 `inline`인 경우 block으로 계산

<br>

#### float이 발생시키는 문제
