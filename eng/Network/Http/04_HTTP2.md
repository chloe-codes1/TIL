# HTTP/2

> What changed in HTTP 2.0

<br>

### Why HTTP/1 is Slow

The response from the previous request must be received before the next request can be processed

>
>
- In `HTTP 1.0`, a new `connection` was created for every request sent -> `inefficient`
- In `HTTP 1.1`, concepts of `persistent connections` and `HTTP pipelining` were introduced
  - Connections could be `reused`,
  - And multiple requests could be sent to the server in advance
- However, a problem arose in that responses could only be received `in the order the requests were sent`
  - If the first request had an issue and its response was delayed, the responses of subsequent requests would also be delayed

        -> `Head of Line Blocking`

    - A `performance degradation phenomenon` that occurs when a head packet is `delayed` in a packet `queue` in the Network

<br>

### Features of HTTP/2

- HTTP `header` data `compression`
  - Prevents retransmission of `fields` that are `duplicated` from previous headers, saving data
  - Previously headers were `Plain Text`, but HTTP/2 uses a header compression method called `HPACK` to improve data `transmission efficiency`
- `Server Push`
  - The server can `send along` certain files that will be needed, such as JS, CSS, and image files that the client did not request, in response to a `single HTTP request`
- Solved the `Head of Line Blocking` problem of `HTTP 1.x`
  - HTTP/2 reduced transmission time by sending multiple files in `parallel transmission` at once
  - Multiple requests and responses can be sent `in parallel` over a single TCP connection
    - Multiple parallel `streams` can exist in a single `connection`
    - If streams are mixed during transmission, they are `reassembled` at the receiver using stream numbers
- `Stream priority`
  - As `frames` from multiple streams can be `multiplexed`, the need to specify stream priorities arose
  - The client can use a `priority tree` to specify stream processing priorities for the server
    - The server sets bandwidth so that higher-priority responses are delivered to the client first
