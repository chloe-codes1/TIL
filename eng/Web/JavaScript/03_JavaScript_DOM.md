# JavaScript DOM (Document Object Model)

<br>

<br>

### DOM

: The core of client-side JavaScript

- Objectification of the web browser and web document content
  - Each object can read or set information through properties
- Want to know the position of the web browser window?
  - Read the property of the window object that tells the window position

<br>

#### DOM Levels and Confusion

- Recently, DOM has been organized and standardized
  - Ranges from level 0 to the latest level

<br>

<br>

### Composition of the DOM

: Objectified -> Structured -> Composed of layers

- Current web browser window

  - #### `Window Object`

    - The window displaying the DOM document
    - Virtual topmost object
    - The window object is a global object
    - Contains various functions, namespaces, and objects

  - #### `Document Object`

    - Serves as the entry point for page content
    - Contains `<body>` and other elements

- The web browser is a window that displays web documents, and it is the basis of the DOM

  - Objects other than the Window object are accessed as properties of the Window object!

- To access the Document object

  - Use the document property of the window object
  - The document property of the window object points to the Document object
    - The Document object can access the web document and some HTML elements within it!

<br>

<br>

### Window Creation

- Creation
  - Use the `open method` of the window object
- Close window
  - Use the `close method` of the window object

<br>

#### `alert`

- Creates an alert box

- Mainly used for debugging

<br>

<br>

### Web Document Access

<br>

#### getElementById(id)

- Returns as a single node
- Everything else returns in an array-like format

<br>

#### querySelector()

- Selects a node using a CSS Selector, but returns only the first matching node

<br>

#### querySelectorAll()

- Selects nodes using a CSS Selector
- Returns all matching nodes as an array

<br>

<br>

### DOM Manipulation

<br>

#### Things You Can Do Depending on the Type of Node

- Change element attributes or CSS properties
- Read or change input form values
- Insert new HTML elements and content into the document

<br>

#### `document.write()`

- When used inside a function and called through an event
  - It erases the entire existing document and outputs the content

<br>

#### `appendChild()`

: Used to insert a node as a child of a specific node

- Inserted at the end of existing child elements

<br>

#### `insertBefore()`

: Used to insert before a specific element

- Usage
  - parentNode.**insertBefore**(node to insert, reference node)

<br>

#### `replaceChild()`

: Replaces a specific child node with a new node

- Usage
  - parentNode.**replaceChild**(new node, node to be replaced)

<br>

#### `getAttribute()`, `setAttribute()`

: Gets the attribute value of a node, and sets the node's attribute to an attribute value

- Usage
  - node.**getAttribute**("attribute name")
  - node.**setAttribute**("attribute name", "attribute value")

<br>

#### `innerHTML`, `insertAdjacentHTML`

- Methods that can be used for DOM manipulation
- Has the effect of processing `createElement()`, `createTextNode()`, `appendChild()` all at once
- Usage
  - element.**innerHTML**(text)
  - element.**insertAdjacentHTML**(position, text)
    - Position can also specify the insertion location

<br>

<br>
