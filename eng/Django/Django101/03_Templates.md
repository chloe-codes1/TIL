# Templates

<br>

- Template language is different for each framework
- Django's template language is `DTL`!

<br>

## DTL (Django Template Language)

<br>

### Ground Rule

: Operations should be calculated as results in `views.py`'s `context`, not in DTL. DTL should only play the role of simply outputting the results.

<br>

<br>

### Basic syntax

<br>

#### 1. Output `{{ }}`

```html
{{ menu }}
{{ menu.0 }}
```

<br>

#### 2. Syntax `{% %}`

```html
{% for menu in menus %}

{% endfor %}
```

<br>

#### 3. Comments

```html
{# This is comment #}
```

<br>

<br>

### Loops

> Loops over each item in an array

```html
{% for reply in replies %}
	<p> {{reply}} </p>
{% endfor %}
```

```django
{{ forloop.counter }}
```

```django
{{ forloop.counter0 }}
```

```django
{% empty %}
```

- Used to specify content to display when array is empty

<br>

> Loop over each item in a dictionary

```html
{% for key, value in data.items %}
    {{ key }}: {{ value }}
{% endfor %}
```

<br>

| Variable              | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| `forloop.counter`     | The current iteration of the loop (1-indexed)                |
| `forloop.counter0`    | The current iteration of the loop (0-indexed)                |
| `forloop.revcounter`  | The number of iterations from the end of the loop (1-indexed) |
| `forloop.revcounter0` | The number of iterations from the end of the loop (0-indexed) |
| `forloop.first`       | True if this is the first time through the loop              |
| `forloop.last`        | True if this is the last time through the loop               |
| `forloop.parentloop`  | For nested loops, this is the loop surrounding the current one |

<br>

<br>

### Conditionals

```html
{% if user == 'admin' %}
    <p> Accessible</p>
{% else %}
    <p> Inaccessible</p>
{% endif %}
```

<br><br>

### built-in tag, filter (`|`) 

`Refer to the official documentation`: https://docs.djangoproject.com/en/3.0/ref/templates/builtins/

<br>

> length

```html
{{content | length}}
```

- Check length

<br>

> truncatechars:num

```html
{{content|truncatechars:10}}
```

- Show only 10 characters (truncated)

<br>

> dictsort

```html
{{ value|dictsort:"name" }}
```

- For dictionary data type, sort by specified key

<br>

<br>

### Template Extension

<br>

> pages/templates/base.html

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django Basics - Pages</title>
    {% block css %}
    {% endblock %}
</head>
<body>
    <h1> Django Basic Syntax</h1>
    {% block body %}

    {% endblock %}
</body>
</html>
```

<br>

> posts.html

```html
{% extends 'base.html' %}

{% block css %}
<style>

    h1 {
        color: blue;
    }
</style>

{% endblock %}


{% block body %}
    <!-- {# Comment in Template language #} -->
    <h1> Post No. {{id}}</h1>
    <p> {{content}}</p>
    <p> {{content | length}}</p>
    <p> {{content|truncatechars:10}}</p>
    <hr>
    {% for reply in replies %}
        <p> {{forloop.counter}} {{reply}}</p>
    {% endfor %}

    <hr>

    {% for reply in no_replies %}
        <p> {{forloop.counter}} {{reply}}</p>
        {% empty %}
        <p> There's no reply ㅠ_ㅠ</p>
    {% endfor %}
    <hr>
    {% if user == 'admin' %}
        <p> Accessible</p>
    {% else %}
        <p> Inaccessible</p>
    {% endif %}

{% endblock %}
```

<br>

<br>

### Template Configuration - `DIR`

```python
TEMPLATES = [
    {	
        # Use DTL engine. Can be changed to jinja2 etc.
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # Additional paths to use as templates, not in APP folders.
        'DIRS': [os.path.join(BASE_DIR, 'intro', 'templates')],
        # APP_DIRS: True means use templates folder in directories of registered apps (INSTALLED_APPS) as template folders.
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

<br>

#### BASE_DIR

```python
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```

- Use `os.path.dirname()` to configure regardless of OS like `Linux`, `Windows`

<br>

#### Check folder structure through path definition in DIRS list

```
00_django_intro/ <- BASE_DIR
	django_intro/
		templates/
```

<br>

<br>

## Multiple Apps

<br>

> From now on, whenever you create an app, it will have the following folder structure.

```
app1/
	templates/
		app1/
			index.html
			a.html
    urls.py
    views.py
    ...

app2/
	templates/
		app2/
			index.html
			b.html
    urls.py
    views.py
    ...

```

<br>

### 1. URL configuration separation

> Manage URLs for each app separately.

- Define project folder urls.py

  ```python
  # django_intro/urls.py
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('pages/', include('pages.urls')),
      path('boards/', include('boards.urls')),
  ]
  ```

<br>

- Define urls.py for each project

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns = [
      # /boards/
      path('', views.index),
      # /boards/new/
      path('new/', views.new),
      # /boards/complete/
      path('complete/', views.complete),
  ]
  ```

  <br>

  <br>

### 2. templates folder structure

- To return template files, django searches the following folders:
  - Subdirectories of paths defined in DIRS
  - Subdirectories of templates folder in INSTALLED_APPS directories

- If there are duplicate files in this process, unexpected results may occur.
- Therefore, maintain the following structure from now on:

```
app1/
	templates/
		app1/
app2/
	templates/
		app2/
```

<br>

<br>

## Processing Requests through Forms

> 1. Receive values from users (boards/new/)
>
> 2. Configure page to simply display (boards/complete/)

<br>

### 1. Provide form to users

#### 1-1 URL specification

```python
# boards/urls.py
path('new/', views.new),
```

<br>

#### 1-2 Create view function

```python
#boards/views.py
def new (request):
    return render(request, 'boards/new.html')
```

<br>

#### 1-3 template

```html
<form action="/boards/complete/">
    Title: <input type="text" name="title">
</form>
```

- Define `action` attribute in form tag
  - URL to process content received from users
- In input tag, specify variable name to hold user input through `name` attribute
- URL example
  - `/boards/complete/?title="제목제목"`

<br><br>

### 2. Process user requests

<br>

#### 2-1. urls.py definition

> boards/urls.py

```python
path('/boards/complete', views.complete)
```

<br>

#### 2-2. views.py

> boards/views.py

```python
def complete(request):
    title = request.GET.get('title')
    context = {
        'title': title
    }
    return render(request, 'boards/complete.html', context)
```

- `request` contains an object with information related to the request

<br>

#### 2-3. template

```html
<!-- boards/templates/boards/complete.html -->
{{ title }}
```

<br>

<br>

`+`

#### Tip) Creating project easily!

```bash
$ cd intro/
$ django-admin startproject intro .
``` 
