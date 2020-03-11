# CSS

<br>

<Br>

### Why CSS ?

: CSS (Cascading Style Sheets) 은 스타일을 정의한다

<b>

#### CSS 기본 사용법

```html
h2 {
color: blue;
font-size: 20px;
}
```

<br>

#### CSS 정의방법

1. In-line
2. 내부 참조
3. 외부 참조

<br>

<br>

### CSS Selelctor

기타 의사 클래스, 의사 앨리먼트 ...잘 알아보기

<br>

#### CSS Tip

: 되는 것 vs 하면 안되는 것을 잘 구분하기

<br>

<br>

### CSS 상속

- 속성 중에는 상속 되는것과 상속 않는 것이 있다
  - 상속 되는 것
    - Text 관련 요소 (front, color, text-align, opacity, visuality)
  - 상속 되지 않는 것
    - Positon 관련 요소 (position, top/right/bottom/left, z-index)

<br>

<br>

### CSS 적용 우선순위 (Cascading order)

- 중요도 (Importance) - 사용시 주의 (왜냐면 최강)

  - Important

    ```css
    h3 {
    	color: violet !important
    }
    ```

    

- 우선 순위 (Specificity)

  - in-line / id 선택자 / class 선택자 / **속성 선택자**, **Pseudo-class** / 요소 선택자
    - 나중에 정의된 것이 더 우선순위를 갖는다!

- Source 순서

<br>

<br>

### 크기단위

사진 참조



#### `em` vs `rem`

- em 
  - 자기가 갖을 수 있는 크기의 배수
  - 상속을 받아서 그 수에 대해 em
  - 24px 일때 1.5em == 36px
- rem (root em - root를 기준으로 함)
  - 기본적으로 browser pixcel size == 16px
  - 1.5 rem == 24px

<br>

<br>

### Box model

> 모든 html은 box model을 갖고있음

<br>



#### Box-sizing

- 기본적인 모든 요소의 box-sizing은

Tip!

```css
Box-sizing:border-box;
```

- margin 등등을 포함한

<br>

<br>

### display inline vs block

1. block
   - 화면 너비의 100%를 가짐
2. inline
3. inline-block
   - Block과 inline level 요소의 특징을 모두 갖는다
   - inline처럼 한 줄에 표시한다
   - 