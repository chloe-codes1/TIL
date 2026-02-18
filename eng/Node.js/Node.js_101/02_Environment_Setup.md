# Node.js Environment Setup

<br>

<br>

### Local Environment Setup

> Text Editor & The Node.js binary installable

<br>

#### Linux

> Debian

```bash
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<br>

> Redhat

```bash
sudo yum install epel-release
sudo yum install nodejs
sudo yum install npm
```

<br>

<br>

#### Verify installation: Executing a File

: Create a JavaScript file named **main.js** on your machine (Windows or Linux) having the following code.

<br>

> main.js

```javascript
console.log("Hello, Node.js!")
```

<br>

> Execute main.js file using Node.js interpreter to see the result

```bash
$node main.js
```

<br>

> Result

```bash
Hello, Node.js!
```

<br>
