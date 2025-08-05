# Wrap-up

<br>

<br>

## Project and APP initial setup

### Create project

```bash
django-admin startproject [project name]
```

<br>

#### `settings.py` configuration

- ALLOWED_HOST = ['*']
- Locale
  - Timezone
  - Language

<br>

### Create App

```bash
python manage.py startapp [app name]
```

<br>

#### `settings.py` configuration

- Register app in INSTALLED_APPS

<br>

### Define Model

- `models.py`

<br>

### Define ModelForm

- `forms.py`

<br>

<br>

## Code writing flow

> url -> view -> template

<br>

### views.py

- Function (argument -> return)

<br>

<br>

### What is OOP?

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
touch .gitignore

python -m venv venv

source venv/bin/activate

python -m pip install --upgrade pip

pip install django==2.1.15 django_extensions django_bootstrap4

pip freeze > requirements.txt

django-admin startproject django_additional .
```

<br>

<br>

## Social Login

> Installation

```bash
pip install django-allauth
```

<br>

### Google

> settings.py

```python

...

INSTALLED_APPS = [
    # pip
    'django_extensions',
    'bootstrap4',
    'bootstrap_pagination',
    'mathfilters',

    # django original
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.sites', #new
    'storages',

    # my apps
    'articles',
    'accounts',

    # allauth
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google',
    'allauth.socialaccount.providers.github',
]

...

# allauth setting
AUTHENTICATOIN_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
)

SITE_ID =1

SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        }
    },
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

> urls.py

```python
urlpatterns = [
  ...
    path('accounts/', include('accounts.urls')),
    # Below our defined accounts.url
    path('accounts/', include('allauth.urls')),
    ...
]
```

<br>

### GitHub

- App registration (get your key and secret here)

  <https://github.com/settings/applications/new>

- Development callback URL

  <http://127.0.0.1:8000/accounts/github/login/callback/>

If you want more than just read-only access to public data, specify the scope as follows. See <https://developer.github.com/v3/oauth/#scopes> for details.

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

### Make Pagination pretty with django-bootstrap-pagination

> Install

```bash
pip install django-bootstrap-pagination
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
