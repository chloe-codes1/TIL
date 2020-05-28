# Dump Data

<br>

> data dumping 하기

```bash
$ python manage.py dumpdata
```

<br>

> dump 한 data를 data.json file로 만들기

```bash
$ python manage.py dumpdata > data.json
```

<br>

```bash

```

<br>

<br>

DB의 data 고스란히 이전하고파

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
│   │   ├── 0001_initial.py
│   │   ├── __init__.py
│   │   └── __pycache__
│   │       ├── 0001_initial.cpython-36.pyc
│   │       ├── 0002_user_image.cpython-36.pyc
│   │       ├── 0003_remove_user_image.cpython-36.pyc
│   │       └── __init__.cpython-36.pyc
│   ├── models.py
│   ├── __pycache__
│   │   ├── admin.cpython-36.pyc
│   │   ├── forms.cpython-36.pyc
│   │   ├── __init__.cpython-36.pyc
│   │   ├── models.cpython-36.pyc
│   │   ├── urls.cpython-36.pyc
│   │   └── views.cpython-36.pyc
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
│   │   └── __pycache__
│   │       ├── 0001_initial.cpython-36.pyc
│   │       ├── 0002_article_liked_user.cpython-36.pyc
│   │       ├── 0002_comment.cpython-36.pyc
│   │       ├── 0003_auto_20200428_1306.cpython-36.pyc
│   │       ├── 0003_auto_20200505_2001.cpython-36.pyc
│   │       ├── 0004_auto_20200428_2150.cpython-36.pyc
│   │       ├── 0005_auto_20200428_2227.cpython-36.pyc
│   │       ├── 0006_auto_20200428_2331.cpython-36.pyc
│   │       └── __init__.cpython-36.pyc
│   ├── models.py
│   ├── __pycache__
│   │   ├── admin.cpython-36.pyc
│   │   ├── forms.cpython-36.pyc
│   │   ├── __init__.cpython-36.pyc
│   │   ├── models.cpython-36.pyc
│   │   ├── urls.cpython-36.pyc
│   │   └── views.cpython-36.pyc
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
│   ├── __pycache__
│   │   ├── __init__.cpython-36.pyc
│   │   ├── settings.cpython-36.pyc
│   │   ├── urls.cpython-36.pyc
│   │   └── wsgi.cpython-36.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── latest.dump
├── manage.py
├── media
│   ├── CACHE
│   │   └── images
│   │       ├── 토핑은내얼귤
│   │       │   └── 26b612657d5fa8ad25f41426cada2e97.jpg
│   │       ├── daenak
│   │       │   └── 523e71a86045e265802ac022b0fa825e.jpg
│   │       ├── fajita
│   │       │   └── 283581d910a3fe0bff6267df60730441.jpg
│   │       ├── fig-3640553_1920
│   │       │   ├── b1efcabe7a3474972cdee37a5074baf2.jpg
│   │       │   └── f6d9ea29a584af379ca5192d726378ac.jpg
│   │       ├── gravy
│   │       │   └── 13d7388dcc4a42ad8428f6a9d2b7e793.jpg
│   │       ├── koreanfood
│   │       │   └── d1691117d22fb958d4e723e3a4100e2d.jpg
│   │       ├── lit_it_Tommy
│   │       │   └── a83b1ac7fd379b28039a993545beb2ea.jpg
│   │       ├── pancake
│   │       │   └── 9f976a58f4133f28b4cd5d38e72e6575.jpg
│   │       ├── pancake_Ef6at0Z
│   │       │   └── ad50bc8ab4d1bebfa63423628a1d8057.jpg
│   │       ├── pepperoni
│   │       │   ├── 5a7b37281693fa8cc9c40c7187565d33.jpg
│   │       │   ├── 641d832cfd1d728826e311a615fed4a8.jpg
│   │       │   ├── a52a18ed4326aa0df2c57b9ee836f585.jpg
│   │       │   └── d89b6c489bd11ec68190e8ab31c66ff2.jpg
│   │       ├── salad-2756467_1920
│   │       │   ├── 4af47b8191fe3d8855c985ba15d3748c.jpg
│   │       │   └── c9ad6f25191e71de3e07e4f4910b544e.jpg
│   │       ├── steak-2936531_1920
│   │       │   └── f7f0e3356d713681d21ba4b651a03e72.jpg
│   │       ├── steak-2936531_1920_qDYpiSA
│   │       │   └── 6d26a7a0f8c69196f3c962c12f19730b.jpg
│   │       ├── steak-3640560_640
│   │       │   ├── 0b6bfb5faabfca5e841f05aa5fd46cfd.jpg
│   │       │   └── c9f7d08bc5191bc1c225feab2335d97a.jpg
│   │       └── tomcat
│   │           ├── 2c883cdd147988ae535b516dff12c407.jpg
│   │           ├── 32be02d1a5f586b8d15a48eea6bd1c6f.jpg
│   │           ├── 724f0157cdb56d4d964f7799ec70eecf.jpg
│   │           ├── a7cd805c1c42c6a2c4293619558124c3.jpg
│   │           ├── af0700f88a5856f61f97f139ba165cc2.jpg
│   │           └── dc7bda6c277f26d282f0dbd99daf549c.jpg
│   ├── daenak.jpg
│   ├── fajita.jpg
│   ├── favicon
│   │   └── instagram-64.ico
│   ├── fig-3640553_1920.jpg
│   ├── gravy.jpg
│   ├── 토핑은내얼귤.jpg
│   ├── koreanfood.jpg
│   ├── lit_it_Tommy.jpg
│   ├── pancake_Ef6at0Z.jpg
│   ├── pancake.jpg
│   ├── pepperoni.jpg
│   ├── salad-2756467_1920.jpg
│   ├── steak-2936531_1920.jpg
│   ├── steak-2936531_1920_qDYpiSA.jpg
│   ├── steak-3640560_640.jpg
│   └── tomcat.png
├── Procfile
├── README-images
│   ├── gram-gram_comment_01.png
│   ├── gram-gram_index_01.png
│   ├── gram-gram_index_02.png
│   ├── gram-gram_profile_01.png
│   └── gram-gram_search_01.png
├── README.md
├── requirements.txt
├── runtime.txt
├── src
│   └── django-debug-toolbar
│       ├── CONTRIBUTING.md
│       ├── debug_toolbar
│       │   ├── apps.py
│       │   ├── decorators.py
│       │   ├── __init__.py
│       │   ├── locale
│       │   │   ├── ca
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── cs
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── de
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── en
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── es
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── fi
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── fr
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── he
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── id
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── it
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── nl
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── pl
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── pt
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── pt_BR
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── ru
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── sk
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── sv_SE
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   ├── uk
│       │   │   │   └── LC_MESSAGES
│       │   │   │       ├── django.mo
│       │   │   │       └── django.po
│       │   │   └── zh_CN
│       │   │       └── LC_MESSAGES
│       │   │           ├── django.mo
│       │   │           └── django.po
│       │   ├── management
│       │   │   ├── commands
│       │   │   │   ├── debugsqlshell.py
│       │   │   │   └── __init__.py
│       │   │   └── __init__.py
│       │   ├── middleware.py
│       │   ├── panels
│       │   │   ├── cache.py
│       │   │   ├── headers.py
│       │   │   ├── __init__.py
│       │   │   ├── logging.py
│       │   │   ├── profiling.py
│       │   │   ├── __pycache__
│       │   │   │   ├── cache.cpython-36.pyc
│       │   │   │   ├── headers.cpython-36.pyc
│       │   │   │   ├── __init__.cpython-36.pyc
│       │   │   │   ├── logging.cpython-36.pyc
│       │   │   │   ├── profiling.cpython-36.pyc
│       │   │   │   ├── redirects.cpython-36.pyc
│       │   │   │   ├── request.cpython-36.pyc
│       │   │   │   ├── settings.cpython-36.pyc
│       │   │   │   ├── signals.cpython-36.pyc
│       │   │   │   ├── staticfiles.cpython-36.pyc
│       │   │   │   ├── timer.cpython-36.pyc
│       │   │   │   └── versions.cpython-36.pyc
│       │   │   ├── redirects.py
│       │   │   ├── request.py
│       │   │   ├── settings.py
│       │   │   ├── signals.py
│       │   │   ├── sql
│       │   │   │   ├── forms.py
│       │   │   │   ├── __init__.py
│       │   │   │   ├── panel.py
│       │   │   │   ├── __pycache__
│       │   │   │   │   ├── forms.cpython-36.pyc
│       │   │   │   │   ├── __init__.cpython-36.pyc
│       │   │   │   │   ├── panel.cpython-36.pyc
│       │   │   │   │   ├── tracking.cpython-36.pyc
│       │   │   │   │   ├── utils.cpython-36.pyc
│       │   │   │   │   └── views.cpython-36.pyc
│       │   │   │   ├── tracking.py
│       │   │   │   ├── utils.py
│       │   │   │   └── views.py
│       │   │   ├── staticfiles.py
│       │   │   ├── templates
│       │   │   │   ├── __init__.py
│       │   │   │   ├── panel.py
│       │   │   │   ├── __pycache__
│       │   │   │   │   ├── __init__.cpython-36.pyc
│       │   │   │   │   ├── panel.cpython-36.pyc
│       │   │   │   │   └── views.cpython-36.pyc
│       │   │   │   └── views.py
│       │   │   ├── timer.py
│       │   │   └── versions.py
│       │   ├── __pycache__
│       │   │   ├── apps.cpython-36.pyc
│       │   │   ├── decorators.cpython-36.pyc
│       │   │   ├── __init__.cpython-36.pyc
│       │   │   ├── middleware.cpython-36.pyc
│       │   │   ├── settings.cpython-36.pyc
│       │   │   ├── toolbar.cpython-36.pyc
│       │   │   ├── utils.cpython-36.pyc
│       │   │   └── views.cpython-36.pyc
│       │   ├── settings.py
│       │   ├── static
│       │   │   └── debug_toolbar
│       │   │       ├── css
│       │   │       │   ├── print.css
│       │   │       │   └── toolbar.css
│       │   │       ├── img
│       │   │       │   ├── ajax-loader.gif
│       │   │       │   └── indicator.png
│       │   │       └── js
│       │   │           ├── redirect.js
│       │   │           ├── toolbar.js
│       │   │           └── toolbar.timer.js
│       │   ├── templates
│       │   │   └── debug_toolbar
│       │   │       ├── base.html
│       │   │       ├── panels
│       │   │       │   ├── cache.html
│       │   │       │   ├── headers.html
│       │   │       │   ├── logging.html
│       │   │       │   ├── profiling.html
│       │   │       │   ├── request.html
│       │   │       │   ├── settings.html
│       │   │       │   ├── signals.html
│       │   │       │   ├── sql_explain.html
│       │   │       │   ├── sql.html
│       │   │       │   ├── sql_profile.html
│       │   │       │   ├── sql_select.html
│       │   │       │   ├── sql_stacktrace.html
│       │   │       │   ├── staticfiles.html
│       │   │       │   ├── templates.html
│       │   │       │   ├── template_source.html
│       │   │       │   ├── timer.html
│       │   │       │   └── versions.html
│       │   │       └── redirect.html
│       │   ├── templatetags
│       │   │   ├── __init__.py
│       │   │   └── __pycache__
│       │   │       └── __init__.cpython-36.pyc
│       │   ├── toolbar.py
│       │   ├── utils.py
│       │   └── views.py
│       ├── django_debug_toolbar.egg-info
│       │   ├── dependency_links.txt
│       │   ├── not-zip-safe
│       │   ├── PKG-INFO
│       │   ├── requires.txt
│       │   ├── SOURCES.txt
│       │   └── top_level.txt
│       ├── docs
│       │   ├── changes.rst
│       │   ├── commands.rst
│       │   ├── configuration.rst
│       │   ├── conf.py
│       │   ├── contributing.rst
│       │   ├── index.rst
│       │   ├── installation.rst
│       │   ├── make.bat
│       │   ├── Makefile
│       │   ├── panels.rst
│       │   └── tips.rst
│       ├── example
│       │   ├── django-debug-toolbar.png
│       │   ├── example.db
│       │   ├── __init__.py
│       │   ├── manage.py
│       │   ├── README.rst
│       │   ├── settings.py
│       │   ├── static
│       │   │   └── test.css
│       │   ├── templates
│       │   │   ├── index.html
│       │   │   ├── jquery
│       │   │   │   └── index.html
│       │   │   ├── mootools
│       │   │   │   └── index.html
│       │   │   └── prototype
│       │   │       └── index.html
│       │   ├── urls.py
│       │   └── wsgi.py
│       ├── LICENSE
│       ├── Makefile
│       ├── MANIFEST.in
│       ├── README.rst
│       ├── requirements_dev.txt
│       ├── setup.cfg
│       ├── setup.py
│       ├── tests
│       │   ├── additional_static
│       │   │   └── base.css
│       │   ├── base.py
│       │   ├── commands
│       │   │   ├── __init__.py
│       │   │   └── test_debugsqlshell.py
│       │   ├── context_processors.py
│       │   ├── forms.py
│       │   ├── __init__.py
│       │   ├── loaders.py
│       │   ├── models.py
│       │   ├── panels
│       │   │   ├── __init__.py
│       │   │   ├── test_cache.py
│       │   │   ├── test_logging.py
│       │   │   ├── test_profiling.py
│       │   │   ├── test_redirects.py
│       │   │   ├── test_request.py
│       │   │   ├── test_sql.py
│       │   │   ├── test_staticfiles.py
│       │   │   ├── test_template.py
│       │   │   └── test_versions.py
│       │   ├── settings.py
│       │   ├── templates
│       │   │   ├── base.html
│       │   │   ├── basic.html
│       │   │   └── jinja2
│       │   │       └── basic.jinja
│       │   ├── test_integration.py
│       │   ├── test_utils.py
│       │   ├── urls.py
│       │   └── views.py
│       └── tox.ini
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









```bash
$ python manage.py loaddata articles/data.json
Installed 113 object(s) from 1 fixture(s)
```

