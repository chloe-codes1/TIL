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

- '*' is a wildcard that means everything

<br>

> Application definition

```python
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

- Must be added every time a new app is created

> Language setting & Internationalization

```python
LANGUAGE_CODE = 'ko-kr' 

TIME_ZONE = 'Asia/Seoul'

#Internationalization
USE_I18N = True 
USE_L10N = True
USE_TZ = True
```

<br>

<br>

#### `manage.py`

- A file that helps execute commands
- Do not modify!

<br>

<br>

### 2. Apps folder

<br>

- `apps.py`

  : App configuration

- `admin.py`

  : Admin view

- `models.py`

  : Model

- `tests.py`

  : Tests

<br>

<br>

## Variable routing

> Use specific values in URL positions as variables

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
    return render(request, 'hi.html', context)
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

> Template files (HTML) can be structured using Django template language!

<br>

- Django's template language is designed to strike a balance between power and ease.
- It's designed to feel comfortable to those used to working with HTML.

<br>

### Basic syntax

#### 1. Output `{{ }}`

```html
{{ name }}
{{ menu.0 }}
```

<br>

#### 2. Syntax `{% %}`

```html
{% for option in options%}

{% endfor %}
```

<br> 
