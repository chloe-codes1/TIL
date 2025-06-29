# Class Based View in Django

> [Docs](https://docs.djangoproject.com/en/3.0/topics/class-based-views/)

<br>

## Class Based View

- View 함수를 만들어주는 class

- `function-based-view` 와 비교했을 때 차이점 & 장점이 있다!

  - **GET**, **POST** 요청과 같은 HTTP method를 조건 분기가 아닌 각각의 method로 표현 할 수 있다

    HTTP method 가 class method 와 1:1 대응이라 가독성이 좋다

- 확장성이 뛰어남

  - `Mixin` 모듈을 활용하여 확장성을 극대화 할 수 있다
    - **Mixin**: class에 부가적인 기능이나 정보를 추가해주기 위한 모듈

- 로직이 복잡해도 코드의 직관성을 유지 할 수 있음

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
    # template_name = 'articles/모델명_list.html' -> 이렇게 하면 자동으로 찾음
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
