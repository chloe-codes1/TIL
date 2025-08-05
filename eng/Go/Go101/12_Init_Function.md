# Init Function

> Let's learn about Go's init() function

<br>

<br>

### init() function

- `init()` function looks similar to main function, but doesn't take arguments or return values
- `init()` function is the first function called when a package is loaded
  - Use it when you need package initialization logic!

<br>

<br>

### When is the `init()` function run?

It executes in the order: `import` --> `const` --> `var` --> `init()`

![](../../../kor/images/go_init_function.png) 
