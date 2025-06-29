# Model in Django

<br>

<br>

### Django 기본 흐름

1. `url`을 정의한다
   - `urls.py`는 이정표다!
2. `views.py`에 실행할 함수를 만든다
3. 반환할 `html`를 만든다

<br>

<br>

## Django project / app 설정

- Django는 하나의 project가 복수의 app을 가지는 구조로 되어있다
- 각각의 app들은 MTV pattern을 갖고 있다
- 다중 app으로 구성되는 경우 이름 중복이 가능하여 `template/{app이름}/{}.html` 으로 구성한다
  - why?
    - 개별 app에 생성된 templates folder의 하위 directory는 template file로 활용된다 (default)
    - Django는 template file을 탐색하는 과정에서 `settings.py`의 `DIR`과 `INSTALLED_APPS`의 선언 순서에 따르기 때문에 이름 중복을 막고자 **template** 밑에 **app 이름**과 동일한 folder를 둔다

<br>

### 1. Project 생성

```bash
django-admin startproject {프로젝트 명}
```

<br>

### 2. Project 기본 설정 - `settings.py`

1.

```python
# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```

2.

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # app/templates/ 가 아닌 다른 폴더에 templates를 만들고 싶은 경우 명시하는 것
        'DIRS': [os.path.join(BASE_DIR, 'templates')], # project root 경로에 `templates` folder를 만들 경우 `templates`만
        # 등록된 앱에 templates folder를 모두 다 같은 templates 로 보겠다 => True
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

3.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

<br>

### 3. app 생성 (articles)

- app이름은 일반적으로 복수형으로 구성된다

  ```bash
  python manage.py startapp articles
  ```

- app 등록

  > settings.py

  ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'articles',
      'django_extensions',
  ]
  ```

<br>

### 4. `urls.py`  생성

> 프로젝트 폴더

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/',include('articles.urls'))
]
```

<br>

> 개별 app

```python
from django.urls import path
from . import views

urlpatterns = [
    #/articles/
    path('new/', views.new),
    path('create/', views.create),
    path('', views.index),
    ]
```

<br>

<br>

### MTV의 역할

<br>

#### view

- url
- request (요청 관련 정보)
- return render()

<br>

#### Template

- html
- DTL
- 반복 / 보건 /필터

<br>

#### Model

- DB

<br>

<br>

## Model in Django

<br>

### Model

: Data에 대한 단일 정보 소스

<br>

### Migrations

: 모델의 변경사항들을 데이터베이스 스키마에 반영하는 방법

<br>

#### Migration 흐름

1. Model 생성/수정/삭제 등
2. `migration` 파일 생성
   - migration file은 model의 변경사항을 기록하고, database에 반영하기 위한 코드들로 구성된다
   - migration file은 **database scheme**를 위한 `버전관리 시스템` 이라고 생각하자! -> `git`
3. `migrate`를 통한 database에 적용

<br>

| Model                       | Migration                       | ORM (Query mtehods, QuerySet API)                     |
| :-------------------------- | ------------------------------- | ----------------------------------------------------- |
| MTV pattern에서 데이터 관리 | Model로 정의된 db schema를 반영 | db를 조작하는 query문 (python 객체 조작으로 가능하다) |

<br>

<br>

## Model 활용

<br>

### 1. model 정의

> models.py

```python
from django.db import models

# Create your models here.

class Article(models.Model):
    title = models.CharField(max_length=140)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

- `models.Model`을 상속받은 class를 생성한다

- 속성으로는 내가 구성하고 싶은 table의 column의 이름을 지정하고, data type에 맞춰서 field를 정의한다

- id 필드는 자동적으로 pk 값으로 생성된다.

- 위에서 정의된 필드와 옵션 정보는 다음과 같다.

  - `CharField` :
    - `max_length` : 필수

  - `DateTimeField`
    - `auto_now_add` : (선택) 생성시에만 자동으로 해당 시간 값 설정
    - `auto_now` : (선택) 수정시마다 자동으로 해당 시간 값 설정

  - 이외의 필드는 <https://docs.djangoproject.com/ko/2.1/ref/models/fields/#field-types> 링크에서 확인!

<br>

#### `CharField` vs `TextField()`

: 실제로 `<form>` tag로 data를 받을때 `<input>`으로 받을 지 `<textarea>` 로 받을지에 따라 선택하기

<br>

### 2. migration

> Migrations are Django’s way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema.
> 마이그레이션은 django에서 모델의 변경 사항을 데이터베이스 스키마에 반영하기 위한 방법이다.

<br>

#### 2-1. makemigrations

```bash
$ python manage.py makemigrations
Migrations for 'articles':
  articles/migrations/0001_initial.py
    - Create model Article
```

- 정의된 model을 database에 반영하기 위해서는 migration 명령어를 통해 migration file을 생성한다
- 마이그레이션 파일은 모델의 변경사항은 기록하며, app 별로 있는 migrations/ 폴더에 기록된다. 최초에 0001_initial.py 라는 파일이 생성되어 있을 것이다.
- migration file은 model의 변경사항을 관리한다
  - Modeling 한 내용을 db에 반영 할 준비를 하는 것!

<br>

#### 2-2. migrate

```bash
$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, articles, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying articles.0001_initial... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK

```

- 생성된 migration file을 database에 반영하기 위한 명령어
- 위와 같이 많아 보이는 것은 django가 기본적으로 활용하고 있는 데이터베이스 마이그레이션 파일까지 반영되었기 때문이다
  - 앞으로는 프로젝트 생성과 동시에 `python manage.py migrate` 를 하자!

<br>

<br>

### Migration Flow

- 마이그레이션 생성

  ```bash
  python manage.py makemigrations
  ```

- 마이그레이션 DB 반영 여부 확인

  ```bash
  python manage.py showmigratons
  ```

- 마이그레이션에 대응되는 SQL문 출력

  ```bash
  python manage.py sqlmigrate app_label migration_name
  ```

- 마이그레이션 파일의 내용을 DB에 최종 반영

  ```bash
  python manage.py migrate
  ```

<br>

<br>

`+`

#### admin 등록

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```

<br>

<br>

## Django ORM

> 기본적인 데이터베이스 조작을 CRUD(Create, Read, Update, Delete) operation 이라고 한다.

<br>

### ORM (Object Relational Mapping)

- DB와 OOP language 간의 호환되지 않는 data를 변환하는 programming 기법
  - ORM은 db에 저장되어 있는 값을 object로 mapping 해준다!
    - *Python 객체 조작(method 호출)으로 db를 조작하는 것!*

<br>

#### Django shell

> python interactive interpreter를 django 프로젝트에 맞게 쓸 수 있는 기능

```bash
python manage.py shell
```

- 추가적인 패키지 설치를 통해 편하게 활용할 수 있다.

  ```bash
  pip install django-extensions ipython
  ```

  - django-extensions 는 django 개발에 있어서 유용한 기능들을 기본적으로 제공한다.

    - <https://github.com/django-extensions/django-extensions>
  - `ipython` 은 인터렉티브 쉘을 조금 더 편하게 활용하기 위해서 설치

- 설치 이후에, settings.py 에 다음의 내용을 추가한다. (콤마 유의)

  ```python
  # django_crud/settings.py
  INSTALLED_APPS = [
      ...
      'django_extensions',
      'articles',
  ]
  ```

- 그리고 이제부터는 아래의 명령어를 사용한다.

  ```bash
  python manage.py shell_plus
  ```

  <br>

#### 1. 생성

```python
article = Article()
article.title = '제목'
article.content = '내용'
article.save()
```

<br>

#### 2. 조회

- 전체 데이터 조회

  ```bash
  Article.objects.all()
  >> <QuerySet [<Article: Article object (1)>]>
  ```

- 단일 데이터 조회

  > 단일 데이터 조회는 고유한 값인 id를 통해 가능하다.

  ```shell
  Article.objects.get(id=1)
  >> <Article: Article object (1)>
  ```

  ```shell
  In [2]: Article.objects.get(id=3)                                         
  Out[2]: Title: sample title & Content: sample content
  
  In [3]: Article.objects.get(pk=3)                                         
  Out[3]: Title: sample title & Content: sample content
  ```

  - id == pk!
    - 중복을 불허한다

  <br>

#### 3. 수정

```bash
a1 = Article.objects.get(id=1)
a1.title = '제목 수정'
a1.save()
```

- 수정이 되었는지  확인하기 위해서 데이터 조회를 다시 해보자

<br>

#### 4. 삭제

```python
a1 = Article.objects.get(id=1)
a1.delete()
>> (1, {'articles.Article': 1})
```

<br>

<br>

## Admin 페이지 활용

<br>

### 1. 관리자 계정 생성

```bash
$ python manage.py createsuperuser
사용자 이름 (leave blank to use 'ubuntu'): admin1
이메일 주소:
Password:
Password (again):
Superuser created successfully.
```

<br>

### 2. admin 등록

> admin 페이지를 활용하기 위해서는 app 별로 있는 admin.py에 정의 되어야 한다

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```

<br>

### 3. 확인

- /admin/ url로 접속하여, 관리자 계정으로 로그인

<br>

<br>

<br>

`+`

### Tips

```shell
$ python manage.py sqlmigrate articles 0001
BEGIN;
--
-- Create model Article
--
CREATE TABLE "articles_article" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(20) NOT NULL, "content" text NOT NULL);
COMMIT;
```

<br>

#### Fat Model

- MVC
  - M (C) V
- MTV
  - M (V) T

 -> *Make model fat!!!!*

<br>
