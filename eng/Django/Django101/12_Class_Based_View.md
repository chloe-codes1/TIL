# Class Based View in Django

> [Docs](https://docs.djangoproject.com/en/3.0/topics/class-based-views/)

<br>

## Class Based View

- Class that creates View functions

- There are differences & advantages compared to `function-based-view`!

  - HTTP methods like **GET**, **POST** requests can be expressed as individual methods rather than conditional branching

    HTTP methods have 1:1 correspondence with class methods, so readability is good

- Excellent extensibility

  - Can maximize extensibility by utilizing `Mixin` modules
    - **Mixin**: Module for adding additional functionality or information to classes

- Can maintain code intuitiveness even with complex logic

<br>

<br>

### `Function generic view`  vs  `class based generic view`

<br>

#### Function generic view

ex)

```python
def index(request):
    articles = Article.objects.all()
    return render(request, 'articles/index.html', {'articles': articles})
```

<br>

#### class based generic view

ex)

> views.py

```python
from django.views.generic import ListView, DetailView

class ArticleListView(ListView):
    model = Article
    # template_name = 'articles/model_name_list.html' -> Automatically finds this way
    # context_object_name = 'object_list'

class ArticleDetailView(DetailView):
    model = Article
```

<br>

> urls.py

```python
from django.contrib import admin
from django.urls import path
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', views.ArticleListView.as_view()),
    path('articles/<int:pk>',views.ArticleDetailView.as_view()),
]
```

<br>

<br>

`+`

### Django REST API Auth

<https://django-rest-auth.readthedocs.io/en/latest/installation.html>

<br> 
