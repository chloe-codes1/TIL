# AJAX

<br>

## What is AJAX?

- Asynchronous JavaScript And Xml
  - Sends **asynchronous requests**

<br>

<br>

### AJAX Request

: Sends an `XHR`

<br>

### XMLHttpRequest (XHR)

- Use `XMLHttpRequest (XHR)` objects to interact with servers.
- You can retrieve data from a URL without having to do a full page refresh.
- This enables a Web page to update just part of a page without disrupting what the user is doing.
- XMLHttpRequest is used heavily in AJAX programming.

<br>

<br>

## Django API: Building Ping-Pong

<br>

> Creating a virtual environment

```bash
python -m venv venv
```

<br>

> Making the project find pip list here

```bash
source venv/bin/activate
```

<br>

> Installing pip inside the virtual environment

```bash
(venv)
chloe@chloe-XPS-15-9570 ~/Workspace/VanillaJS/live/AJAX
$ pip -m pip install --upgrade pip
```

<br>

> Installing django inside the virtual environment

```bash
(venv)
chloe@chloe-XPS-15-9570 ~/Workspace/VanillaJS/live/AJAX
$ pip install django==2.1.15
```

<br>

### Using the `art` package

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
    <title>Art</title>
</head>
<body>
    <label for="userInput">Input: </label>
    <input id="userInput" name="inputText" type="text">
    <pre id="resultArea">

    </pre>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script>
        // 1. On the 'change' event of input#userInput, send the value to '/art/pong'
        const userInput = document.querySelector('#userInput')
        userInput.addEventListener('input', function(event){
            // input type="text" focus out === enter
            const inputText = userInput.value
            // 2. pong receives it and sends a response back as JSON
            axios.get('/arts/pong/', {
                params: {
                    inputText: inputText,
                }
            })
                .then(function(res){
                 // 3. Display the content of the response JSON in div#resultArea
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

## Implementing Likes with AJAX

<br>

1. Send a request to the data manipulation URL (Django app) through AJAX (HTTP Request sent by the browser)
2. Based on the received response data, change only the heart's HTML attributes

<br>

### `index.html`

```html
{% extends 'base.html' %}

{% block content %}
  <h2>INDEX</h2>
  {% for article in articles %}
    <h3>Author: {{ article.user }}</h3>
    <h4>Title: {{ article.title }}</h4>
    <p>Content: {{ article.content }}</p>
    <span>AJAX method</span>

      {% if user in article.like_users.all %}
        <i class="fas fa-heart fa-lg likeButtons" style="color:crimson" data-id="{{article.pk}}"></i>
      {% else %}
      <i class="fas fa-heart fa-lg likeButtons" style="color:black" data-id="{{article.pk}}"></i>
      {% endif %}

    <span>Traditional method</span>
    <a href="{% url 'articles:like' article.pk %}">
      {% if user in article.like_users.all %}
        <i class="fas fa-heart fa-lg" style="color:crimson"></i>
      {% else %}
        <i class="fas fa-heart fa-lg" style="color:black"></i>
      {% endif %}
    </a>
    <span id="likeCount-{{article.pk}}">{{article.like_users.all|length}}</span> people like this post.
    <hr>
  {% endfor %}
  <a href="{% url 'articles:create' %}">CREATE</a>

    <script>
      const likeButtonList = document.querySelectorAll('.likeButtons')
      likeButtonList.forEach(likeButton => {
        likeButton.addEventListener('click', e => {
        // 1. Send request with axios (like)
        //const articleID = e.target.getAttribute('data-id')
        const articleID = e.target.dataset.id
                          // -> Attributes starting with data- are stored in dataset and can be retrieved by the id after the dash

        {% if user.is_authenticated %}
          axios.get(`/articles/${articleID}/like_api/`)
            .then( res => {
              // Things to do after receiving the result

              likeCount = document.querySelector(`#likeCount-${articleID}`).innerText = res.data.count

              // If the current value stored in db is liked=True,
              if (res.data.liked){
                e.target.style.color = 'crimson'
              }else{
                e.target.style.color = 'black'
              }
            })
        {% else %}
            alert('Non-logged-in users cannot press the like button :(')
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
