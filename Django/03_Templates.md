# Templates

<br>

- Template 언어는 각 framework 마다 다르다
- Django의 template 언어는 `DTL` !

<br>

## DTL (Django Template Language)

<br>

### Ground Rule

: 연산은 DTL이 아닌 `views.py` 의 `context`로 계산된 결과를 DTL은 단순히 출력하는 역할만 하게 하기

<br>

<br>

### 기본 문법

<br>

#### 1. 출력 `{{ }}`

```html
{{ menu }}
{{ menu.0 }}
```

<br>

#### 2. 문법 `{% %}`

```html
{% for menu in menus %}

{% endfor %}
```

<br>

#### 3. 주석

```html
{# This is comment #}
```

<br>

<br>

### 반복문

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

- 배열이 비어있으면 출력할 내용 써줄 때 사용

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

### 조건문

```html
{% if user == 'admin' %}
    <p> Accessible</p>
{% else %}
    <p> Inaccessible</p>
{% endif %}
```

<br><br>

### built-in tag, filter (`|`) 

`공식문서 참고하자` : https://docs.djangoproject.com/en/3.0/ref/templates/builtins/

<br>

> length

```html
{{content | length}}
```

- 길이 확인하기

<br>

> truncatechars:num

```html
{{content|truncatechars:10}}
```

- 10자만 잘라서 보이기

<br>

> dictsort

```html
{{ value|dictsort:"name" }}
```

- dictionary 자료형일때, 명시한 key를 기준으로 정렬

<br>

<br>

### Template 확장

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
    <!-- {# Template language 에서의 주석 #} -->
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

### Template 설정 - `DIR`

```python
TEMPLATES = [
    {	
        # DTL 엔진을 활용. jinja2 등으로 변경 가능함
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # APP 내에 있는 폴더가 아닌 추가적으로 템플릿으로 활용하고 싶은 경로.
        'DIRS': [os.path.join(BASE_DIR, 'intro', 'templates')],
        # APP_DIRS: True 인경우, 등록된 app(INSTALLED_APPS)의 디렉토리에 있는 templates 폴더를 템플릿 폴더로 활용하겠다.
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

- `Linux`, `Windows` 등 OS에 상관없이 설정하려고 `os.path.dirname()`으로 함

<br>

#### DIRS 리스트에 경로 정의 폴더 구조를 통해 확인하기

```
00_django_intro/ <- BASE_DIR
	django_intro/
		templates/
```



<br>

<br>

## Multiple Apps

<br

> 앞으로는 항상 app을 생성하면 다음과 같은 폴더 구조를 가진다.

```
app1/
	templates/
		app1/
			index.html
			a.thml
    urls.py
    views.py
    ...

app2/
	templates/
		app2/
			index.html
			b.thml
    urls.py
    views.py
    ...

```

<br>

### 1. url 설정 분리

> 각각의 app 별로 url을 관리한다.

- 프로젝트 폴더 urls.py 정의

  ```python
  # django_intro/urls.py
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('pages/', include('pages.urls')),
      path('boards/', include('boards.urls')),
  ]
  ```

<br>

- 각 프로젝트별 urls.py  정의

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

### 2. templates 폴더 구조

- template 파일을 반환하기 위해서 django는 아래의 폴더들을 탐색한다.
  - DIRS 에 정의된 경로의 하위 디렉토리

  - NSTALLED_APPS 디렉토리의 templates 폴더의 하위 디렉토리 탐색

- 이 과정에서 중복된 파일이 있는 경우, 예상치 못한 결과가 나타날 수 있다.
- 따라서, 앞으로 다음과 같은 구조를 유지한다.

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

## Form 을 통한 Request 처리

> 1. 사용자들로부터 값을 받아서 (boards/new/)
>
> 2. 단순 출력하는 page 구성 (boards/complete/)

<br>

### 1. 사용자에게 form 양식 제공



#### 1-1 url 지정

```python
# boards/urls.py
path('new/', views.new),
```

<br>

#### 1-2 view 함수 생성

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

- form tag에는 `action` 속성을 정의한다
  - 사용자로부터 내요을 받아서 처리하는 url
- input tag에는 `name` 속성을 통해 사용자가 입력한 내용을 담을 변수 이름을 지정한다
- url 예시
  - `/boards/complete/?title="제목제목"`

<br><br>

### 2. 사용자 요청 처리

<br>

#### 2-1. urls.py 정의

> bords/url.py

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

- `request`에는 요청과 관련된 정보들이 담긴 object가 저장되어 있다

<br>

#### 2-3. template

```html
<!-- boards/templates/boards/complete.html -->
{{ title }}
```



<br>

<br>

`+`

#### Tip) project 쉽게 만들기!

```bash
$ cd intro/
$ django-admin startproject intro .
```

