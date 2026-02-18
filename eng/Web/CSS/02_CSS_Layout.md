# CSS Layout

<br>

<br>

#### Table of Contents

- Multi-column layout
  - position
  - display
  - float
- Navigation
  - Image buttons
  - Text navigation
- animation, transition
  - Element transformation
  - Element clipping

### CSS Position

<br>

#### static

: Default value (reference position)

- Follows the basic element placement order (top left)
- When placed inside a parent element, it is positioned relative to the parent element

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

- div has block property
  - Since width is 100px, the remaining screen space after 100px is filled with margin!!

<br>

#### relative

: Relative position

```css

```

<br>

#### absolute

: Absolute position

- Reference
  - Based on the nearest ancestor element that is not static
  - Affects the position of not only itself but also other siblings!
    - Use with caution!

```css

```

<br>

#### fixed

: Absolute position

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

#### CSS float property

- float is one of the properties that takes an element out of the normal flow
  - Must be reset through the clear property, and unexpected situations may occur
- Using `float` implies using `block`, and if the `display` value is `inline`, it is calculated as block

<br>

#### Problems caused by float
