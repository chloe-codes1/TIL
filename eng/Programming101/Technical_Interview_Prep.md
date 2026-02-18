# Technical Interview Prep

> Let's get that job offer!

<br>

<br>

## 1. Spring Class: `Helper Class (Util Class)`?

> Wikipedia
>
> : In object-oriented programming, a helper class is used to assist in providing some functionality, which isn't the main goal of the application or class in which it is used
>
> - Utility Class, also known as Helper class means that contains just static methods
> - Stateless & cannot be instantiated
> - Used to handle repetitive or commonly used functionalities with `Util Class`!

<br>

ex)

### 1-1. org.springframework.util.ClassUtils

#### boolean isPresent(String className, @Nullable ClassLoader classLoader)

Checks whether the class exists (you should not use [class].class.getName() - it will throw an error if the class doesn't exist)

```
boolean isPresent = ClassUtils.isPresent("org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter", null);
```

<br>

### 1-2. org.springframework.util.StringUtils

#### boolean isEmpty(@Nullable Object str)

Checks for String null and empty

```
StringUtils.isEmpty(stringValue);
```

#### boolean containsWhitespace(@Nullable String str)

Checks whether whitespace exists

#### String trimWhitespace(String str)

Removes leading and trailing whitespace

#### String replace(String inString, String oldPattern, @Nullable String newPattern)

Replaces all matching strings. Does not replace if newPattern is null

#### String delete(String inString, String pattern)

Deletes all matching strings

#### String getFilename(@Nullable String path)

Returns the file name from the path (returns the last string)

#### String delete(String inString, String pattern)

Deletes all matching strings

<br>

### 1-3. org.springframework.util.TypeUtils

#### boolean isAssignable(Type lhsType, Type rhsType)

Checks whether the type on the right is a subtype of the type on the left

<br>

<br>

`+`

#### Service Class vs Helper Class

- A Service class/interface provides a way of a client to interact with some functionality in the application. This is typically public, with some business meaning. For example, a `TicketingService` interface might allow you to `buyTicket`, `sellTicket` and so on.
- A helper class tends to be hidden from the client and is used internally to provide some boiler plate work that has no business domain meaning. For example, let's say you wanted to convert a date into a timestamp in order to save it to your particular datastore. You might have a utility class called `DateConvertor` with a `convertDateToTimestamp` method that performs this processing.

 <br>

## 2. What is MVC?

> - A methodology for development that separates roles into 3 forms
>   - One of the design patterns
>
> - It has the advantage of separating business processing logic from user interface elements, making it easier to develop them independently without affecting each other!

- **M**odel
  - Defines **what** the application will do
  - Responsible for handling internal business logic
  - ex) Algorithms being processed, DB, Data, etc
- **V**iew
  - Responsible for **displaying** something on the screen
  - Subordinate to the Controller, displays everything that the Model or Controller wants to show
  - Receives user input and updates the model's data
- **C**ontroller
  - Responsible for telling the Model **how** to process
  - In mobile, the **screen logic processing** part

<br>

#### Brief Summary

> Based on Django project

- M
  - Data  ex) models.py
- V (T)
  - UI  (html + js)
- C
  - Mediator between Data & UI   ex) views.py

<br>

<br>

## 3. CORS Policy

<br>

### Same-Origin Policy

- A **browser** security mechanism that restricts how documents or scripts loaded from one origin can interact with resources from another origin
- Criteria for determining same origin
  - `Protocol`
  - `Host`
  - `Port`

<br>

### Cross-Origin Resource Sharing(CORS)

> <https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS>

- A mechanism that uses additional HTTP headers to tell the browser to grant a web application running at one origin permission to access selected resources from a different origin
- A web application executes a CORS HTTP request when the resource has a different origin (Domain, Protocol, Port) from its own
  - A policy that allows data access from a different domain even for AJAX requests on the server side!

<br>

<br>

## 4. GET and POST Requests

<br>

### GET

- A method designed for querying information from the server

- Sends data through query strings rather than in the body

  - Query string

    - A request parameter consisting of name-value pairs appended to the URL with `?`

    - Multiple parameters are concatenated with `&`

      ex)

      ```
      https://movie-box1.herokuapp.com/movies/genre/?option=Fantasy
      ```

- Requests can be cached to limit unnecessary requests

- Idempotent

  - The same response must be returned even if the same request is sent to the server multiple times
    - Primarily used for queries

<br>

### POST

- A method designed for creating/modifying resources
- Sends data in the body
- Can send data without length restrictions
  - Unlike the GET method, large data transfers are possible!
- The data type of the request must be indicated in the Content-Type of the request header
- Non-idempotent
  - The response may always differ when the same request is sent to the server multiple times
  - Used when changing the state or data of the server
    - Can be used for create/update/delete, but primarily used as follows
      - Create - POST
      - Update - PUT or PATCH
      - Delete - DELETE

<br>

<br>

## 5. JSP's application class

> <https://gmlwjd9405.github.io/2018/11/03/jsp.html>

<br>

### What is JSP(Java Server Pages)?

- A server-side scripting language based on Java
  - A language that inserts Java code within HTML to dynamically generate web pages on the web server and returns them to the web browser

<br>

![JSP Architecture](https://iq.opengenus.org/content/images/2019/05/JSP-architecture.jpg)

<br>

### Key Classes of JSP

- Request
  - An object that provides request information sent by the client
- Response
  - An object representing the HTTP response to the client's request
- pageContext
  - A built-in object for a single page
- Session
- Application
  - An object for the web application serving the page
  - Holds and maintains information about the server

<br>

<br>

## 6. Session and Cookie

> Reference: <https://jeong-pro.tistory.com/80>

<br>

### Why Use Cookies and Sessions

: Used to compensate for the characteristics and weaknesses of the **`HTTP Protocol`**

<br>

1. Connectionless
   - When the client sends a request to the server, the server sends an appropriate response and then disconnects
2. Stateless
   - The moment the connection is severed, communication between client and server ends, and state information is not maintained

<br>

*Without cookies and sessions, you would have to log in again every time you navigate to a different page!*

<br>

### Cookie

- A small data file containing keys and values stored on the client's local machine
- Cookies contain name, value, expiration date (cookie storage period), and path information
- Cookies can store data for a certain period of time
  - Used for maintaining login state
- Cookies store the client's state information locally and reference it later
- Cookies are **automatically sent to the server** by the browser in the Request Header without the user making a separate request

<br>

**Cookie process**

1. Access a web page through the browser

2. While receiving the web page requested by the client, cookies are saved to the client's local (hard) drive

3. When the client makes another request, cookie values are sent along with the web page request

4. It appears as if login information is continuously maintained

<br>

**Cookie use cases**

- Auto-login
- Checking "Don't show this popup again today" in a popup
- Shopping cart in online stores

<br>

<br>

### Session

- A technology that views a series of requests coming from **the same browser** for a **certain period of time** as one state and **maintains that state**
  - The state maintained from the time of connecting to the web server through a web browser until the browser is closed

<br>

**Session process**

1. A session ID is issued when the client connects to the server

2. The server stores the issued session ID using a cookie on the client side (JSESSIONID)

3. When the client reconnects, it uses this cookie (JSESSIONID) to send the session ID value to the server
   - An ID is needed to distinguish sessions, and only that ID is stored using cookies (cookie usage)
   - Since cookies are automatically sent to the server, the server can process based on the session ID

<br>

**Session use cases**

: Maintaining login information

<br>

<br>

### Difference between `Session` and `Cookie`

|             | Session                                                      | Cookie                                                       |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Storage location | Server                                                  | Stored as a file on the client                               |
| Security    | Relatively secure because only the session ID is stored using cookies and the server processes based on it | Vulnerable to security because it is stored locally and can be altered or sniffed during requests |
| Life Cycle  | An expiration time can be set, but it is deleted when the browser is closed regardless of the expiration time | Although there is an expiration time, since it is stored as a file, information may persist even after the browser is closed. If the expiration period is set generously, it may persist until cookies are deleted |
| Speed       | Relatively slower because processing is required since information is on the server | Faster when making server requests because information is in the cookie |

<br>

<br>

## 7. SOLID Principles

> 5 Principles of Object-Oriented Design

- **S**RP (Single Responsibility Principle)
  - Single Responsibility Principle
    - A software design component (class, method, etc.) should have only one responsibility (function)
- **O**CP (Open-Closed Principle)
  - Open-Closed Principle
    - Should be designed so that functionality can be modified or added (open) without changing existing code (closed)
- **L**SP (Liskov Substitution Principle)
  - Liskov Substitution Principle
    - A child class must be able to perform the behaviors possible in the parent class
- **I**SP (Interface Segregation Principle)
  - Interface Segregation Principle
    - Multiple specific interfaces are better than one general interface
- **D**IP (Dependency Inversion Principle)
  - Dependency Inversion Principle
    - When forming dependency relationships, relationships should be formed with interfaces or abstract classes rather than concrete classes

<br>

<br>

## 8. What is Jenkins?

<br>

### Continuous Integration

- When adding code to a shared repository, it automatically **builds** the project, **tests** for errors and bugs, and notifies the developers of the results for safe development
  - Major tools for this
    - Jenkins
    - CircleCI

- Why it's needed
  - Since code is automatically tested before being committed to the repository, bugs are reduced and faster development becomes possible!
  - Since each developer's development environment may differ, testing code in a unified environment is essential!

<br>

<br>

## 9. Difference between JSON and XML

![](../kor/images/JSON_vs_XML.png)

<br>

#### Advantages of JSON

- XML documents are accessed using the XML DOM (Document Object Model)
  - JSON parses the received string directly
    - This provides faster processing speed than XML!
    - Widely used in web environments where fast responses are needed with HTML and JavaScript integration

<br>

#### Advantages of XML

- With JSON, the user must verify the integrity of received data themselves
  - XML is still widely used where data verification is needed, as it can validate data integrity using schemas

<br>

<br>

## 10. Overloading vs Overriding

- Overriding
  Redefining a method that exists in a parent class to suit the needs of a child class
- Overloading
  Creating a method that has the same name and return type as a parent class method but with different parameters
  - Allows the method to be called in various situations
