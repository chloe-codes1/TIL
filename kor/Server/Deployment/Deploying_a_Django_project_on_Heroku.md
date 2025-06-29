# Deploying a Django project on Heroku

<br>

### 1. Modify `settings.py`

#### 1-1. Debug

```python
DEBUG = bool( os.environ.get('DJANGO_DEBUG', True))
```

<br>

#### 1-2. SECRET_KEY

```python
import os 
SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'YOUR_SECRET_KEY')
```

<br>

<br>

### 2. Install `Heroku`

```bash
npm install -g heroku
```

<br>

<br>

### 3. Update the app for `Heroku`

#### 3-1. `Procfile`

```
web: gunicorn [YOUR_APP_NAME].wsgi --log-file -
```

- same directory as `manage.py`

<br>

#### 3-2. Install `Gunicorn`

> The Gunicorn "Green Unicorn" is a Python Web Server Gateway Interface HTTP server.

```bash
pip install gunicorn
```

<br>

#### 3-3. Database configuration

> **dj-database-url** (Django database configuration from environment variable)

```bash
pip install dj-database-url 
```

> Add it into the bottom of the `settings.py`

```python
# Heroku: Update database configuration from $DATABASE_URL.
import dj_database_url
db_from_env = dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(db_from_env)
```

> **psycopg2** (Python Postgres database support)

```bash
pip install psycopg2-binary
```

<br>

#### 3-4. Serving static files in production

> Install `whitenoise`

```bash
pip install whitenoise
```

> Add it into the MIDDLEWEAR of the `settings.py`

```python
MIDDLEWARE = [
    'whitenoise.middleware.WhiteNoiseMiddleware',
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

> Add it into the bottom of the `settings.py`

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/2.1/howto/static-files/

STATIC_URL = '/static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),
]

STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

<br>

#### 3-5. Requirements

> The Python requirements of your web application must be stored in a file **requirements.txt** in the root of your repository

```bash
pip freeze > requirements.txt
```

<br>

#### 3-6. Runtime

> `runtime.txt`  tells Heroku which programming language to use

```txt
python-3.6.9
```

<br>

<br>

### 4. Create and upload the website

<br>

#### 4-1. Create the app

```bash
heroku create [APP_NAME]
```

<br>

#### 4-2. Push our app to the Heroku repository

```bash
git add .
git commit
git push heroku master
```

<br>

#### 4-3. Set up the database tables

```bash
heroku run python manage.py migrate
```

<br>

#### 4-4. Create superuser

```bash
heroku run python manage.py createsuperuser
```

<br>

#### 4-5. Open your app

```bash
heroku open
```

<br>

<br>

### 5. You are now live

<br>

<br>

<br>

`+`

## Heroku Tips & Tricks

<br>

### 1. Disable collectstatic

```bash
heroku config:set DISABLE_COLLECTSTATIC=1
```

<br>

<br>

### 2. [Download backup](https://devcenter.heroku.com/articles/heroku-postgres-import-export#download-backup)

To export the data from your Heroku Postgres database, create a new backup and download it.

```term
heroku pg:backups:capture
heroku pg:backups:download
```

<br>

<br>

### 3. Maintenance Mode

<br>

#### To enable maintenance mode

```bash
$ heroku maintenance:on
Enabling maintenance mode for myapp... done
```

<br>

#### To disable maintenance mode

```bash
$ heroku maintenance:off
Disabling maintenance mode for myapp... done
```

<br>

#### To check the current maintenance status of an app

```bash
$ heroku maintenance
off
```

<br>

<br>

### 4. Restart

```bash
heroku restart
```

- run this when  you see this message
  - "Your account has reached its concurrent builds limit"

<br>

<br>

### 5. Loaddata

```bash
heroku run python manage.py loaddata [YOUR_JSON_FILE_NAME]
```

<br>

<br>

### 6. [Using AWS S3 to Store Static Assets on Heroku](https://github.com/chloe-codes1/TIL/blob/master/Server/Deployment/Using_AWS_S3_to_Store_Static_Assets_on_Heroku.md)
