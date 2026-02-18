# Http Methods

> Characteristics of each Http method

<br>

- `GET`
  - Requests to retrieve a specific resource
  - GET requests should only be used when fetching data
- `POST`
  - Sends data to the server
  - The type of the Request Body is indicated by the `Content-Type` header
  - The difference between PUT and POST is idempotency; `PUT` has `idempotency`
    - PUT produces the same effect whether sent once or multiple times (no side effects)
  - Sends data to the server through the Message body
  - Primarily used when `creating` new resources
- `PUT`
  - Uses the request payload to `create a new resource` or `replace the data` representing the target resource
  - Has `idempotency`
- `PATCH`
  - Used when `partially modifying` a resource
  - Not idempotent
  - PATCH or POST may cause side-effects on other resources
- `DELETE`
  - Deletes the specified resource
- `HEAD`
  - Requests the Header that would be returned if a specific resource were requested with a GET method
  - Responses to a HEAD method must not have a Body, and even if a Body exists, it must be ignored
  - Used for health checks of web services or to obtain web server information
- `OPTIONS`
  - Used to set communication options with the target resource
- `TRACE`
  - Used for `loopback` testing
- `CONNECT`
  - A method that initiates `bidirectional communication` with the requested resource
    - Can be used to open a tunnel
  - ex) Can be used to access a web site using SSL (HTTPS)
    - The Client requests the HTTP proxy server to establish a TCP connection with the desired destination
    - The server then proceeds to create the connection on behalf of the client
    - Once the connection is established by the server, the proxy server continues to proxy the TCP stream going to and from the client
