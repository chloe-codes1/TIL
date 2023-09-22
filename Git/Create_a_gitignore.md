# How to create a .gitignore file

> I'm jotting it down so as not to forget how to create a .gitignore later on

<br>

<br>

### 1. `cd` into your projects root directory

<br>

### 2. Create `.gitignore` file

```bash
touch .gitignore
```

<br>

### 3. Write it down using `.gitignore` patterns

ex)

- To exclude all files ending in `.log`

  ```
  *.log
  ```

- To exclude any file names that contain `.log`

  ```
  *.log*
  ```

- To exclude all files in a specific path

  ```
  /Build/*
  ```

<br>

<br>

`+`

### If you create a `.gitignore` when in use

```bash
git rm -r --cached .

git add .

git commit -m "git ignore add"

git push
```

<br>

<br>

#### `.gitignore` example

```
*.bash_history

*.gitconfig

*.python_history

.c9/

.cache/

.local/
```
