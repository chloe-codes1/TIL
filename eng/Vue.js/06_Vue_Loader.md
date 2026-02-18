# Vue Loader

> <https://vue-loader-v14.vuejs.org/kr/features/scoped-css.html>

<br>

<br>

## Scoped CSS

> When the `<style>` tag has the scoped attribute, the CSS applies only to elements of the current component

<br>

### `scoped` option

- The scoped option only affects the current component
  - However, you should still specify a **class**
    - This makes it faster!
      - why?
        - Due to the way browsers render CSS selectors, not specifying a class causes a full traversal

<br>

### Local style and global style

- You can use both `scoped` style and non-scoped style simultaneously within a single component

  ex)

  ```html
  <style>
  /* global styles */
  </style>

  <style scoped>
  /* local styles */
  </style>
  ```

<br>

### Root element of Child component

- When using the `scoped` attribute, the parent component's styles do not affect child components
  - However!
    - The child component's root node IS affected!
      - This is for the purpose of setting layout by modifying the root element of the child component

<br>

### Deep Selectors

#### `>>>` Combinator

- If you want to affect child components while using `scoped` styles, you can use the `>>>` combinator

  ex)

  ```html
  <style scoped>
  .a >>> .b { /* ... */ }
  </style>
  ```

<br>

### `v-html` and `scoped` style

- `v-html` is not affected by `scoped` styles
  - but, you can style it using a deep selector (e.g., the `>>>` combinator shown above)

<br>

<br>

`+`

### `v-html` vs `v-text`

: Think of it as the difference between **innerHTML** and **innerText**!

<br>

<br>

### What is lazy load?

- A component only sends a call when it is actually used
  - Much more economical!
- Used when fast loading is needed
- Set lazy loading for pages that are rarely visited!
  - ex) Customer service page
