# SQL and Django ORM

<br>

## Reference Documentation

[Making queries | Django documentation | Django](https://docs.djangoproject.com/en/2.2/topics/db/queries/#making-queries)

[QuerySet API reference | Django documentation | Django](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#queryset-api-reference)

[Aggregation | Django documentation | Django](https://docs.djangoproject.com/en/2.2/topics/db/aggregation/#aggregation)

<br>

## **Basic Prerequisites**

- django app

  - Install `django_extensions`

  - Create `users` app

  - Write `models.py` according to csv file and migrate

        python manage.py sqlmigrate users 0001

- Utilize `db.sqlite3` and apply data

  - Run `sqlite3`

        $ ls
        db.sqlite3 manage.py ...
        $ sqlite3 db.sqlite3

  - Load csv file data

        sqlite > .tables
        auth_group                  django_admin_log
        auth_group_permissions      django_content_type
        auth_permission             django_migrations
        auth_user                   django_session
        auth_user_groups            auth_user_user_permissions
        users_user
        sqlite > .mode csv
        sqlite > .import users.csv users_user
        sqlite > SELECT COUNT(*) FROM users_user;
        1000

- Verification

  - Check schema in sqlite3

    ```sqlite
    sqlite > .schema users_user
    ```

<br>

<br>

## Problems

> Write SQL statements and corresponding ORM for the following problems.

### Table Creation

- django

  ```python
  # django
  class User(models.Model):
      first_name = models.CharField(max_length=10)
      last_name = models.CharField(max_length=10)
      age = models.IntegerField()
      country = models.CharField(max_length=10)
      phone = models.CharField(max_length=15)
      balance = models.IntegerField()
      
  # python manage.py makemigrations
  # python manage.py migrate
  ```

- SQL

  - Create the same table in sql.sqlite3

    ```sql
    --sql
    
    CREATE TABLE IF NOT EXISTS "users_user" (
        "id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, 
        "first_name" varchar(10) NOT NULL, 
        "last_name" varchar(10) NOT NULL, 
        "age" integer NOT NULL, 
        "country" varchar(10) NOT NULL, 
        "phone" varchar(15) NOT NULL, 
        "balance" integer NOT NULL
    );
    ```

    <br>

### Basic CRUD Logic

1. Retrieve all user records

   ```python
   # orm
   
   users = User.objects.all()
   type(users)
   # => django.db.models.query.QuerySet
   print(users.query)
   # only queryset can output sql statement
   # => SELECT "users_user"."id", "users_user"."first_name", "users_user"."last_name", "users_user"."age", "users_user"."country", "users_user"."phone", "users_user"."balance" FROM "users_user"
   ```

      ```sql
   -- sql
   
   SELECT*FROM users_user;
      ```

2. Create user record

   ```python
   # orm
   
   User.objects.create (
    first_name='구름',
       last_name='김',
       age=100,
       country='제주도',
       phone='010-1234-5678',
       balance=10000000
   )
   ```

   ```sqlite
   -- sql
   
   INSERT INTO users_user(first_name, last_name, age, country, phone, balance)
   VALUES ('주현', '김', 26, '경기도', '010-0000-0000', 100000000000);
   ```

   - Write after excluding one record and check the `NOT NULL` constraint error in both ORM and SQL.

     ```python
     # orm
     IntegrityError: NOT NULL constraint failed: users_user.age
     ```

     ```sqlite
     -- sql
     Error: NOT NULL constraint failed: users_user.last_name
     ```

3. Retrieve the specific user record

   ```python
   # orm
   
   User.objects.get(id=100)
   #=> <User: User object (100)>
   ```

   - `get` requires that the query result must be exactly one. (anything else returns an error!)

     ```python
     User.object.get(last_name='김')
     # MultipleObjectsReturned: get() returned more than one User -- it returned 24!
     User.objects.get(id=1000)
     # DoesNotExists: User matching query does not exists.
     ```

      ```sqlite
     -- sql
      ```

   SELECT * FROM users_user WHERE id = 100;

      ```
   
      ```

4. Update the specific user record

   ```python
   # orm
   
   user = User.objects.get(id=100)
   user.last_name='성'
   user.save()
   ```

      ```sql
   -- sql
   
   UPDATE users_user
   SET last_name='최'
   WHERE id=100;
      ```

5. Delete the specific user record

   ```python
   # orm
   
   User.objects.get(id=101).delete()
   ```

   ```sqlite
   -- sql
   DELETE FROM users_user
   WHERE id = 102;
   ```

<br>

### Conditional Query Statements

1. Total number of people

   ```python
   # orm
   
   # ver1)
   User.objects.all().count()
   # ver2) - use this one
   User.objects.count()
   ```

      ```sql
   -- sql
   
   -- ver1)
   SELECT COUNT(*) FROM users_user;
   
   -- ver2)
   SELECT COUNT(id) FROM users_user;
      ```

2. Names of people aged 30

   ```python
   # orm
   User.objects.filter(age=30)
   #=> <QuerySet [<User: User object (5)>, <User: User object (57)>, <User: User object (60)>]>
   
   User.objects.filter(age=30).values('first_name')
   #=> <QuerySet [{'first_name': '영환'}, {'first_name': '보람'}, {'first_name': '은영'}]>
   
   type(User.objects.filter(age=30).values('first_name')[0])  
   #=> dict
   
   print(User.objects.filter(age=30).values('first_name').query)  
   #=> SELECT "users_user"."first_name" FROM "users_user" WHERE "users_user"."age" = 30
   ```

      ```sql
   -- sql
   
   SELECT first_name FROM users_user
   WHERE age = 30;
      ```

3. Number of people aged 30 or older

   > Comparison operators
   > __gte : >=
   >
   > __gt : >
   > __lte : <=
   >
   > __lt : <

   ```python
   # orm
   User.objects.filter(age__gte=30)
   print(User.objects.filter(age__gte=30).query)
   # SELECT "users_user"."id", "users_user"."first_name", "users_user"."last_name", "users_user"."age", "users_user"."country", "users_user"."phone", "users_user"."balance" FROM "users_user" WHERE "users_user"."age" >= 30
   User.objects.filter(age__gte=30).count()
   ```

   ```sql
   -- sql
   
   SELECT COUNT(*) FROM users_user
   WHERE age>=30;
   ```

4. Number of people aged 30 with surname Kim

   ```python
   # orm -1 
   User.objects.filter(age=30).filter(last_name='김').count()
   # orm -2
   User.objects.filter(age=30, last_name='김').count()
   # query
   print(User.objects.filter(age=30).filter(last_name='김').query)
   # => SELECT "users_user"."id", "users_user"."first_name", "users_user"."last_name", "users_user"."age", "users_user"."country", "users_user"."phone", "users_user"."balance" FROM "users_user" WHERE ("users_user"."age" = 30 AND "users_user"."last_name" = 김)
   ```

      ```sql
   -- sql
   
   SELECT COUNT(*) from users_nuser
   WHERE age = 30 AND last_name ='김';
      ```

5. Number of people with area code 02

   > <https://docs.djangoproject.com/en/2.2/topics/db/queries/#escaping-percent-signs-and-underscores-in-like-statements>

   ```python
   # orm
   
   User.objects.filter(phone__startswith='02-').count()
   
   # query
   print(User.objects.filter(phone__startswith='02-').query)
   #=> SELECT "users_user"."id", "users_user"."first_name", "users_user"."last_name", "users_user"."age", "users_user"."country", "users_user"."phone", "users_user"."balance" FROM "users_user" WHERE "users_user"."phone" LIKE 02-% ESCAPE '\'
   ```

      ```sql
   -- sql
   
   SELECT COUNT(*) FROM users_user
   WHERE phone LIKE '02-%';
      ```

6. Names of people living in Gangwon-do with surname Hwang

   ```python
   # orm
   ```

      ```sql
   -- sql
      ```

<br>

### Sorting and LIMIT, OFFSET

1. Top 10 oldest people

   ```python
   # orm
   User.objects.order_by('-age')[:10]
   
   # query
   print(User.objects.order_by('-age')[:10].query)
   #=> SELECT "users_user"."id", "users_user"."first_name", "users_user"."last_name", "users_user"."age", "users_user"."country", "users_user"."phone", "users_user"."balance" FROM "users_user" ORDER BY "users_user"."age" DESC  LIMIT 10
   ```

      ```sql
   -- sql
   
   SELECT * FROM users_user
   ORDER BY age DESC
   LIMIT 10;
   
   id | first_name | last_name | age | country | phone | balance
   1 | 정호 | 유 | 40 | 전라북도 | 016-7280-2855 | 370
   4 | 미경 | 장 | 40 | 충청남도 | 011-9079-4419 | 250000
   28 | 성현 | 박 | 40 | 경상남도 | 011-2884-6546 | 580000
      ```

2. Top 10 people with lowest balance (ascending order)

   ```python
   # orm
   User.objects.order_by('balance')[:10]
   ```

      ```sql
   -- sql
   SELECT * FROM users_user
   ORDER BY balance ASC
   LIMIT 10;
      ```

3. The 5th person in descending order by last name and first name

   ```python
   # orm
   
   User.objects.order_by('-last_name', '-first_name')[4]
   #=>  <User: User object (67)>
   ```

      ```sql
   -- sql
   
   SELECT * FROM users_user
   ORDER BY last_name DESC, first_name DESC
   LIMIT 1 OFFSET 4;
   
   id | first_name | last_name | age | country | phone | balance
   67 | 보람 | 허 | 28 | 충청북도 | 016-4392-9432 | 82000
      ```

<br>

### Expressions

> To use expressions, you need to know [aggregate]([https://docs.djangoproject.com/en/2.2/topics/db/aggregation/](https://docs.djangoproject.com/en/2.2/topics/db/aggregation/)).

1. Overall average age

   ```python
   # orm
   
   from django.db.models import Avg
   User.objects.aggregate(Avg('age'))
   #=> {'age__avg': 28.23}
   ```

      ```sql
   -- sql
   
   SELECT AVG(age) FROM users_user;
   AVG(age)
   28.23
      ```

2. Average age of people with surname Kim

   ```python
   # orm
   
   from django.db.models import Avg
   User.objects.filter(last_name='김').aggregate(Avg('age'))
   ```

      ```sql
   -- sql
   
   SELECT AVG(age) FROM users_user
   WHERE last_name = '김';
      ```

3. Highest account balance

   ```python
   # orm
   
   from django.db.models import Max
   User.objects.aggregate(Max('balance'))
   ```

      ```sql
   -- sql
   
   SELECT MAX(balance) FROM users_user;
      ```

4. Total account balance

   ```python
   # orm
   
   from django.db.models import Sum
   User.objects.aggregate(Sum('balance'))
   ```

      ```sql
   -- sql
   
   SELECT SUM(balance) FROM users_user;
      ```

### Group by

> annotate adds additional fields to individual items.
> Will be used later in 1:N relationships.

1. Number of people by region

   ```python
   # orm
   
   User.objects.values('country')
    # <QuerySet [{'country': '전라북도'}, {'country': '경상남도'}, {'country': '전라남도'}, ...
   from django.db.models import Count
   User.objects.values('country').annotate(Count('country'))
   # <QuerySet [{'country': '강원도', 'country__count': 14}, {'country': '경기도', 'country__count': 9}, {'country': '경상남도', 'country__count': 9}, {'country': '경상북도', 'country__count': 15}, {'country': '전라남도', 'country__count': 10}, {'country': '전라북도', 'country__count': 11}, {'country': '제주특별자치도', 'country__count': 9}, {'country': '충청남도', 'country__count': 9}, {'country': '충청북도', 'country__count': 14}]>
   ```

   ```sql
   -- sql
   
   SELECT country, COUNT(country) FROM users_user
   GROUP BY country;
   
   country | COUNT(country)
   강원도 | 14
   경기도 | 9
   경상남도 | 9
   경상북도 | 15
   전라남도 | 10
   전라북도 | 11
   제주특별자치도 | 9
   충청남도 | 9
   충청북도 | 14
   