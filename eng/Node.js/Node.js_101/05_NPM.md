# NPM

<br>

<br>

### Key Features of NPM (Node Package Manager)

1. A Node.js package/module repository searchable on [NPMSearch](https://npmsearch.com/)
2. A command-line utility for installing Node.js packages and managing versions/compatibility

<br>

<br>

> Check npm installation

```shell
$ npm --version
6.13.4
```

<br>

> npm version update

```shell
sudo npm install npm -g
```

<br>

<br>

### Installing Modules using NPM

<br>

> Syntax to install any Node.js module

```shell
npm install <Module Name>
```

<br>

> Install a famous Node.js web framework module called **express**

```shell
npm install express
```

<br>

> Now you can use this module in your js file as following

```shell
var express = require('express');
```

<br>

<br>

### Global vs Local Installation

<br>

By default, `npm` installs modules in local mode

- **Local mode**

  : Means installing the package in the `node_modules` directory within the directory where the command was executed

- **Global mode**

  : Means installing in the System directory

<br>

> Install express in global mode

```shell
$ sudo npm install express -g
/usr/lib
└─┬ express@4.13.4
 ├─┬ accepts@1.2.13
 │ ├─┬ mime-types@2.1.9
 │ │ └── mime-db@1.21.0
 │ └── negotiator@0.5.3
 .... truncated for brevity....
 │ └── statuses@1.2.1
 ├── utils-merge@1.0.0
 └── vary@1.0.1
```

- You can see that the module is installed in /usr/lib/node_modules, not in the current path

- Since it saves to the system, you need to prefix with `sudo` if you are not the root user!

- When installed in **Global mode**, you cannot directly `require` it in a node application

  - but, you can use the `npm link` command to import the module

  ```shell
  npm install -g express
  cd [local path]/project
  npm link express
  ```

<br>

<br>

### package.json

: Located in the path of the Node application/module and defines the properties of the package

<br>

> **package.json** generated when creating a project with express

```shell
{
  "name": "myapp",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.13.2",
    "cookie-parser": "~1.3.5",
    "debug": "~2.2.0",
    "express": "~4.13.1",
    "jade": "~1.11.0",
    "morgan": "~1.6.1",
    "serve-favicon": "~2.3.0"
  }
}
```

- **package.json** contains information about the modules and module versions that the project depends on

<br>

<br>

#### Uninstalling a Module

<br>

```shell
npm uninstall express
```

<br>

<br>

#### Updating a Module

<br>

```shell
npm update express
```

<br>

<br>

#### Search a Module

<br>

```shell
npm search express
```

- This command consumes a lot of memory the first time it is used
  - If you are using a Cloud IDE or your server has about 1G of RAM, it will take a very long time or cause errors
  - In that case, search on [NPMSearch](https://npmsearch.com/)!

<br>
