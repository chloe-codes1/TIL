# Vue token

<br>

## Django for Vue

<br>

```bash
django-admin startproject django_for_vue .
```

- 뒤에 . 을 해야 프로젝트가 중첩해서 생기지 않음

<br>

<br>

## django-rest-auth & django-allauth

> <https://django-rest-auth.readthedocs.io/en/latest/installation.html>

<br>

#### Installation

> Install

```bash
pip install django-rest-auth django-allauth
```

<br>

- django-rest-auth
  - login
- django-rest-auth + django-allauth
  - login + signup

<br>

> settings.py

```python
INSTALLED_APPS = (
    ...,
    'rest_framework',
    'rest_framework.authtoken',
    ...,
    'rest_auth'
)

...

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

<br>

> urls.py

```python
urlpatterns = [
    ...,
    path('rest-auth/', include('rest_auth.urls')),
]
```

<br>

#### registration

> settings.py

```python
INSTALLED_APPS = (
    ...,
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'rest_auth.registration',
)

SITE_ID = 1
```

<br>

> urls.py

```pyhon
urlpatterns = [
    ...,
    path('rest-auth/', include('rest_auth.urls')),
    path('rest-auth/signup/', include('rest_auth.registration.urls')),
]
```

<br>

<br>

## `django-cors-headers`

<br>

> Installation

``` bash
pip install django-cors-headers
```

<br>

> settings.py

```python
INSTALLED_APS = [
    ...
    'corsheaders',
]

...

MIDDLEWARE = [
    ...
    'corsheaders.middleware.CorsMiddleware', # commonMiddleware 위에 와야 함!
    'django.middleware.common.CommonMiddleware',
]

...
# CORS Allow
CORS_ORIGIN_ALLOW_ALL = True
```

<br>

<br>

<br>

<br>

`+`

## JWT (JSON Web Token)

- 해당하는 유저에 대한 모든 정보를 날림
