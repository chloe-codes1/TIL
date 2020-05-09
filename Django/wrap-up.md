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
