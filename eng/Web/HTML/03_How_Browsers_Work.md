# How Browsers Work

> Back to basics!
>
> Reference: [How Browsers Work: Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

<br>

<br>

### Main Functions of the Browser

- The main function of the browser is to **request** the **resource** selected by the user from the server and **display** it in the browser
  - Resources are usually HTML documents, but can also be PDFs, images, or other formats
  - The address of a resource is determined by a **URI (Uniform Resource Identifier)**
- The browser interprets and displays HTML files according to the `specifications` of HTML and CSS
  - The specifications are established by **W3C (World Wide Web Consortium)**, the web standardization organization
  - In the past, browsers implemented only parts of these specifications and extended the rest in their own ways, causing serious **compatibility issues**, but currently most browsers follow the standard specifications

<br>

### Basic Structure of the Browser

![browser-components](../../../kor/Web/images/browser-components.png)

1. **User Interface**
   - Address bar, back/forward buttons, Bookmarks, etc.
   - All parts except the window that displays the requested page
2. **Browser engine**
   - Controls the actions between the `User Interface` and the `Rendering engine`
3. **Rendering engine**
   - Displays the contents requested by the user
     - ex) When HTML is requested, it parses HTML and CSS and displays them on screen
4. **Networking**
   - Used for network calls such as HTTP requests
5. **UI Backend**
   - Draws basic widgets
   - A generic interface not specified by the platform, using the OS user interface system
6. **JavaScript Interpreter**
   - Interprets and executes JS code
7. **Data Persistence**
   - A layer for storing data
   - All kinds of resources need to be saved to the hard disk, such as storing cookies
     - The HTML5 specification defines a `web database` supported by browsers

<br>

<br>

## The Rendering Engine

- The role of the Rendering Engine is to display requests on the browser screen
- The Rendering Engine can display `HTML`, `XML` documents and `images`
  - It can also display other types such as `PDF` using plug-ins or browser extensions

<br>

### Rendering Engines

The browsers covered in this article -- **Firefox**, **Chrome**, and **Safari** -- are built with two types of Rendering Engines

- **Firefox** uses the `Gecko` Engine made directly by Mozilla, and
- **Safari** and **Chrome** use the `Webkit` Engine
  - **Webkit** is an open source engine originally built to run on the Linux platform,
    - which Apple modified to support the Safari browser on Mac and Windows.

<br>

### The main flow

The Rendering Engine starts by obtaining the requested contents from the **Network layer**, and the document content is usually transmitted in 8kb chunks

![image-20201124005119156](../../../kor/Web/images/image-20201124005119156.png)

- The Rendering Engine **parses** the HTML document and converts `tags` into **DOM nodes** within the "**content tree**"
  - Then it also parses in-line style elements along with external CSS files
    - The style information and HTML display rules create another tree called the "**Render tree**"
- The **Render tree** contains rectangles with **visual attributes** such as colors or dimensions,
  - These are displayed on screen **in a defined order**
    - When the Render tree construction is complete, a **layout** process begins, which means each node is displayed at its exact position on the screen
- It is important to know that these processes progress **incrementally**!
  - The rendering engine tries to display content as **quickly** as possible for a better user experience, and it does not wait until all HTML is parsed but starts the **layout** and **painting** process
    - While waiting for the rest of the content to be transmitted from the network, it displays parts of the received content **first** on the screen

![image-20201124005950727](../../../kor/Web/images/image-20201124005950727.png)
