# Web Module

> Web server & web client with http module

<br>

<br>

### HTTP Server

ex)

> index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTTP server test</title>
</head>
<body>
    <p> Testing web server coding with http module!</p>
</body>
</html>
```

<br>

> server.js

```javasc
var http = require("http");
var fs = require("fs");
var url = require("url");

// Create server
http.createServer(function(request, response) {
  // Parse the directory/file name after the url
  var pathname = url.parse(request.url).pathname;

  console.log("Request for " + pathname + " received!");

  // If the file name is empty, set it to index.html
  if (pathname == "/") {
    pathname = "/index.html";
  }

  // Read the file
  fs.readFile(pathname.substr(1), function(error, data) {
    if (error) {
      console.log(error);
      // 1) When the page is not found
      // HTTP Status: 404 : NOT FOUND
      // Content Type: text/plain
      response.writeHead(404, { "Content-Type": "text/html" });
    } else {
        // 2) When the page is found
        // HTTP Status: 200 : OK
        // Content Type: text/plain
        response.writeHead(200, {'Content-Type': 'text/html'});

        // Read the file and write to responseBody
        response.write(data.toString());
    }
    // Send responseBody

    response.end();

  });
}).listen(8081);

console.log('Server currently running at http://127.0.0.1:8081/ !');
```

- When a client connects to the server, it **parses** the file to open from the URL and serves it
- If the file does not exist, an **error message** is printed to the console!

<br>

<br>

#### Results

> Run the Server

```shell
$ node server.js
Server currently running at http://127.0.0.1:8081/ !
```

<br>

> Access <http://127.0.0.1:8081/>

![image-20200328135841386](../../../kor/images/image-20200328135841386.png)

```shell
Request for / received!
Request for /favicon.ico received!
{ [Error: ENOENT: no such file or directory, open 'favicon.ico']
  errno: -2,
  code: 'ENOENT',
  syscall: 'open',
  path: 'favicon.ico' }

```

<br>

> Access <http://127.0.0.1:8081/showmeerror>

![image-20200328143323679](../../../kor/images/image-20200328143323679.png)

```shell
Request for /showmeerror received!
{ [Error: ENOENT: no such file or directory, open 'showmeerror']
  errno: -2,
  code: 'ENOENT',
  syscall: 'open',
  path: 'showmeerror' }

```

<br>

> Access <http://127.0.0.1:8081/index.html>

![image-20200328144715931](../../../kor/images/image-20200328144715931.png)

```shell
Request for /index.html received!
```

<br>

<br>

### HTTP Client

ex)

> client.js

```javascript
var http = require('http');

// Set HTTP Request options
var options = {
    host: 'localhost',
    port: '8081',
    path: '/index.html'
};

// Receive the Response using a Callback function
var callback = function(response) {
    // When a response event is detected, receive data into the body
    var  body = '';
    response.on('data', function(data){
        body += data;
    });

    // When an end event is detected, finish receiving data and print the content
    response.on('end', function(){
        // Data reception complete!
        console.log(body);
    });

    // Send an HTTP Request to the Server~!
    var request = http.request(options, callback);
    request.end();
}
```

- From `response.on()`, the `.on()` method tells us that `response` is an object that inherits the `EventEmitter` class!

<br>

#### Results

```shell
$ node client.js
<html>
<head>
    <title>HTTP server test</title>
</head>
<body>
    <p> Testing web server coding with http module!</p>
</body>
</html>
```

<br>
