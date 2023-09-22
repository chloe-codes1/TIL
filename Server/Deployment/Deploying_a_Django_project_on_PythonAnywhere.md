# Deploying a Django project on PythonAnywhere

<br>

### 1. Git

<br>

#### 1-1. Add `.gitignore` in the base directory

> .gitignore

```
*.pyc
*~
/.vscode
__pycache__
myvenv
db.sqlite3
/static
.DS_Store
*.swp
*.swo
```

<br>

#### 1-2. Push your code to GitHub

```bash
$ git add .
$ git commit -m "Initial commit"
$ git push origin master
```

<br>

<br>

### 2. PythonAnywhere

> Assuming you already have a PythonAnywhere account 

<br>

#### 2-1. Start a "Bash" console on PythonAnywhere Dashboard

<br>

#### 2-2. Clone your git repo

```bash
$ git clone https://github.com/<your-github-username>/my-first-blog.git
```

<br>

#### 2-3. Create a virtual environment

```bash
$ cd my-first-project

$ virtualenv --python=python3.6 myvenv
Running virtualenv with interpreter /usr/bin/python3.6
[...]
Installing setuptools, pip...done.

$ source myvenv/bin/activate

(myvenv) $  pip install django~=2.0
Collecting django
[...]
Successfully installed django-2.0.6
```

<br>

#### 2-4. Create a database

```bash
(mvenv) $ python manage.py migrate
Operations to perform:
[...]
  Applying sessions.0001_initial... OK
  
(mvenv) $ python manage.py createsuperuser
```

<br>

#### 2-5.  Add a new web app

1. Hit the logo
2. Click `Web` on the menu
3. Click ` Add a new web app`
4. Confirm `Domain name`
   - You have to pay extra money if you want to customize it
5. Select `manual configuration`
6. Select `Python 3.6`

<br>

#### 2-6. Virtualenv configurations

1. Click `Web` on the menu

2. Scroll down

3. You'll see `Enter the path to a virtualenv`

4. Type the following path

   ```
   /home/<your-username>/my-first-blog/myvenv/
   ```

<br>

#### 2-7. WSGI configuration file

- Copy & Paste it

```python
import os
import sys

path = '/home/<your-PythonAnywhere-username>/my-first-blog'  # Type your PythonAnywhere account!
if path not in sys.path:
    sys.path.append(path)

os.environ['DJANGO_SETTINGS_MODULE'] = 'mysite.settings'

from django.core.wsgi import get_wsgi_application
from django.contrib.staticfiles.handlers import StaticFilesHandler
application = StaticFilesHandler(get_wsgi_application())
```

- Change **mysite** from `mysite.settings` to the directory name where your `settings.py` at
- Save it (I mean, of course)

<br>

<br>

### 3. You are now live!



<br>
