# Dump and load data

<br>

### data dumping 하기

```bash
python manage.py dumpdata
```

<br>

### dump 한 data를 data.json file로 만들기

```bash
python manage.py dumpdata > data.json
```

<br>

<br>

### `fixtures` directory 만들기

```bash
.
├── accounts
│   ├── admin.py
│   ├── apps.py
│   ├── forms.py
│   ├── __init__.py
│   ├── migrations
│   ├── models.py
│   ├── templates
│   │   └── accounts
│   │       ├── login.html
│   │       ├── profile.html
│   │       ├── signup.html
│   │       └── update.html
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── articles
│   ├── admin.py
│   ├── apps.py
│   ├── fixtures
│   │   └── articles
│   │       └── data.json
│   ├── forms.py
│   ├── __init__.py
│   ├── migrations
│   │   ├── 0001_initial.py
│   │   ├── 0002_comment.py
│   │   ├── 0003_auto_20200505_2001.py
│   │   ├── __init__.py
│   ├── models.py
│   ├── templates
│   │   └── articles
│   │       ├── comment.html
│   │       ├── form.html
│   │       ├── index.html
│   │       └── like.html
│   ├── templatetags
│   │   ├── article_extras.py
│   │   ├── __init__.py
│   │   └── __pycache__
│   │       ├── article_extras.cpython-36.pyc
│   │       ├── hashtags.cpython-36.pyc
│   │       └── __init__.cpython-36.pyc
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── a.txt
├── crud
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── latest.dump
├── manage.py
├── media
├── Procfile
├── README-images
├── README.md
├── requirements.txt
├── runtime.txt
├── src
│   └── django-debug-toolbar
├── static
│   ├── css
│   └── js
├── templates
│   ├── _accountdelete.html
│   ├── base.html
│   ├── _commentdelete.html
│   ├── _deletemodal.html
│   ├── _nav.html
│   └── _replies.html
└── tree.txt

117 directories, 324 files
```

<br>

<br>

### loaddata

```bash
$ python manage.py loaddata articles/data.json
Installed 113 object(s) from 1 fixture(s)
```
