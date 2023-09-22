# AJAX

<br>

## What is AJAX?

- Asynchronous JavaScript And Xml
  - **비동기 요청**을 보낸다

<br>

<br>

### AJAX 요청

: `XHR`을 보낸다

<br>

### XMLHttpREquest (XHR)

- Use `XMLHttpRequest (XHR)` objects to interact with servers.
- You can retrieve data from a URL without having to do a full page refresh.
- This enables a Web page to update just part of a page without disrupting what the user is doing.
- XMLHttpRequest is used heavily in AJAX programming.

<br>

<br>

## Django API: Ping-Pong 만들기

<br>

> 가상 환경 만들기

```bash
python -m venv venv
```

<br>

> 해당 프로젝트에서 pip list 찾게 하기

```bash
source venv/bin/activate
```

<br>

> 가상 환경 안에 pip 설치

```bash
(venv) 
chloe@chloe-XPS-15-9570 ~/Workspace/VanillaJS/live/AJAX
$ pip -m pip install --upgrade pip
```

<br>

> 가상 환경 안에 django 설치

```bash
(venv) 
chloe@chloe-XPS-15-9570 ~/Workspace/VanillaJS/live/AJAX
$ pip install django==2.1.15
```

<br>

### `art` package 사용하기

> installation

```bash
pip install art
```

<br>

### `ping.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>아-트</title>
</head>
<body>
    <label for="userInput">Input: </label>
    <input id="userInput" name="inputText" type="text">
    <pre id="resultArea">

    </pre>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script>
        // 1. input#userInput 의 'change' 이벤트 때, value값을 '/art/pong' 으로 보낸다
        const userInput = document.querySelector('#userInput')
        userInput.addEventListener('input', function(event){
            // input type="text"는 focus out === enter
            const inputText = userInput.value
            // 2. pong이 받아서 다시 JSON으로 응답을 보낸다
            axios.get('/arts/pong/', {
                params: {
                    inputText: inputText,
                }
            })
                .then(function(res){ 
                 // 3. 응답 JSON의 내용을 div#resultArea에 표시한다
                    const resultArea = document.querySelector('#resultArea')
                    resultArea.innerText = res.data.content
        })
    })
    </script>
    
</body>
</html>
```

<br>

### `views.py`

```python
from django.shortcuts import render
from django.http import JsonResponse

import art 

# Create your views here.
def ping(request):
    return render(request, 'arts/ping.html')

def pong(request):
    user_input = request.GET.get('inputText')
    art_text = art.text2art(user_input)
    data = {
        'success': True,
        'content': art_text,
    }
    return JsonResponse(data)
```

<br>

<br>

## 좋아요 AJAX로 구현하기

<br>

1. AJAX (browser가 보내는 HTTP Request)를 통해 data 조작 URL에 요청 (Django app) 을 보내서
2. 받은 응답의 data를 바탕으로, 하트만 HTML 속성 변경

<br>

### `index.html`

```html
{% extends 'base.html' %}

{% block content %}
  <h2>INDEX</h2>
  {% for article in articles %}
    <h3>작성자: {{ article.user }}</h3>
    <h4>제목: {{ article.title }}</h4>
    <p>내용: {{ article.content }}</p>
    <span>AJAX 방식</span>

      {% if user in article.like_users.all %}
        <i class="fas fa-heart fa-lg likeButtons" style="color:crimson" data-id="{{article.pk}}"></i>
      {% else %}
      <i class="fas fa-heart fa-lg likeButtons" style="color:black" data-id="{{article.pk}}"></i>
      {% endif %}
      
    <span>기존 방식</span>
    <a href="{% url 'articles:like' article.pk %}">
      {% if user in article.like_users.all %}
        <i class="fas fa-heart fa-lg" style="color:crimson"></i>
      {% else %}
        <i class="fas fa-heart fa-lg" style="color:black"></i>
      {% endif %}
    </a>
    <span id="likeCount-{{article.pk}}">{{article.like_users.all|length}}</span> 명이 이 글을 좋아합니다.
    <hr>
  {% endfor %}
  <a href="{% url 'articles:create' %}">CREATE</a>

    <script>
      const likeButtonList = document.querySelectorAll('.likeButtons')
      likeButtonList.forEach(likeButton => {
        likeButton.addEventListener('click', e => {
        // 1. axios로 요청보내기(like)
        //const articleID = e.target.getAttribute('data-id')
        const articleID = e.target.dataset.id
                          // -> data- 로 시작하는 attribute는 dataset에 저장되고, dash 뒤의 id로 데려올 수 있음
        
        {% if user.is_authenticated %}
          axios.get(`/articles/${articleID}/like_api/`)
            .then( res => {
              // 결과 받은 뒤에 할 것들
              
              likeCount = document.querySelector(`#likeCount-${articleID}`).innerText = res.data.count

              // 현재 db에 저장된 값이 liked=True 라면,
              if (res.data.liked){
                e.target.style.color = 'crimson'
              }else{
                e.target.style.color = 'black'
              }
            })
        {% else %}
            alert('비 로그인 사용자는 좋아요룰 누를 수 없어요 ㅠ_ㅠ')
        {% endif %}
      })
    })
    </script>


{% endblock %}
```

<br>

### `views.py`

```python
@login_required
def like_api(request, article_pk):
    user = request.user 
    article = get_object_or_404(Article, pk=article_pk)
    
    if article.like_users.filter(pk=user.pk).exists():
        article.like_users.remove(user)
        liked = False
    else:
        article.like_users.add(user)
        liked = True

    context = {
        'liked': liked,
        'count': article.like_users.count()
    }

    return JsonResponse(context)  
```
