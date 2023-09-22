# Python Virtual Environment

<br>

### Purpose of Python virtual environment

- To create an isolated environment for different Python projects
  - You can install a specific version of module on each project  without worrying that it will affect your other Python projects.

<br>

<br>

## Create Virtual Environment for Python 3

<br>

> Check your python version

```bash
$ python --version
Python 3.6.9
```

<br>

>Install `virtualenv`

```bash
pip install virtualenv
```

<br>

> Create a virtual environment

```bash
python -m venv venv
```

<br>

> activate your virtual environment

```bash
source venv/bin/activate
```

<br>

> set up command alias in .`bashrc`

```bash
alias va="source venv/bin/activate"
```

<br>
