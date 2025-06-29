# Django REST Framework

<br>

<br>

### MVT란?

Model: 데이터 구조화

View: 데이터가 흘러다니는 곳

Template: 데이터를 표시하는 곳

<br>

### API 란?

- Application Programming Interface
  - 개발자용 접점
    - 개발자는 **Data**만 필요함!

<br>

### Request

: 요청은 URL로 보낸다!

<br>

### Data의 표기법

: 약속

<br>

- JSON
  - JavaScript Object Notation
  - Javascript 객체식 **표기법**
- XML
  - eXtended Markup Language (W3C, 1996)

<br>

### Why not HTML?

: key값이 반영이 안 됨!

- 그래서 등장한 것이 `tag`를 내맘대로 정의할 수 있는 **XML**

<br>

### Why JSON

- XML이 닫는 tag 때문에 길이가 길다
  - 돈

<br>

### 우리가 할 일

: *Django 에서 JSON 형식에 맞춰서 Data만 제공한다!*

<br>

### JSON ... 그리고 나서는?

![image-20200511121142258](../images/image-20200511121142258.png)

<br>

### Javscript & framewokr를 분리하는 이유

1. 좋은 유저 경험을 위해서

   - UX 안 좋으면 -> User X -> 돈 X

   - data -> 인간이 뭘 좋아할까?
   - 모바일 어플리케이션 (웹)
   - **churn (이탈율)**
   - JS 필수 (Adobe Flash)

2. 분리되어 있는 것이 편해서

<br>

<br>

### Django 다시 깔기

```bash
pip uninstall django

pip install django==2.1.15
```

<br>

<br>

## Faker 사용하기

<br>

### faker 설치

```bash
pip install faker
```

<br>

### Dummy data 만들기

```shell
In [1]: from faker import Faker                                                                                     

In [2]: f = Faker()                                                                                                 

In [3]: f.text()                                                                                                    
Out[3]: 'Soldier live various argue many expect important once. Next possible whom I.\nSome national left wall score few else always. Action less culture spring any night.'

In [4]: f.name()                                                                                                    
Out[4]: 'Jenna Davis'

In [5]: f.paragraph()                                                                                               
Out[5]: 'Improve knowledge hot matter himself. Growth water act bill to can discuss there. Follow out person vote action someone.'

In [6]: f.paragraph(4)                                                                                              
Out[6]: 'Early program four bill. Comput
```

<br>

<br>

## RESTful API

> <https://meetup.toast.com/posts/92> 참고하기

: url을 깔끔하게 정리하는 방식 (공통의 rule / 약속)

<br>

### RESTful

1. HTTP verb (GET, POST)
2. 명사 (복수형)로 구정

<br>

### 규칙들

- 동사 URL에 집어 넣지마!  -> `HTTP method` 활용해
  - C (POST)
    - `(POST) / articles /`
  - R (GET)
    - index (모든 정보) - `(GET) / articles /`
    - detail (하나의 정보) - `(GET) / articles / <id>`
  - U (PUT/PATCH)
    - `(PUT) / articles / <id>`
  - D (DELETE)
    - `(DELETE) / articles / <id>`
- 목적어만 URL에 집어 넣어 -> 복수형으로
  - Data

<br>

<br>

### API 관련 URL

1. subdomain
   - ex)
     - lab.ssafy.com
     - api.gitbub.com
2. 분리 URL /api/
   - ssafy.com/api/lectures/
   - github.com/api/repos/

3. versionning
   - ssafy.com/api/v1/lectures/
   - POST /api/articles/1/like/
   - POST /api/articles/1/comments/like/

<br>

<br>

## Django REST Framework (DRF)

> djangorestframework 설치

```bash
pip install djangorestframework
```

<br>

> 설치되어 있는지 확인

```bash
$ pip show djangorestframework
Name: djangorestframework
Version: 3.11.0
Summary: Web APIs for Django, made easy.
Home-page: https://www.django-rest-framework.org/
Author: Tom Christie
Author-email: tom@tomchristie.com
License: BSD
Location: /home/chloe/.local/lib/python3.6/site-packages
Requires: django
Required-by: drf-serializer-cache
```

<br>

## Serialize (직렬화)

> 포맷의 변환 (데이터를 전송/이동)

<br>

dict -> JSON (**stringify**, `serialize`)

JSON -> dict (**parse**, `deserialize`)

<br>

### 직렬화  

### : Object(언어, database) -> String (JSON)

<br>

<br>

### CREATE

![image-20200511162710246](../images/image-20200511162710246.png)

<br>

<br>

### `raise_exception`으로 Error 예쁘게 출력하기

ex)

```python
@api_view(['POST'])
def article_create(request):
    # 글을 생성
    serializer = ArticleSerializer(data=request.data)
    if serializer.is_valid(raise_exception=True):
        serializer.save()
    return Response(serializer.data)
```

<br>

> 하나만 보냄

![image-20200511162920160](../images/image-20200511162920160.png)

<br>

> 에러메시지

![image-20200511162959467](../images/image-20200511162959467.png)

<br>

<br>

## yasg

- API 관련 문서를 자동으로 생성
-

### DRF yasg 설치하기

> <https://drf-yasg.readthedocs.io/en/stable/readme.html>

```bash
pip install drf-yasg
```

<br>

<br>

## Dummy data JSON 으로 불러오기

<br>

### fixtures 폴더에 `dummy.json` 넣기

```
├── api
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── manage.py
└── musics
    ├── admin.py
    ├── apps.py
    ├── fixtures
    │   └── dummy.json
    ├── __init__.py
    ├── migrations
    ├── models.py
    ├── serializers.py
    ├── tests.py
    ├── urls.py
    └── views.py

7 directories, 29 files
```

<br>

### `loaddata` 로 dummy.json 을 DB에 넣기

```bash
$ python manage.py loaddata dummy.json
Installed 14 object(s) from 1 fixture(s)
```

<br>

### `dumpdata` 로 DB에 있는 data dumping 하기

```json
$ python manage.py dumpdata musics
[{"model": "musics.artist", "pk": 1, "fields": {"name": "Coldplay"}}, {"model": "musics.artist", "pk": 2, "fields": {"name": "Maroon5"}}, {"model": "musics.music", "pk": 1, "fields": {"artist": 2, "title": "Girls Like You"}}, {"model": "musics.music", "pk": 2, "fields": {"artist": 2, "title": "Sunday Morning"}}, {"model": "musics.music", "pk": 3, "fields": {"artist": 1, "title": "viva la vida"}}, {"model": "musics.music", "pk": 4, "fields": {"artist": 1, "title": "paradise"}}, {"model": "musics.comment", "pk": 1, "fields": {"music": 1, "content": "\uac78\uc2a4 \ub77c\uc78c \uc720!!!"}}, {"model": "musics.comment", "pk": 2, "fields": {"music": 1, "content": "\ub9c8\ub8ec \ud30c\uc774\ube0c \uc9f1\uc9f1!"}}, {"model": "musics.comment", "pk": 3, "fields": {"music": 2, "content": "\uc77c\uc694\uc77c \ubaa8\ub2dd~~~"}}, {"model": "musics.comment", "pk": 4, "fields": {"music": 2, "content": "\ud558\uc9c0\ub9cc \ub0b4\uc77c\uc740 \uc6d4\uc694\uc77c"}}, {"model": "musics.comment", "pk": 5, "fields": {"music": 3, "content": "10\ub144\uc774 \uc9c0\ub098\ub3c4 \uc88b\uc544"}}, {"model": "musics.comment", "pk": 6, "fields": {"music": 3, "content": "\ub9c8\uce58 \ub0b4\uac00 \uc655\uc774 \ub41c \uac83 \uac19\uc544!"}}, {"model": "musics.comment", "pk": 7, "fields": {"music": 4, "content": "\ud30c\ub77c\ub2e4\uc774\uc2a4 \ud30c\ub77c\ud30c\ub77c\ud30c\ub77c\ub2e4\uc774\uc2a4~"}}, {"model": "musics.comment", "pk": 8, "fields": {"music": 4, "content": "\uc228\uaca8\uc9c4 \uba85\uace1!!!"}}]
```

<br>

### `dumpdata`로 dumping 한 data를 JSON file로 만들기

> 이렇게 하면 다닥다닥 붙어있음

```bash
python manage.py dumpdata musics > dump.json
```

<br>

### indenting 줘서 예쁘게 만들기

> `--indent 2`  -> indenting을 2 줘라

```bash
python manage.py dumpdata musics --indent 2 > dump2.json
```

<br>

> result

```json
[
{
  "model": "musics.artist",
  "pk": 1,
  "fields": {
    "name": "Coldplay"
  }
},
{
  "model": "musics.artist",
  "pk": 2,
  "fields": {
    "name": "Maroon5"
  }
},
{
  "model": "musics.music",
  "pk": 1,
  "fields": {
    "artist": 2,
    "title": "Girls Like You"
  }
},
{
  "model": "musics.music",
  "pk": 2,
  "fields": {
    "artist": 2,
    "title": "Sunday Morning"
  }
},
{
  "model": "musics.music",
  "pk": 3,
  "fields": {
    "artist": 1,
    "title": "viva la vida"
  }
},
{
  "model": "musics.music",
  "pk": 4,
  "fields": {
    "artist": 1,
    "title": "paradise"
  }
},
{
  "model": "musics.comment",
  "pk": 1,
  "fields": {
    "music": 1,
    "content": "\uac78\uc2a4 \ub77c\uc78c \uc720!!!"
  }
},
{
  "model": "musics.comment",
  "pk": 2,
  "fields": {
    "music": 1,
    "content": "\ub9c8\ub8ec \ud30c\uc774\ube0c \uc9f1\uc9f1!"
  }
},
{
  "model": "musics.comment",
  "pk": 3,
  "fields": {
    "music": 2,
    "content": "\uc77c\uc694\uc77c \ubaa8\ub2dd~~~"
  }
},
{
  "model": "musics.comment",
  "pk": 4,
  "fields": {
    "music": 2,
    "content": "\ud558\uc9c0\ub9cc \ub0b4\uc77c\uc740 \uc6d4\uc694\uc77c"
  }
},
{
  "model": "musics.comment",
  "pk": 5,
  "fields": {
    "music": 3,
    "content": "10\ub144\uc774 \uc9c0\ub098\ub3c4 \uc88b\uc544"
  }
},
{
  "model": "musics.comment",
  "pk": 6,
  "fields": {
    "music": 3,
    "content": "\ub9c8\uce58 \ub0b4\uac00 \uc655\uc774 \ub41c \uac83 \uac19\uc544!"
  }
},
{
  "model": "musics.comment",
  "pk": 7,
  "fields": {
    "music": 4,
    "content": "\ud30c\ub77c\ub2e4\uc774\uc2a4 \ud30c\ub77c\ud30c\ub77c\ud30c\ub77c\ub2e4\uc774\uc2a4~"
  }
},
{
  "model": "musics.comment",
  "pk": 8,
  "fields": {
    "music": 4,
    "content": "\uc228\uaca8\uc9c4 \uba85\uace1!!!"
  }
}
]
```
