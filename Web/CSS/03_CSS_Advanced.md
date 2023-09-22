# CSS Advanced

<br>

### Emnet Tips

<br>

- `+ 인접, > 자식, * 개수`
  - a+ul>li*3
  - a+ul.nav-items>li.nav-item*3

<br>

- `link:css`
  - link tag 만들어줌

<br>

- `line-height`
  - 한줄 text일 때 수직 가운데 정렬

<br>

- `display: flex`
  - container와 자식요소가 item으로 구성됨

<br>

<br>

### Layout Tips

1. `Box model`

   - 모든 요소를 네모네모로 생각해라!

2. `position: absolute;`

   - 어딘가의 끝에 올리고 싶으면 **absolute**
   - Side에 놓고 싶으면 **flex**

3. `flex`

   - **부모 요소 (container)**

     - `display: flex;` 가 적용된 것
     - inline, block이 적용되지 않음

   - **자식 요소(item)**

   - **main axis**

     - `justify-content`

   - **cross axis**

     - `align-items`

       : 수직 정렬에 주로 사용

4. `rem`

   : 일반적인 browser는 16px

5. `box-sizing: border-box;`

6. `margin: 상하 / 좌우;`

<br>

<br>
