# MySQL with Django

> 지수언니를 위해 정리!  지수주현 화이팅!

<br>

<br>

## 1. MySQL 설정

<br>

### MySQL 접속

```bash
$ mysql -u [username] -p
```

- Password 입력

<br>

### Database 만들기 

```mysql
mysql> CREATE DATABASE [database 이름];
```

- 우리가 쓸 DB 이름은 ms_movie

<br>

### Database 목록 확인

```mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| db                 |
| finalProject       |
| ms_movie           |
| mydb               |
| mysql              |
| mysql_1            |
| performance_schema |
| phpmyadmin         |
| sys                |
| testdb             |
+--------------------+
11 rows in set (0.00 sec)
```

- ms_movie 만들어진 것 확인 가능

<br>

### 사용할 Database 선택

```mysql
mysql> use [database 이름];
```

<br>

<br>

## 2. Django 연동

<br>

### 설치

```bash
$ pip install mysqlclient
```

- 여기서 에러 발생함!

  ```bash
  $ pip install mysqlclient
  Collecting mysqlclient
    Downloading mysqlclient-1.4.6.tar.gz (85 kB)
       |████████████████████████████████| 85 kB 132 kB/s 
      ERROR: Command errored out with exit status 1:
       command: /home/chloe/Workspace/ms-movie/backend/venv/bin/python -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-jnj4kig9/mysqlclient/setup.py'"'"'; __file__='"'"'/tmp/pip-install-jnj4kig9/mysqlclient/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base /tmp/pip-pip-egg-info-3szrzd1v
           cwd: /tmp/pip-install-jnj4kig9/mysqlclient/
      Complete output (12 lines):
      /bin/sh: 1: mysql_config: not found
      /bin/sh: 1: mariadb_config: not found
      /bin/sh: 1: mysql_config: not found
      Traceback (most recent call last):
        File "<string>", line 1, in <module>
        File "/tmp/pip-install-jnj4kig9/mysqlclient/setup.py", line 16, in <module>
          metadata, options = get_config()
        File "/tmp/pip-install-jnj4kig9/mysqlclient/setup_posix.py", line 61, in get_config
          libs = mysql_config("libs")
        File "/tmp/pip-install-jnj4kig9/mysqlclient/setup_posix.py", line 29, in mysql_config
          raise EnvironmentError("%s not found" % (_mysql_config_path,))
      OSError: mysql_config not found
      ----------------------------------------
  ERROR: Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.
  ```

- 해결 방법

  ```bash
  $ sudo apt-get install libmysqlclient-dev
  ```

  ```bash
  $ sudo apt-get install python-dev
  ```

  



<br>

### `settings.py` 설정

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'ms_movie',
        'USER': '유저이름',
        'PASSWORD': '비밀번호',
        'HOST': 'localhost',
        'PORT': '3306',
        'OPTIONS': {
            'init_command': 'SET sql_mode="STRICT_TRANS_TABLES"'
        }
    }
}
```

- 유저이름 / 비밀번호는 슬랙으로 공유할게! 가즈아!

<br>

