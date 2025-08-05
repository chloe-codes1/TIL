# Model in Django

<br>

<br>

### Django Basic Flow

1. Define `url`
   - `urls.py` is a signpost!
2. Create function to execute in `views.py`
3. Create `html` to return

<br>

<br>

## Django project / app configuration

- Django has a structure where one project has multiple apps
- Each app has an MTV pattern
- When composed of multiple apps, name duplication is possible, so structure as `template/{app name}/{}.html`
  - why?
    - Subdirectories of templates folder created in individual apps are used as template files (default)
    - Django follows the declaration order of `DIR` and `INSTALLED_APPS` in `settings.py` when searching for template files, so to prevent name duplication, create a folder with the same name as the **app name** under **template**

<br>

### 1. Project creation

```bash
django-admin startproject {project name}
```

<br>

### 2. Project basic configuration - `settings.py`

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
        # What to specify when you want to create templates in a folder other than app/templates/
        'DIRS': [os.path.join(BASE_DIR, 'templates')], # If you create a `templates` folder in the project root path, just `templates`
        # See all templates folders in registered apps as the same templates => True
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

### 3. Create app (articles)

- App names are generally composed in plural form

  ```bash
  python manage.py startapp articles
  ```

- App registration

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

### 4. Create `urls.py`

> Project folder

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/',include('articles.urls'))
]
```

<br>

> Individual app

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

### Role of MTV

<br>

#### view

- url
- request (request related information)
- return render()

<br>

#### Template

- html
- DTL
- loop / conditional / filter

<br>

#### Model

- DB

<br>

<br>

## Model in Django

<br>

### Model

: Single source of information about Data

<br>

### Migrations

: A method to reflect model changes to the database schema

<br>

#### Migration Flow

1. Model creation/modification/deletion etc.
2. Create `migration` file
   - Migration file records model changes and consists of code to reflect them in the database
   - Think of migration file as a `version control system` for **database schema**! -> `git`
3. Apply to database through `migrate`

<br>

| Model                                        | Migration                                   | ORM (Query methods, QuerySet API)                           |
| :------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ |
| Data management in MTV pattern               | Reflect db schema defined by Model         | Query statements that manipulate db (possible through Python object manipulation) |

<br>

<br>

## Model usage

<br>

### 1. Model definition

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

- Create a class that inherits from `models.Model`

- For attributes, specify the column names of the table you want to compose, and define fields according to data types

- ID field is automatically created as pk value.

- Field and option information defined above is as follows:

  - `CharField`:
    - `max_length`: Required

  - `DateTimeField`
    - `auto_now_add`: (Optional) Automatically set the time value only when creating
    - `auto_now`: (Optional) Automatically set the time value every time it's modified

  - For other fields, check the link <https://docs.djangoproject.com/ko/2.1/ref/models/fields/#field-types>!

<br>

#### `CharField` vs `TextField()`

: Choose based on whether to receive data with `<input>` or `<textarea>` when actually receiving data with `<form>` tag

<br>

### 2. migration

> Migrations are Django's way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema.
> Migration is a method for reflecting model changes to the database schema in django.

<br>

#### 2-1. makemigrations

```bash
$ python manage.py makemigrations
Migrations for 'articles':
  articles/migrations/0001_initial.py
    - Create model Article
```

- To reflect the defined model in the database, create a migration file through the migration command
- Migration files record model changes and are recorded in the migrations/ folder for each app. Initially, a file called 0001_initial.py will be created.
- Migration file manages model changes
  - Preparing to reflect modeled content in db!

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

- Command to reflect created migration file to database
- The reason it looks like a lot is because database migration files that django uses by default are also reflected
  - From now on, do `python manage.py migrate` as soon as you create a project!

<br>

<br>

### Migration Flow

- Create migration

  ```bash
  python manage.py makemigrations
  ```

- Check migration DB reflection status

  ```bash
  python manage.py showmigrations
  ```

- Output SQL statement corresponding to migration

  ```bash
  python manage.py sqlmigrate app_label migration_name
  ```

- Finally reflect migration file content to DB

  ```bash
  python manage.py migrate
  ```

<br>

<br>

`+`

#### admin registration

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

> Basic database manipulation is called CRUD(Create, Read, Update, Delete) operation.

<br>

### ORM (Object Relational Mapping)

- Programming technique to convert incompatible data between DB and OOP language
  - ORM maps values stored in db to objects!
    - *Manipulating db through Python object manipulation (method calls)!*

<br>

#### Django shell

> A function that allows you to use python interactive interpreter for django projects

```bash
python manage.py shell
```

- Can be used conveniently through additional package installation.

  ```bash
  pip install django-extensions ipython
  ```

  - django-extensions basically provides useful functions for django development.

    - <https://github.com/django-extensions/django-extensions>
  - `ipython` is installed to use interactive shell more conveniently

- After installation, add the following content to settings.py. (mind the comma)

  ```python
  # django_crud/settings.py
  INSTALLED_APPS = [
      ...
      'django_extensions',
      'articles',
  ]
  ```

- And from now on, use the following command.

  ```bash
  python manage.py shell_plus
  ```

  <br>

#### 1. Create

```python
article = Article()
article.title = '제목'
article.content = '내용'
article.save()
```

<br>

#### 2. Read

- Read all data

  ```bash
  Article.objects.all()
  >> <QuerySet [<Article: Article object (1)>]>
  ```

- Read single data

  > Single data inquiry is possible through unique value id.

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
    - Does not allow duplicates

  <br>

#### 3. Update

```bash
a1 = Article.objects.get(id=1)
a1.title = '제목 수정'
a1.save()
```

- To check if it was modified, query the data again

<br>

#### 4. Delete

```python
a1 = Article.objects.get(id=1)
a1.delete()
>> (1, {'articles.Article': 1})
```

<br>

<br>

## Using Admin Page

<br>

### 1. Create administrator account

```bash
$ python manage.py createsuperuser
사용자 이름 (leave blank to use 'ubuntu'): admin1
이메일 주소:
Password:
Password (again):
Superuser created successfully.
```

<br>

### 2. admin registration

> To use the admin page, it must be defined in admin.py for each app

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```

<br>

### 3. Verification

- Access /admin/ url and log in with administrator account

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
