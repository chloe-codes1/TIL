# Http Stateless

<br>

- HTTP generally operates in a connectionless manner
  - It connects to the server, sends a request, receives a response, and then disconnects
- By default, one connection is created for each resource
- `Advantages`
  - It is suitable for services targeting an unspecified large number of users
  - Even if hundreds of thousands of users are using a web service, connection maintenance can be kept to a minimum, allowing more user requests to be processed
- `Disadvantages`
  - Since it disconnects, the previous state of the client cannot be known
    - This characteristic is called `Stateless`, and it can be considered a characteristic derived from Connectionless
  - If the client's previous state information cannot be known, it immediately causes problems for web services
    - ex) Even if the client successfully logged in before, the login information cannot be maintained
    - HTTP solves this problem using Cookies!
