# Introduction to Node.js

<br>

<br>

#### Reasons to learn Node.js

1. Allows you to build complex & powerful applications without writing complex code
2. Well suited to build **microservices**

3. Can be used for more than just web development
4. A robust project that won't be going anywhere

<br><br>

### What is Node.js?

> JavaScript runtime environment

<br>

- A server-side platform built on Google Chrome's JavaScript Engine (V8 Engine)
  - A JavaScript runtime built with Chrome V8 Engine
- Lightweight and efficient due to its event-based non-blocking I/O model
- `npm`, the package ecosystem of Node.js, is the world's largest **open source library**

<br>

#### Node is NOT a Web Server

- Node itself does nothing!

  - Unlike Apache web server, there is no configuration to specify HTML file paths and open servers!
  - but, you need to write the **HTTP Server** yourself (using a library)

- Node.js is merely a **JavaScript Runtime** - just a way to execute code!

  ```javascript
  Node.js == Runtime Environment + JavaScript Library
  ```

<br>

<br>

### Features of Node.js

<br>

#### 1. Asynchronous I/O Processing & Event Driven

- All APIs of the Node.js library are asynchronous, meaning they are non-stopping (**Non-blocking**)
- A Node.js-based server does not wait for the API to return data when executed, but moves on to execute the next API
- The result value from the previously executed API is received through Node.js's notification mechanism of Events

<br>

#### 2. Fast Speed

- Provides fast code execution using Google Chrome's V8 JavaScript engine

<br>

#### 3. Single Threaded, but highly scalable

- Node.js uses a single thread model with an event loop
- The event mechanism allows the server to respond without blocking, increasing **server scalability**
  - In contrast, typical web servers like Apache create a limited number of threads to handle requests
- Node.js uses only one thread and can handle far more requests than web servers like Apache!

<br>

#### 4. No buffering

- Node.js applications have no data buffering and output data in chunks

#### 5. License

- MIT License is applied

<br>

<br>

### Who Uses Node.js?

Following is the link on github wiki containing an exhaustive list of projects, application and companies which are using Node.js. This list includes eBay, General Electric, GoDaddy, Microsoft, PayPal, Uber, Wikipins, Yahoo!, and Yammer to name a few.

- [Projects, Applications, and Companies Using Node](https://github.com/joyent/node/wiki/projects,-applications,-and-companies-using-node)

<br>

<br>

### Where to Use Node.js?

> Node.js is highly efficient in the following areas!

<br>

- I/O-intensive applications
- Data streaming application
- Data Intensive Real-time Applications (DIRT)
- JSON APIs based Applications
- Single Page Applications

<br>

<br>

### Where Not to Use Node.js?

- Node.js is not recommended for CPU-intensive applications.

<br>
