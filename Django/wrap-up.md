# Wrap-up

<br>

<br>

## 프로젝트 및 APP 초기 설정



### 프로젝트 만들기

```bash
$ django-admin startproject [project name]
```

<br>

#### `settings.py` 설정

- ALLOWED_HOST = ['*']
- Locale
  - Timezone
  - Language

<br>

###  App 만들기

```bash
$ python manage.py startapp [app name]
```

<br>

#### `settings.py` 설정

- INSTALLED_APPS에 app 등록

<br>

### Model 정의

- `models.py`

<br>

### ModelForm 정의

- `forms.py`

<br>

<br>

## 코드 작성 흐름

> url -> view -> template

<br>

### views.py

- 함수 ( 인자 -> 반환 return)



<br>

<br>

### OOP란?

S + V



<br>

<br>

### Import

```python
# urls.py
from django.contrib import admin
from django.urls import path, include

# forms.py
from django import forms

# models.py
from django.db import models

# auth
from django.contrib import messages
from django.contrib.auth.decorators import login_required
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
from django.contrib.auth.decorators import login_required
from django.contrib.auth import get_user_model, login, logout
from django.contrib.auth.models import User 

# views.py
from django.shortcuts import render, redirect, get_object_or_404
from django.views.decorators.http import require_POST


from django.conf import settings
from django.contrib import admin
```

<br>

<br>

## Project setup

```bash
$ touch .gitignore

$ python -m venv venv

$ source venv/bin/activate

$ python -m pip install --upgrade pip

$ pip install django==2.1.15 django_extensions django_bootstrap4

$ pip freeze > requirements.txt

$ django-admin startproject django_additional .
```

<br>

<br>

## Social Login

```bash
$ pip install django-allauth
```

<br>

### GitHub

- App registration (get your key and secret here)

  https://github.com/settings/applications/new

- Development callback URL

  http://127.0.0.1:8000/accounts/github/login/callback/

If you want more than just read-only access to public data, specify the scope as follows. See https://developer.github.com/v3/oauth/#scopes for details.

```
SOCIALACCOUNT_PROVIDERS = {
    'github': {
        'SCOPE': [
            'user',
            'repo',
            'read:org',
        ],
    }
}
```



<br>

<br>



## Pagination



<br>

### django-bootstrap-pagination 으로 Pagination 예쁘게 하기

> Install

```bash
$ pip install django-bootstrap-pagination
```

<br>

> `settings.py`

```python
    INSTALLED_APPS = (
        'bootstrap_pagination',
    )
```

<br>

> template

```html
 {% load bootstrap_pagination %}

	...

{% bootstrap_paginate page_obj range=10 show_prev_next="false" show_first_last="true" %}
```

