# Installing Node.js Using NVM

<br>

### 1. Download the `nvm` installation script from [GitHub page](https://github.com/nvm-sh/nvm) by using `curl`

```bash
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh -o install_nvm.sh
```

<br>

### 2. Run the script with `bash`

```bash
bash install_nvm.sh
```

<br>

### 3. Restart your terminal

```bash
source ~/.profile
```

- Source the `~/.profile` file to gain access to the `nvm` functionality
- or you can just logout & login

<br>

### 4.  Check the versions of `Node.js` that are available

```bash
$ nvm ls-remote

      ...
  
        v12.0.0
        v12.1.0
        v12.2.0
        v12.3.0
        v12.3.1
        v12.4.0
        v12.5.0
        v12.6.0
        v12.7.0
        v12.8.0
        v12.8.1
        v12.9.0
        v12.9.1
       v12.10.0
       v12.11.0
       v12.11.1
       v12.12.0
       v12.13.0   (LTS: Erbium)
       v12.13.1   (LTS: Erbium)
       v12.14.0   (LTS: Erbium)
       v12.14.1   (LTS: Erbium)
       v12.15.0   (LTS: Erbium)
       v12.16.0   (LTS: Erbium)
       v12.16.1   (LTS: Erbium)
       v12.16.2   (LTS: Erbium)
       v12.16.3   (Latest LTS: Erbium)
       
        ...
        
```

<br>

### 5. Install

> Install specific version

```bash
nvm install 12.14.0
```

> Install the most recent LTS release

```bash
nvm install --lts
```

<br>

### 6. See the version currently being used by the shell

```bash
$ node -v
v12.14.0
```

or

```bash
$ node --version
v12.14.0
```

<br>

### 7. If you have multiple Node.js versions, you can see what is installed

```bash
$ nvm ls
       v10.15.1
->     v12.14.0
         system
default -> 10.15.1 (-> v10.15.1)
node -> stable (-> v12.14.0) (default)
stable -> 12.14 (-> v12.14.0) (default)
iojs -> N/A (default)
lts/* -> lts/erbium (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.20.1 (-> N/A)
lts/erbium -> v12.16.3 (-> N/A)
```

<br>

### 8. Switch Node.js versions

> Switch to Node.js version `12.14.0`

```bash
$ nvm use 12.14.0
Now using node v12.14.0 (npm v6.13.4)
```

> Switch to the latest Node.js version

```bash
nvm use node
```

> Switch to the latest LTS version

```bash
nvm use --lts
```

<br>

### 9. Set the default version of node when starting a new shell

> Specific version

```bash
nvm alias default 12.14.0
```

> Latest Node.js version

```bash
nvm alias default node
```

<br>

<br>

`+`

### Uninstall `Node.js`

```bash
nvm uninstall [NODE_VERSION]
```
