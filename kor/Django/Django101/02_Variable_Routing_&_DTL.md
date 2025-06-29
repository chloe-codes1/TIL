# Variable Routing & DTL

> Django - The web framework for perfectionists with deadlines

<br>

<br>

## Folder structure

<br>

### 1. Package folder

#### `settings.py`

<br>

> Allowed hosts

```python
ALLOWED_HOSTS = ['*']
```

- '*' 은 모든 것을 의미하는 wildcard

<br>

> Application definition

```pyton
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'pages', #app register
]
```

- 새로운 app을 만들 때마다 추가해줘야함

> Language setting & Internalization

```python
LANGUAGE_CODE = 'ko-kr' 

TIME_ZONE = 'Asia/Seoul'

#Internalization
USE_I18N = True 
USE_L10N = True
USE_TZ = True
```

<br>

<br>

#### `manage.py`

- 명령어를 실행 할 수 있도록 도와주는 파일
- 수정하지 말것!

<br>

<br>

### 2. Apps folder

<br>

- `apps.py`

  : app 설정

- `admin.py`

  : 관리자 view

- `models.py`

  : model

- `tests.py`

  : 테스트

<br>

<br>

## Variable routing

> url의 특정 위치의 값을 변수로 활용

<br>

#### 1. urls.py

```python
# django_intro/urls.py
path('hi/<str:name>/', views.hi),
path('add/<int:a>/<int:b>/', views.add),
```

<br>

#### 2. views.py

```python
# pages/views.py
def hi(request, name):
    context = {
        'name':name
    }
    return rnder(request, 'hi.html', context)
```

<br>

#### 3. template

```html
<!-- pages/templates/hi.html -->
<h1>
 Hi, {{name}}
</h1>
```

<br><br>

## DTL (Django Template Language)

> Template file (HTML) 은 django template language를 통해 구성할 수 있다!

<br>

- Django’s template language is designed to strike a balance between power and ease.
- It’s designed to feel comfortable to those used to working with HTML.

<br>

### 기본 문법

#### 1. 출력 `{{ }}`

```html
{{ name }}
{{ menu.0 }}
```

<br>

#### 2. 문법 `{% %}`

```html
{% for option in options%}

{% endfor %}
```

<br>
