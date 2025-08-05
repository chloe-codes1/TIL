# One-To-Many Relationship

<br>

### OR operation in ORM

> Use Q

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

- When querying (method)

- #### Lookup

    - `get()`
      - Returns the **object** matching the given lookup parameters
      - Returns exactly one or Error occurs
      - ex) **RUD (Read / Update / Delete)**
    - `filter()`
      - Returns a new **QuerySet** containing objects that match the given lookup parameters.
        - (if none, returns empty QuerySet)
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

- Django query for individual Object CRUD

- Used when you want to see QuerySet as combined results

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

- Manipulate necessary values from results fetched from DB

<br>

<br>

## 1:N (one to many)

- *1 has many N*
- *N must belong to 1*
  - (Therefore cascading is possible)
  - ex)
    - Article has many Comments
  - Comment belongs to Article
- `Foreign Key` is given to **N**

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
    #reporter is a name we created, but it's best practice to match the model name!
```

- A `reporter_id` column is added to the `articles_article` table.
- In the case of `reporter`, you can fetch N items (QuerySet) with `article_set`.
- In the case of `article`, you can fetch 1 corresponding object with `reporter`.
- `on_delete` : When the referenced target is deleted
  - `CASCADE`
    - When the corresponding object(`reporter`) is deleted, all referencing objects(`article`) are also deleted
  - `PROTECT`
    - Deletion is prohibited if referencing objects(`article`) exist
  - `SET_NULL`
    - Replace with **NULL** value
    - Cannot be used if **NOT NULL** option exists
  - `SET_DEFAULT`
    - Reference the default value(`article`)

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

## Basic Queries

<br>

### 1. Preparation

```python
Reporter.objects.create(username='요트맨')
Reporter.objects.create(username='chloe')
Reporter.objects.create(username='camila')
Reporter.objects.create(username='bella')

r1 = Reporter.objects.get(pk=1)
```

<br>

### 2. Create article (N)

```shell
In [3]: article = Article()                             

In [4]: article.title = '제목1'                         

In [5]: article.content = '내용1'                       

In [6]: r1 = Reporter.objects.get(pk=1)                 

In [7]: article.reporter = r1                           
  # reporter_id stores numbers(INTEGER)
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

### 3. Using 1:N Relationship

```python
# 1. Article's author
a2 = Article.objects.get(pk=2)
a2.reporter

# 2. Article's author username
a2.reporter.username

# 3. Article's author id
a2.reporter.id
a2.reporter_id

# 4. Author(1)'s articles
r1 = Reporter.objects.get(pk=1)
r1.article_set.all()
# -> <QuerySet [<Article: Article object(2)>]

# 5. All articles written by the author of article #1
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

#### Important Note

```shell
In [11]: comment.article_pk                                                                                        
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-11-e72fca1b8134> in <module>
----> 1 comment.article_pk

AttributeError: 'Comment' object has no attribute 'article_pk'
```

- It must be `article_id`
  - Aliases cannot be used!

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

- To avoid calling with the default **related_name** `.comment_set`, modify `models.py`

  ```python
  class Comment(models.Model):
      content = models.TextField()
      article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
                                  # pointing to Article among models
      
      def __str__(self):
          return f'Comment #{self.pk} for Post #{self.article_id}'
  ```

  - Set `related_name`= 'comments'

    - However, since this is just changing an option, **migration** is not needed!

    <br>

- After modification, can be called with `comments`

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
  - We don't want to have a situation where a foreign key value has no matching primary key value in the primary table.
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

- allows the user to apply business rules to the database that aren't covered by any of the other three data integrity types.

<br>

<br>

### Django settings.py

<https://github.com/django/django/blob/master/django/conf/global_settings.py>

For reference

<br>

<br>

*Update, delete can be applied to individual objects and querysets*

<br>

<br>

## Exercises

<br>

### Preparation

> Create `onetomany` app

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

### Problems

1. Articles written by user #1

   ```python
   u1.article_set.all()
   ```

2. Print all content of comments written by user #2

   ```python
   for comment in u2.comment_set.all():
       print(comment.content)
   ```

3. Print all content of comments written on article #3

   ```python
   for comment in a3.comment_set.all():
       print(comment.content)
   ```

   ```html
   {% for comment in article.comment_set.all %}
      {{ comment.content }}
   {% endfor %}
   ```

4. Posts with title "1글"

   ```python
   Article.objects.filter(title='1글')
   ```

5. Posts containing the word "글"

   ```python
   Article.objects.filter(title__contains='글')
   ```

6. Comments(N) where the corresponding article(1) title is "1글"

   ```python
   Comment.objects.filter(article__title='1글')
   print(Comment.objects.filter(article__title='1글').query)
   ```

   - Filtering by 1's column in 1:N relationship

     ```sql
     SELECT "onetomany_comment"."id", "onetomany_comment"."content", "onetomany_comment"."article_id", "onetomany_comment"."user_id" FROM "onetomany_comment" INNER JOIN "onetomany_article" ON ("onetomany_comment"."article_id" = "onetomany_article"."id") WHERE "onetomany_article"."title" = 1글
     ```

<br>

<br>

`+`

### Open `sqlite` with Django handling

```bash
python manage.py dbshell
```

<br>

### Option to directly show ORM query in Shell

```shell
python manage.py shell_plus --print-sql
``` 
