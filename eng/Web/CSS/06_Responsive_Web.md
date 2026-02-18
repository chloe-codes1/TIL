# Responsive Web

<br>

<br>

### What is Responsive Web Design?

- Making a website readable by changing the width or layout according to the resolution so that users can use the website comfortably regardless of which device they use to visit
  - Building one website that provides an optimized website for the screen resolution of various devices

<br>

![the adaption to different devices](http://magazine.magix.com/en/wp-content/uploads/sites/3/2017/11/responsive-webdesign.jpg)

<br>

### 1. viewport meta tag

- `viewport` refers to the visible area of a web page

  - The viewport varies depending on the device
  - Using the viewport, you can provide an optimized web page to users of various devices by considering the characteristics and screen size of the device

- `meta tag` is used to deliver metadata to the browser or search engines for **Search Engine Optimization (SEO)**

  - The viewport meta tag provides information related to the browser's display settings

    | Property      | Description                      | Usage               |
    | :------------ | :------------------------------- | :------------------ |
    | width         | viewport width (px). Default: 980px | width=240           |
    |               |                                  | width=device-width  |
    | height        | viewport height (px)                | height=800          |
    |               |                                  | width=device-height |
    | initial-scale | viewport initial scale                | initial-scale=1.0   |
    | user-scale    | Zoom in/out availability              | user-scale=no       |
    | maximum-scale | viewport maximum scale               | maximum-scale=2.0   |
    | minimum-scale | viewport minimum scale               | minimum-scale=1.0   |

  - The *px* unit is used in meta tags, and the unit expression is omitted
  - When using multiple properties, separate them with commas (,)

  ex)

  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1.0"
  ```

  - The most common viewport setting
  - Setting the horizontal width to match the device width and the initial screen scale to 100%

<br>

<br>

### 2. @media

- Enables specifying different styles for different media types (print, screen, etc.)
- A core technology used in Responsive Web
- Specifying styles for each media using `@media` is called a Media Query.
  - Can distinguish not only the device but also the size and ratio of the device

<br>

> Example of specifying different styles for normal screen and print devices

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    @media screen {
      * { color: red; }
    }
    @media print {
      * { color: blue; }
    }
  </style>
</head>
<body>
  <h1>@media practice</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
</body>
</html>
```

<br>

> Media Query Syntax

```css
@media not|only mediatype and (expressions) {
  CSS-Code;
}
```

<br>

> Media Query Example

```css
@media screen and (min-width: 480px) {
  body {
    background-color: lightgreen;
  }
}
```

<br>

| Property            | Description                                              |
| :------------------ | :------------------------------------------------------- |
| width               | viewport width (px)                                        |
| height              | viewport height (px)                                        |
| device-width        | Physical width of the device (px)                               |
| device-height       | Physical height of the device (px)                               |
| orientation         | Device orientation (landscape: horizontal, portrait: vertical) |
| device-aspect-ratio | Physical width/height ratio of the device                      |
| color               | Maximum color bit depth the device can display                |
| monochrome          | Bits per pixel for monochrome devices                           |
| resolution          | Device resolution                                          |

<br>

#### Bootstrap Media Query

```css
// Extra small devices (portrait phones, less than 576px)
// No media query for `xs` since this is the default in Bootstrap

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```

<br>

<br>

## Bootstrap - Layout

<br>

### Grid System

> Bootstrap's grid system uses a series of containers, rows, and columns to layout and align content.
>
> It's built with [flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox) and is fully responsive.

<br>

- The Grid System is a method for composing balanced layouts, and in Bootstrap, you can freely compose responsive layouts.

<br>

Grid System Breakpoint

![image-20200324143533492](../../../kor/Web/images/image-20200324143533492.png)

<br>

- **break point**
  - `.col`, `.col-sm`, `.col-md`, `.col-lg`, `.col-xl`

- `.container`
  - To use Bootstrap's grid system, a `.container` must always exist as a parent
  - `.container`
  - `.container-fluid`
- `.row`
  - Composed of 12 columns
  - `.col - {breakpoint} - {number}`

<br>

#### 12 column grid

: Bootstrap uses 12 columns because 12 is a flexible number for division

<br>

#### Mix and match

> Don't want your columns to simply stack in some grid tiers? Use a combination of different classes for each tier as needed.

<br>

ex)

```html
<!-- Stack the columns on mobile by making one full-width and the other half-width -->
<div class="row">
  <div class="col-12 col-md-8">.col-12 .col-md-8</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
</div>

<!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
<div class="row">
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
</div>

<!-- Columns are always 50% wide, on mobile and desktop -->
<div class="row">
  <div class="col-6">.col-6</div>
  <div class="col-6">.col-6</div>
</div>
```

<br>

#### Gutters

- Padding values between items

- Can be removed using `.no-gutters`!

```css
.no-gutters {
  margin-right: 0;
  margin-left: 0;

  > .col,
  > [class*="col-"] {
    padding-right: 0;
    padding-left: 0;
  }
}
```

<br>

#### Offsetting columns

<br>

- Move columns to the right using `.offset-md-*` classes

```html
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 offset-md-4">.col-md-4 .offset-md-4</div>
</div>
<div class="row">
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
</div>
<div class="row">
  <div class="col-md-6 offset-md-3">.col-md-6 .offset-md-3</div>
</div>
```

- In addition to column clearing at responsive breakpoints, you may need to reset offsets
  - `.offset-md-0`

```html
<div class="row">
  <div class="col-sm-5 col-md-6">.col-sm-5 .col-md-6</div>
  <div class="col-sm-5 offset-sm-2 col-md-6 offset-md-0">.col-sm-5 .offset-sm-2 .col-md-6 .offset-md-0</div>
</div>

<div class="row">
  <div class="col-sm-6 col-md-5 col-lg-6">.col-sm-6 .col-md-5 .col-lg-6</div>
  <div class="col-sm-6 col-md-5 offset-md-2 col-lg-6 offset-lg-0">.col-sm-6 .col-md-5 .offset-md-2 .col-lg-6 .offset-lg-0</div>
</div>
```

<br>

### @media

> Think of it as a conditional statement!

<br>

```css
@media (min-width: 576px) {
  .container {
    max-width: 540px;
  }
}
```

<br>

#### viewport min width device

<br>

<br>

### Tips

- Looking at the Bootstrap description
  - It says *Build responsive, **mobile-first** projects on the web with the world's most popular front-end component library*
  - Think from small -> large
- height is affected by the content and child elements!
