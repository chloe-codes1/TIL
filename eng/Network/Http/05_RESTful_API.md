# RESTful API

> What is a RESTful API?

<br>

### REST Characteristics

- `Client-server architecture`
  - The client handles user-related processing,
  - The server provides REST APIs,
  - Allowing `roles` to be clearly `distinguished` and operate `separated` with a `consistent interface`
- `Statelessness (stateless)`
  - REST is `stateless` because it leverages the characteristics of HTTP
  - The server does not need to remember `state information` to perform tasks; it only needs to process incoming requests, making implementation simple and straightforward
- `Cacheability (cacheable)`
  - Caching is required to efficiently handle large volumes of requests
  - Using caching improves response times and, since REST Server transactions do not occur, can improve overall response time, performance, and server resource utilization
- `Uniform interface (Uniform)`
  - An architecture that enables `manipulation` of resources identified by `URI` and can be used on `all platforms` as long as it follows the `Http standard`
  - In other words, **it is not dependent on any specific language or technology**

<br>

### Core Rules

- URIs should represent the resource information
- `Actions` on resources should be expressed using `HTTP Methods` (GET, POST, PUT, DELETE, etc.)

<br>

### What is a RESTful API?

> RESTful is a way to use REST properly, and it has not been officially published by anyone

- **Resources must be identifiable**
  - It should be possible to tell `what resource` is being controlled just from the URL
- **Actions must be explicit**
  - Using GET to perform UPDATE and DELETE -> X
