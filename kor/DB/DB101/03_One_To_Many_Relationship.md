# One-To-Many Relationship

<br>

### ORM에서의 *or* 연산

> Q를 활용한다

```shell
In [1]: from django.db.models import Q                  

In [2]: User.objects.filter(Q(age=30) | Q(last_name='김'
   ...: )).count()                                      
Out[2]: 25
```

<br>

### QuerySet

```shell
In [4]: User.objects.all()                              
Out[4]: <QuerySet [<User: User object (1)>, <User: User object (2)>, <User: User object (3)>, <User: User object (4)>, <User: User object (5)>, <User: User object (6)>, <User: User object (7)>, <User: User object (8)>, <User: User object (9)>, <User: User object (10)>, <User: User object (11)>, <User: User object (12)>, <User: User object (13)>, <User: User object (14)>, <User: User object (15)>, <User: User object (16)>, <User: User object (17)>, <User: User object (18)>, <User: User object (19)>, <User: User object (20)>, '...(remaining elements truncated)...']>

In [5]: type(User.objects.all())                        
Out[5]: django.db.models.query.QuerySet
```

- Query (method) 할 때

- #### 조회 (loop up)

    - `get()`
      - Returns the **object** matching the given lookup parameters
      - return오직 하나 or Error 발생
      - ex) **RUD (Read / Update / Delete)**
    - `filter()`
      - Returns a new **QuerySet** containing objects that match the given lookup parameters.
        - (없으면 비어있는 QuerySet)
      - ex) **Search**
      - `AND`
        - `method chaining`
        - filter. filter. ....
      - `OR`
        - `Q Object`
        - (Q ( ) | Q ( ) )
      - `LIKE`
        - ex) age__lte
        - ex) name__startswith
    - `exclude()`
      - Returns a new QuerySet containing objects that do not match the given lookup parameters.

<br>

<br>

ex)

```shell
In [1]: Article.objects.all()                                                                                      
Out[1]: SELECT "articles_article"."id",
       "articles_article"."title",
       "articles_article"."content"
  FROM "articles_article"
 LIMIT 21

Execution time: 0.000412s [Database: default]
<QuerySet []>

In [2]: Article.objects.create(title='1st post',content='haha')                                                    
INSERT INTO "articles_article" ("title", "content")
VALUES ('1st post', 'haha')

Execution time: 0.024278s [Database: default]
Out[2]: <Article: #1 (1st post - haha)>
```

<br>

<br>

### Aggregation

- 개별 Object CRUD를 django query

- QuerySet을 합쳐진 결과로 보고싶을 때 사용

  - ex)

    ```python
    # Average price across all books.
    >>> from django.db.models import Avg
    >>> Book.objects.all().aggregate(Avg('price'))
    {'price__avg': 34.35}
    
    # Max price across all books.
    >>> from django.db.models import Max
    >>> Book.objects.all().aggregate(Max('price'))
    {'price__max': Decimal('81.20')}
    
    # Difference between the highest priced book and the average price of all books.
    >>> from django.db.models import FloatField
    >>> Book.objects.aggregate(
    ...     price_diff=Max('price', output_field=FloatField()) - Avg('price'))
    {'price_diff': 46.85}
    
    # All the following queries involve traversing the Book<->Publisher
    # foreign key relationship backwards.
    
    # Each publisher, each with a count of books as a "num_books" attribute.
    >>> from django.db.models import Count
    >>> pubs = Publisher.objects.annotate(num_books=Count('book'))
    >>> pubs
    <QuerySet [<Publisher: BaloneyPress>, <Publisher: SalamiPress>, ...]>
    >>> pubs[0].num_books
    73
    
    # Each publisher, with a separate count of books with a rating above and below 5
    >>> from django.db.models import Q
    >>> above_5 = Count('book', filter=Q(book__rating__gt=5))
    >>> below_5 = Count('book', filter=Q(book__rating__lte=5))
    >>> pubs = Publisher.objects.annotate(below_5=below_5).annotate(above_5=above_5)
    >>> pubs[0].above_5
    23
    >>> pubs[0].below_5
    12
    
    # The top 5 publishers, in order by number of books.
    >>> pubs = Publisher.objects.annotate(num_books=Count('book')).order_by('-num_books')[:5]
    >>> pubs[0].num_books
    1323
    ```

<br>

### Annotate

ex) COUNT( )

```sql
SELECT country, COUNT(country) FROM countries;
```

- DB에서 가져온 결과에서 필요한 값을 조작하여 가져옴

<br>

<br>

## 1:N (one to many)

- *1 has many N*
- *N must belong to 1*
  - (그래서 cascading이 가능하다)
  - ex)
    - Article has many Comments
  - Comment belongs to Article
- `Foreign Key`는 **N** 에게 준다

```python
from django.db import models

# 1
class Reporter(models.Model):
    username = models.CharField(max_length=10)

# N
class Article(models.Model):
    title = models.CharField(max_length=10)
    content = models.TextField()
    reporter = models.ForeignKey(Reporter, on_delete=models.CASCADE)
    #reporter는 우리가 만든 이름인데, 모델명과 같게 하는 것이 best practice!
```

- `articles_article` table에 `reporter_id` column이 추가된다
- `reporter`의 경우 `article_set`으로 N개 (QuerySet)를 가져올 수 있다.
- `article`의 경우 reporter`로 1에 해당하는 object를 가져올 수 있다
- `on_delete` : 참조 대상이 삭제되는 경우
  - `CASCADE`
    - 해당 객체(`reporter`)가 삭제 되었을 때 참조하는 객체도(`article`) 모두 삭제
  - `PROTECT`
    - 참조하는 객체(`article`)가 존재하면 삭제 금지
  - `SET_NULL`
    - **NULL** 값으로 치환
    - **NOT NULL** option이 있는 경우 활용 할 수 없음
  - `SET_DEFAULT`
    - default값(`article`)을 참조하게 함

```sql
-- sql

CREATE TABLE "aricles_article" (
 "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "title" VARCHAR(10) NOT NULL,
    "content" TEXT NOT NULL,
    "reporter_id" INTEGER NOT NULL REFERENCES "artices_reporter" ("id") DEFERRABLE INITIALLY DEFERRED
);
```

<br>

<br>

## 기본 쿼리

<br>

### 1. 준비

```python
Reporter.objects.create(username='요트맨')
Reporter.objects.create(username='chloe')
Reporter.objects.create(username='camila')
Reporter.objects.create(username='bella')

r1 = Reporter.objects.get(pk=1)
```

<br>

### 2. article 생성 (N)

```shell
In [3]: article = Article()                             

In [4]: article.title = '제목1'                         

In [5]: article.content = '내용1'                       

In [6]: r1 = Reporter.objects.get(pk=1)                 

In [7]: article.reporter = r1                           
  # reporter_id는 숫자(INTEGER)를 저장
  # article.reporter_id = 1
  
In [8]: article.save()                                  

In [9]: article                                         
Out[9]: <Article: Article object (1)>

In [10]: article.reporter                               
Out[10]: <Reporter: Reporter object (1)>

In [11]: article.reporter.username                      
Out[11]: '요트맨'
```

```python
a2 = Article.objects.create(title='제목2', conent='내용2', reporter=r1)
```

<br>

### 3. 1:N 관계 활용

```python
# 1. 글의 작성자
a2 = Article.objects.get(pk=2)
a2.reporter

# 2. 글의 작성자의 username
a2.reporter.username

# 3. 글의 작성자의 id
a2.reporter.id
a2.reporter_id

# 4. 작성자(1)의 글
r1 = Reporter.objects.get(pk=1)
r1.article_set.all()
# -> <QuerySet [<Article: Article object(2)>]

# 5. 1번 글의 작성자가 쓴 모든 글
a1 = Article.objects.get(pk=1)
a1.reporter.article_set.all()
```

- `article_set`

<br>

<br>

### Comment exercise

```shell
In [3]: comment = Comment()                                                                                        

In [4]: comment                                                                                                    
Out[4]: <Comment: Comment #None for Post #None>

In [5]: comment.content = 'Comment for Post #1'                                                                    

In [6]: comment                                                                                                    
Out[6]: <Comment: Comment #None for Post #None>

In [7]: comment.article_id                                                                                         

In [8]: comment.article_id =1                                                                                      

In [9]: comment                                                                                                    
Out[9]: <Comment: Comment #None for Post #1>
```

<br>

#### 주의 할 점

```shell
In [11]: comment.article_pk                                                                                        
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-11-e72fca1b8134> in <module>
----> 1 comment.article_pk

AttributeError: 'Comment' object has no attribute 'article_pk'
```

- 무조건 `article_id`이다
  - 별명 사용 불가!

<br>

```shell
In [12]: comment.article_id                                                                                        
Out[12]: 1

In [13]: comment.article                                                                                           
SELECT "articles_article"."id",
       "articles_article"."title",
       "articles_article"."content"
  FROM "articles_article"
 WHERE "articles_article"."id" = 1
 LIMIT 21

Execution time: 0.000417s [Database: default]
Out[13]: <Article: #1 (1st post - haha)>
```

<br>

```shell
In [16]: article = Article.objects.first()                                                                         
SELECT "articles_article"."id",
       "articles_article"."title",
       "articles_article"."content"
  FROM "articles_article"
 ORDER BY "articles_article"."id" ASC
 LIMIT 1

Execution time: 0.000373s [Database: default]

In [17]: article.comment_set                                                                                       
Out[17]: <django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager at 0x7f9603eb1ac8>

In [18]: article.comment_set.all()                                                                                 
Out[18]: SELECT "articles_comment"."id",
       "articles_comment"."content",
       "articles_comment"."article_id"
  FROM "articles_comment"
 WHERE "articles_comment"."article_id" = 1
 LIMIT 21

Execution time: 0.000308s [Database: default]
<QuerySet [<Comment: Comment #1 for Post #1>]>
```

- default **related_name**인`.comment_set`으로 호출하지 않기 위해 `models.py` 수정

  ```python
  class Comment(models.Model):
      content = models.TextField()
      article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
                                  # model 중에 Article을 가리키고 있다
      
      def __str__(self):
          return f'Comment #{self.pk} for Post #{self.article_id}'
  ```

  - `related_name`= 'comments' 로 설정함

    - 단, 여기서는 option을 바꾼 것 이므로 **migration** 안해도 됨!

    <br>

- 수정 후 `comments`로 호출 가능해짐

  ```shell
  In [2]: comment = Comment.objects.first()                                                                          
  SELECT "articles_comment"."id",
         "articles_comment"."content",
         "articles_comment"."article_id"
    FROM "articles_comment"
   ORDER BY "articles_comment"."id" ASC
   LIMIT 1
  
  Execution time: 0.000873s [Database: default]
  
  In [3]: article = comment.article                                                                                  
  SELECT "articles_article"."id",
         "articles_article"."title",
         "articles_article"."content"
    FROM "articles_article"
   WHERE "articles_article"."id" = 1
   LIMIT 21
  
  Execution time: 0.000353s [Database: default]
  
  In [4]: article                                                                                                    
  Out[4]: <Article: #1 (1st post - haha)>
  
  In [5]: comment                                                                                                    
  Out[5]: <Comment: Comment #1 for Post #1>
  
  In [6]: comment.article                                                                                            
  Out[6]: <Article: #1 (1st post - haha)>
  
  In [7]: article.comments                                                                                           
  Out[7]: <django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager at 0x7f4a84996320>
  
  In [8]: article.comments.all()                                                                                     
  Out[8]: SELECT "articles_comment"."id",
         "articles_comment"."content",
         "articles_comment"."article_id"
    FROM "articles_comment"
   WHERE "articles_comment"."article_id" = 1
   LIMIT 21
  
  Execution time: 0.000374s [Database: default]
  <QuerySet [<Comment: Comment #1 for Post #1>]>
  ```

<br><br>

## Data Seeding

<br>

### CSV -> DB

```sql
sqlite> .mode csv

sqlite> .import users.csv users_user
```

<br>

```sql
sqlite> select count(*) from users_user;
100
sqlite> .schema users_user
CREATE TABLE IF NOT EXISTS "users_user" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "first_name" varchar(20) NOT NULL, "last_name" varchar(20) NOT NULL, "age" integer NOT NULL, "country" varchar(20) NOT NULL, "phone" varchar(20) NOT NULL, "balance" integer NOT NULL);
sqlite> .headers on
sqlite> .schema users_user
CREATE TABLE IF NOT EXISTS "users_user" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "first_name" varchar(20) NOT NULL, "last_name" varchar(20) NOT NULL, "age" integer NOT NULL, "country" varchar(20) NOT NULL, "phone" varchar(20) NOT NULL, "balance" integer NOT NULL);
sqlite> select*from users_user limit 10;
id,first_name,last_name,age,country,phone,balance
1,"정호","유",40,"전라북도",016-7280-2855,370
2,"경희","이",36,"경상남도",011-9854-5133,5900
3,"정자","구",37,"전라남도",011-4177-8170,3100
4,"미경","장",40,"충청남도",011-9079-4419,250000
5,"영환","차",30,"충청북도",011-2921-4284,220
6,"서준","이",26,"충청북도",02-8601-7361,530
7,"주원","민",18,"경기도",011-2525-1976,390
8,"예진","김",33,"충청북도",010-5123-9107,3700
9,"서현","김",23,"제주특별자치도",016-6839-1106,43000
10,"서윤","오",22,"충청남도",011-9693-6452,49000
```

<br>

<br>

## Data Integrity

- the maintenance of, and the assurance of the accuracy and consistency of data over its entire life-cycle
- a critical aspect to the design, implementation and usage of any system which stores, processes, or retrieves data

<br>

### Entity Integrity

- defines each row to be unique within its table.
  - No two rows can be the same.

- To achieve this, a `primary key` can be defined.
  - The primary key field contains a unique identifier – no two rows can contain the same unique identifier.

### Referential Integrity

- concerned with relationships.
  - When two or more tables have a relationship, we have to ensure that the foreign key value matches the primary key value at all times.
  - We don’t want to have a situation where a foreign key value has no matching primary key value in the primary table.
  - This would result in an orphaned record.

So referential integrity will prevent users from:

- Adding records to a related table if there is no associated record in the primary table.
- Changing values in a primary table that result in orphaned records in a related table.
- Deleting records from a primary table if there are matching related records.

### Domain Integrity

- concerns the validity of entries for a given column.
- Selecting the appropriate data type for a column is the first step in maintaining domain integrity.
- Other steps could include, setting up appropriate constraints and rules to define the data format and/or restricting the range of possible values.

### User-Defined Integrity

- allows the user to apply business rules to the database that aren’t covered by any of the other three data integrity types.

<br>

<br>

### Django settings.py

<https://github.com/django/django/blob/master/django/conf/global_settings.py>

참고하기

<br>

<br>

*Update, delete는 개별 객체와 쿼리셋에 적용가능*

<br>

<br>

## Excercises

<br>

### 준비

> `onetomany`  app 생성

```python
# models.py
class User(models.Model):
    username = models.CharField(max_length=10)
    
class Article(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    user = models.ForeignKey(User, on_delete=models.CASCADE)

class Comment(models.Model):
    content = models.TextField()
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

```python
from onetomany.models import User, Article, Comment

# objects
u1 = User.objects.create(username='Kim')
u2 = User.objects.create(username='Lee')

a1 = Article.objects.create(title='1글', user=u1)
a2 = Article.objects.create(title='2글', user=u2)
a3 = Article.objects.create(title='3글', user=u2)
a4 = Article.objects.create(title='4글', user=u2)

c1 = Comment.objects.create(content='1글1댓', article=a1, user=u2)
c2 = Comment.objects.create(content='1글2댓', article=a1, user=u2)
c3 = Comment.objects.create(content='2글1댓', article=a2, user=u1)
c4 = Comment.objects.create(content='4글1댓', article=a4, user=u1)
c5 = Comment.objects.create(content='3글1댓', article=a3, user=u2)
c6 = Comment.objects.create(content='3글2댓', article=a3, user=u1)
```

<br>

### 문제

1. 1번 유저가 작성한 글들

   ```python
   u1.article_set.all()
   ```

2. 2번 유저가 작성한 댓글의 내용을 모두 출력

   ```python
   for comment in u2.comment_set.all():
       print(comment.content)
   ```

3. 3번 글의 작성된 댓글의 내용을 모두 출력

   ```python
   for comment in a3.comment_set.all():
       print(comment.content)
   ```

   ```html
   {% for comment in article.comment_set.all %}
      {{ comment.content }}
   {% endfor %}
   ```

4. 1글이라는 제목인 게시글들

   ```python
   Article.objects.filter(title='1글')
   ```

5. 글이라는 단어가 들어간 게시글들

   ```python
   Article.objects.filter(title__contains='글')
   ```

6. 댓글(N)들 중에 해당되는 글(1)의 제목이 1글인 것

   ```python
   Comment.objects.filter(article__title='1글')
   print(Comment.objects.filter(article__title='1글').query)
   ```

   - 1:N 관계에서 1의 열에 따라서,  필터링

     ```sql
     SELECT "onetomany_comment"."id", "onetomany_comment"."content", "onetomany_comment"."article_id", "onetomany_comment"."user_id" FROM "onetomany_comment" INNER JOIN "onetomany_article" ON ("onetomany_comment"."article_id" = "onetomany_article"."id") WHERE "onetomany_article"."title" = 1글
     ```

<br>

<br>

`+`

### Django 에게 맡겨서 `sqlite` 열기

```bash
python manage.py dbshell
```

<br>

### Shell 에서 ORM query 바로 보여주는 option

```shell
python manage.py shell_plus --print-sql
```
