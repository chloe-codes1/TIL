# Form and ModelForm

<br>

<br>

### `.order_by()`

> pk 역순으로 정렬

```python
articles = Article.objects.order_by('-pk')
```

<br>

<br>

## ModelForm

<br>

### ModelForm 정의하기

> forms.py

```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    title = forms.CharField(
        max_length=100,
        label='Title',
        help_text='Your title must be no more than 100 characters in length',
        widget=forms.TextInput(
            attrs={
                'class':'my_input',
                'placeholder': "What's on your mind?"
            }
        )
    )
    content = forms.CharField(
        label='Content',
        help_text='Jot down random musings and thoughts',
        widget=forms.Textarea(
            attrs={
                'row':5,
                'col':50,
            }
        )
    )
    class Meta:
        model = Article
        # 다 때려박아
        fields = '__all__'
```

<br>

### View에서 `ModelFrom` 활용

> view.py

```python
from django.shortcuts import render, redirect, get_object_or_404
from django.views.decorators.http import require_POST
from .models import Article
from .forms import ArticleForm

# Create your views here.
def index(request):
    articles = Article.objects.order_by('-pk')
    context = {
        'articles': articles
    }
    return render(request, 'articles/index.html', context)

def create(request):
    # POST /articles/create/
    if request.method == 'POST':
        # Article table에 data를 저장함
        form = ArticleForm(request.POST)
        if form.is_valid():
            form.save()
            #detail로 redirect
            return redirect('articles:index')
        print('errors?',form.errors)
        print('cleaned_data?',form.cleaned_data)
        
    # GET /articles/create    
    else:
        # 빈 껍데기 input form 
        form = ArticleForm()
    
    context = {
        'form': form,
    }
    return render(request, 'articles/form.html', context)


def detail(request, pk):
    article = get_object_or_404(Article, id=pk)
    context ={
        'article':article
    }
    return render(request, 'articles/detail.html', context)

@require_POST
def delete(request, pk):
    article = get_object_or_404(Article, id=pk)
    article.delete()
    return redirect('articles:index')

def update(request, pk):
    article = get_object_or_404(Article, id=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST,instance=article)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
        else:
            form = ArticleForm(instance=article)
        context = {
            'form':form
        }
        return render(request, 'articles/form.html', context)
```

<br>

### `request.resolver_match.url_name` 으로 조건에 따른 처리

> form.html

- 분기의 기준은 `url_name` 이다

- `path`로 하면, `url`이 바뀔 때마다 바꿔줘야 한다!

```html
{% if request.resolver_match.url_name == 'create' %}

    <h2>Write a post</h2>
    
{% else %}

    <h2>Edit post</h2>

{% endif %}
```

<br>

<br>

### `loop` or `bootstrap4` 활용하여 출력하기

> form.html

```html
{% extends 'base.html' %}
{% load bootstrap4 %}

{% block body %}


    {% if request.resolver_match.url_name == 'create' %}

    <h2>Write a post</h2>
    
    {% else %}

    <h2>Edit post</h2>

    {% endif %}
    
    <!-- loop 활용-->
    <form action="" method="POST">
        {% csrf_token %}
        {% for field in form %}
            <div class="fieldWrapper">
                {{ field.errors }}
                {{ field.label_tag }} <br> 
                
                {{ field }}
                {% if field.help_text %}
                
                <p class="help">{{ field.help_text|safe }}</p>
                {% endif %}
            </div>
        {% endfor %}

        <input type="submit" value="Submit">
    </form>

    <!-- bootstrap4 사용 -->
    <form action="" method="POST">
        {% csrf_token %}
        {% bootstrap_form form %}
        <button class="btn btn-primary"> Submit</button>
    </form>

{% endblock %}
```

<br>

<br>

> shell 들어가기

```bash
python manage.py shell_plus
```

<br>

> shell

```shell
In [1]: from articles.forms import ArticleForm                                                                                               

In [2]: form = ArticleForm()                                                                                                                 

In [3]: form                                                                                                                                 
Out[3]: <ArticleForm bound=False, valid=Unknown, fields=(title;content)>
```

<br>

> `p` tag 로 이루어진 input들의 집합

```shell
In [4]: form.as_p()                                                                                                                          
Out[4]: '<p><label for="id_title">Title:</label> <input type="text" name="title" maxlength="100" required id="id_title"></p>\n<p><label for="id_content">Content:</label> <textarea name="content" cols="40" rows="10" required id="id_content">\n</textarea></p>'
```

<br>

> table로 이루어진 input들의 집합

```shell
In [5]: form.as_table()                                                                                                                      
Out[5]: '<tr><th><label for="id_title">Title:</label></th><td><input type="text" name="title" maxlength="100" required id="id_title"></td></tr>\n<tr><th><label for="id_content">Content:</label></th><td><textarea name="content" cols="40" rows="10" required id="id_content">\n</textarea></td></tr>'
```

<br>

```shell
In [3]: from articles.forms import ArticleForm                                                            

In [4]: form = ArticleForm({'title':'제목'})                                                              

In [5]: print(form)                                                                                       
<tr><th><label for="id_title">Title:</label></th><td><input type="text" name="title" value="제목" maxlength="140" required id="id_title"></td></tr>
<tr><th><label for="id_content">Content:</label></th><td><ul class="errorlist"><li>This field is required.</li></ul><textarea name="content" cols="40" rows="10" required id="id_content">
</textarea></td></tr>
```

<br>

<br>

### Looping over the form’s fields

If you’re using the same HTML for each of your form fields, you can reduce duplicate code by looping through each field in turn using a `{% for %}` loop:

```
{% for field in form %}
    <div class="fieldWrapper">
        {{ field.errors }}
        {{ field.label_tag }} {{ field }}
        {% if field.help_text %}
        <p class="help">{{ field.help_text|safe }}</p>
        {% endif %}
    </div>
{% endfor %}
```

<br>

<br>

### Form rendering options

> There are other output options though for the ``/`` pairs:

- `{{ form.as_table }}` will render them as table cells wrapped in tags
- `{{ form.as_p }}` will render them wrapped in `` tags
- `{{ form.as_ul }}` will render them wrapped in `` tags

Note that you’ll have to provide the surrounding `` or `` elements yourself.

Here’s the output of `{{ form.as_p }}` for our `ContactForm` instance:

<br>

<br>

### Django Bootstrap 사용하기

<br>

> Install

```bash
pip install django-bootstrap4
```

<br>

> settings.py 수정

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
    'bootstrap4',
]
```

<br>

> base.html에 bootstrap 사용할거라고 선언

```html
<!DOCTYPE html>
{% load bootstrap4 %}
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django Test</title>
    {% bootstrap_css %}
</head>
<body>
  <h1 class="text-center">CRUD with ModelForm</h1>
    <div class="w-75 m-auto">
    <hr>
      {% block body %}

      {% endblock %}
    </div>
    {% bootstrap_javascript jquery='full'%}
</body>
</html>
```

<br>

> detail.html - bootstrap 적용되는 template들에도 선언

```html
{% extends 'base.html' %}
{% load bootstrap4 %}

{% block body %}
    <h2>Detail</h2>
    <hr>
    <p ><a href="{% url 'articles:index' %}"> Back</a></p>
    <h3>Post # {{article.pk}}</h3>
    <h4>{{article.title}}</h4>
    <p>Created at {{article.created_at|date:'Y-m-d H:i'}}</p>
    <p>Updated at {{article.updated_at|date:'Y-m-d H:i'}}</p>
    <hr>
    <p>{{article.content|linebreaks}}</p>
     <form action="{% url 'articles:update' article.pk %}" method="POST" class="d-inline">
        {% csrf_token %}
        <button class="btn btn-warning">수정</button>   
    </form>

    <form action="{% url 'articles:delete' article.pk %}" method="POST" class="d-inline">
        {% csrf_token %}
        <button class="btn btn-danger">삭제</button>   
    </form>

{% endblock  %}
```

<br>

<br>

`+`

### Git

> 특정 commit을 기준으로 돌아가기

```bash
git checkout f008d8f
```

<br>

> test branch 만들면서 이동하기

```bash
$ git checkout -b test
$ git log --oneline
f008d8f (HEAD -> test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> reference log 확인

```bash
git reflog
```

<br>

> 어디에 head 있는지 확인

```bash
$ git log --oneline
fc58709 (HEAD -> master, origin/master, origin/HEAD) README.md 추가
fd2e992 06 | Article C with ModelForm
f008d8f (test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> 다시 test branch로 돌아가기

```bash
$ git checkout test
Switched to branch 'test'
```

<br>
