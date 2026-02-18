# Keep-Alive Header

<br>

### What is Keep Alive?

- In the HTTP protocol, it allows multiple requests and responses between the client and server to be processed through `a single TCP connection`
  - HTTP operates by establishing a new TCP connection between the client and server for each request and closing the connection after receiving the response
    - This causes overhead from establishing and terminating connections for each request, which can lead to performance degradation when many requests need to be processed
  - Keep-Alive is a mechanism introduced to solve this problem, maintaining the connection between the client and server and allowing multiple requests and responses to be processed over the same connection
  - When the client includes a `"Connection: keep-alive"` header in a request, the server can continue sending responses for multiple requests without closing the connection
- Starting from `HTTP/1.1`, the `Keep-Alive` feature, which `reuses` already established TCP connections, is supported by default
- Since the `3-way handshake` process is skipped, `performance improvement` can be expected
  - Reduces overhead from connection setup and teardown and improves performance by reducing network latency

<br>

### Keep Alive Characteristics

- The Keep-Alive `retention time` is a structure that maintains the `session` for `a defined duration from the last I/O access termination` on the connected `socket`, even if there is no access
  - In other words, if access occurs within the defined time, the connected state can be maintained
- To use the Keep-Alive header, the Connection header must be set to `keep-alive`
  - However, in HTTP/2 it is ignored, and connection management is handled by different mechanisms within that protocol
- `Event-driven` architectures that use `non-blocking`, such as `Nginx`, do not occupy `Threads` while using `Keep-Alive`, making them advantageous for `concurrent processing`

<br>

### Why Set a Keep-Alive Timeout

- Server resources are not infinite
- Maintaining connections indefinitely causes losses to the server
- In other words, the number of `sockets` that can establish connections with the server is limited, and if connections are maintained for too long, it can lead to situations where others cannot connect

<br>

### Keep-Alive in HTTP/1.0+ and HTTP/1.1

- In `1.0+`, configuration was needed `to use` Keep-Alive,
- In `1.1`, configuration is needed `to disconnect` Keep-Alive
- In other words, the purpose of the configuration differs: whether it's for using it or for disconnecting it!
