# Bootstrap

> An open source toolkit for developing with HTML, CSS, and JS. 

<br>

<br>

초기화 확인

: bootstrap.reboot



<br><br>

### Bootstrap CDN 사용하기

<br>

#### CDN 

> Content Delivery (Distribution) Network

- Content (CSS, JS, Image, Text 등)을 효율적으로 전달하기 위해 여러 node 에 가진 Network에 Data를 제공하는 시스템
- 개별 end-user의 가까운 서버를 통해 빠르게 전달 가능

- Web 상에 CSS code가 들어가 있는 것!

<br>

<br>

### Utility

<br>

#### 1-1. Spacing

Where *property* is one of:

- `m` - for classes that set `margin`
- `p` - for classes that set `padding`

Where *sides* is one of:

- `t` - for classes that set `margin-top` or `padding-top`
- `b` - for classes that set `margin-bottom` or `padding-bottom`
- `l` - for classes that set `margin-left` or `padding-left`
- `r` - for classes that set `margin-right` or `padding-right`
- `x` - for classes that set both `*-left` and `*-right`
- `y` - for classes that set both `*-top` and `*-bottom`
- blank - for classes that set a `margin` or `padding` on all 4 sides of the element

Where *size* is one of:

- `0` - for classes that eliminate the `margin` or `padding` by setting it to `0`
- `1` - (by default) for classes that set the `margin` or `padding` to `$spacer * .25`
- `2` - (by default) for classes that set the `margin` or `padding` to `$spacer * .5`
- `3` - (by default) for classes that set the `margin` or `padding` to `$spacer`
- `4` - (by default) for classes that set the `margin` or `padding` to `$spacer * 1.5`
- `5` - (by default) for classes that set the `margin` or `padding` to `$spacer * 3`
- `auto` - for classes that set the `margin` to auto

<br>

ex)

```css
.mt-0 {
  margin-top: 0 !important;
}

.ml-1 {
  margin-left: ($spacer * .25) !important;
}

.px-2 {
  padding-left: ($spacer * .5) !important;
  padding-right: ($spacer * .5) !important;
}

.p-3 {
  padding: $spacer !important;
}
```



- 브라우저 기본 rem = 16px



Bootstrap ver4 부터 flex 개념 등장



#### BEM

- 1naming 