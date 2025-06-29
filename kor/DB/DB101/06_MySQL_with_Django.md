# MySQL with Django

> 지수언니를 위해 정리!  지수주현 화이팅!

<br>

<br>

## 1. MySQL 설정

<br>

### MySQL 접속

```bash
mysql -u [username] -p
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

### Database 언어설정

> DB 에 Insert 시 오류가 발생함  -> 언어설정으로 인한 문제

```bash
OperationalError: (1366, "Incorrect string value: '\\xEB\\xA1\\x9C\\xEA\\xB1\\xB4' for column 'title' at row 1")
```

<br>

#### 해결 방법

1. `my.cnf` 파일 수정

   ```bash
   sudo vi /etc/mysql/my.cnf
   ```

   ```
   ...
   
   [client]
   default-character-set=utf8
   
   [mysql]
   default-character-set=utf8
   
   [mysqld]
   collation-server = utf8_unicode_ci
   init-connect='SET NAMES utf8'
   character-set-server = utf8
   ...
   ```

   - 위의 설정 추가 후 재시작

     ```bash
     sudo /etc/init.d/mysql restart
     ```

2. `table` character set 설정

   ```mysql
   mysql> ALTER TABLE table_name convert to charset utf8;
   ```

3. `database` character set 설정

   ``` mysql
   mysql> alter database DB_NAME default character set utf8 collate utf8_general_ci;
   ```

<br>

## 2. Django 연동

<br>

### 설치

```bash
pip install mysqlclient
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
  sudo apt-get install libmysqlclient-dev
  ```

  ```bash
  sudo apt-get install python-dev
  ```

<br>

### `settings.py` 설정

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'ms_movie',
        'USER': 'root',
        'PASSWORD': os.getenv('MY_SQL_PASSWORD'),
        'HOST': 'localhost',
        'PORT': '3306',
        'OPTIONS': {
            'init_command': 'SET sql_mode="STRICT_TRANS_TABLES"',
            'charset': 'utf8mb4',
        },
         'TEST': {
            'CHARSET': 'utf8mb4',
            'COLLATION': 'utf8mb4_unicode_ci',
        }
    }
}
```

<br>

<br>

<br>

`+`

### How to handle `Django : Table doesn't exist` error

<br>

#### 1.  Drop tables

#### 2. Comment-out the model in model.py

#### 3. fake migration

```bash
python manage.py makemigrations
python manage.py migrate --fake
```

#### 4. Comment-in the model

#### 5.  migration

```bash
python manage.py makemigrations
python manage.py migrate 
```

<br>

<br>

### DROP TABLE foreign key

```mysql
SET FOREIGN_KEY_CHECKS = 0;
drop table if exists [TABLE_NAME];
SET FOREIGN_KEY_CHECKS = 1;
```
