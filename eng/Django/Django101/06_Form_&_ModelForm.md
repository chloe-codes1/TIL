# Form and ModelForm

<br>

<br>

### `.order_by()`

> Sort in reverse order by pk

```python
articles = Article.objects.order_by('-pk')
```

<br>

<br>

## ModelForm

<br>

### Defining ModelForm

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
        # Include all fields
        fields = '__all__'
```

<br>

### Using `ModelForm` in View

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
        # Save data to Article table
        form = ArticleForm(request.POST)
        if form.is_valid():
            form.save()
            # redirect to detail
            return redirect('articles:index')
        print('errors?',form.errors)
        print('cleaned_data?',form.cleaned_data)
        
    # GET /articles/create    
    else:
        # Empty input form 
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

### Conditional processing with `request.resolver_match.url_name`

> form.html

- The basis for branching is `url_name`

- If you use `path`, you have to change it every time the `url` changes!

```html
{% if request.resolver_match.url_name == 'create' %}

    <h2>Write a post</h2>
    
{% else %}

    <h2>Edit post</h2>

{% endif %}
```

<br>

<br>

### Output using `loop` or `bootstrap4`

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
    
    <!-- Using loop -->
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

    <!-- Using bootstrap4 -->
    <form action="" method="POST">
        {% csrf_token %}
        {% bootstrap_form form %}
        <button class="btn btn-primary"> Submit</button>
    </form>

{% endblock %}
```

<br>

<br>

> Enter shell

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

> Collection of inputs composed of `p` tags

```shell
In [4]: form.as_p()                                                                                                                          
Out[4]: '<p><label for="id_title">Title:</label> <input type="text" name="title" maxlength="100" required id="id_title"></p>\n<p><label for="id_content">Content:</label> <textarea name="content" cols="40" rows="10" required id="id_content">\n</textarea></p>'
```

<br>

> Collection of inputs composed of table

```shell
In [5]: form.as_table()                                                                                                                      
Out[5]: '<tr><th><label for="id_title">Title:</label></th><td><input type="text" name="title" maxlength="100" required id="id_title"></td></tr>\n<tr><th><label for="id_content">Content:</label></th><td><textarea name="content" cols="40" rows="10" required id="id_content">\n</textarea></td></tr>'
```

<br>

```shell
In [3]: from articles.forms import ArticleForm                                                            

In [4]: form = ArticleForm({'title':'title'})                                                              

In [5]: print(form)                                                                                       
<tr><th><label for="id_title">Title:</label></th><td><input type="text" name="title" value="title" maxlength="140" required id="id_title"></td></tr>
<tr><th><label for="id_content">Content:</label></th><td><ul class="errorlist"><li>This field is required.</li></ul><textarea name="content" cols="40" rows="10" required id="id_content">
</textarea></td></tr>
```

<br>

<br>

### Looping over the form's fields

If you're using the same HTML for each of your form fields, you can reduce duplicate code by looping through each field in turn using a `{% for %}` loop:

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

> There are other output options though for the `<label>`/`<input>` pairs:

- `{{ form.as_table }}` will render them as table cells wrapped in `<tr>` tags
- `{{ form.as_p }}` will render them wrapped in `<p>` tags
- `{{ form.as_ul }}` will render them wrapped in `<li>` tags

Note that you'll have to provide the surrounding `<table>` or `<ul>` elements yourself.

Here's the output of `{{ form.as_p }}` for our `ContactForm` instance:

<br>

<br>

### Using Django Bootstrap

<br>

> Install

```bash
pip install django-bootstrap4
```

<br>

> Modify settings.py

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

> Declare that you will use bootstrap in base.html

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

> detail.html - Also declare in templates where bootstrap is applied

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
        <button class="btn btn-warning">Edit</button>   
    </form>

    <form action="{% url 'articles:delete' article.pk %}" method="POST" class="d-inline">
        {% csrf_token %}
        <button class="btn btn-danger">Delete</button>   
    </form>

{% endblock  %}
```

<br>

<br>

`+`

### Git

> Go back to specific commit

```bash
git checkout f008d8f
```

<br>

> Create test branch and move

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

> Check reference log

```bash
git reflog
```

<br>

> Check where head is

```bash
$ git log --oneline
fc58709 (HEAD -> master, origin/master, origin/HEAD) README.md added
fd2e992 06 | Article C with ModelForm
f008d8f (test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> Go back to test branch

```bash
$ git checkout test
Switched to branch 'test'
```

<br> 
