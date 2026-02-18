# Access Modifiers

<br>

<br>

### Access Modifiers

<br>

#### Public

: Allows all access

#### Protected

: Allows access only to objects in the same package (folder) and objects in an inheritance relationship

#### Default

: Allows access only to objects in the same package (folder)   => same package

#### Private

: Allows access only within the current object   => same class

<br><br>

### Access Restriction

- By using access restriction, data (instance variables) is blocked from direct external access, and the operations that can modify or act on the data are kept internal.
  - This way, the outside cannot know what changes are happening internally, and can only receive results through methods

    => Information hiding is possible

  <br>

![img](https://lh4.googleusercontent.com/YtBtKe9qZKtVHKwHfBag3a5UgEdOXqXK1o7USx3p3-F59NIYFUZ1lF0Ph5EhY1POdQDsR6wD5p1y3lRi5JJvxzUsfbjsXwnYwAo8--yfw3s5ErluAz98YqvDisESvdeAKsBByZQ8)

<br><br>

`+`

#### Getters Setters method

: two conventional methods that are used for retrieving and up-dating value of a variable.

- In Eclipse, use the top menu: source - Generate Getters Setters method

- Only for boolean types, it is is___ instead of set___!
