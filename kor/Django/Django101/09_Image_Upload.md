# Image Upload

<br>

### 1. 필요한 package 설치하기

#### 1-1. ImageField

- 단순 ImageField를 활용하기 위해서는 `pillow` 패키지가 반드시 필요하다.

```bash
pip install pillow
```

#### 1-2. resizing

- Resizing을 위해서는 pilkit, django-imagekit 패키지가 필요하다.

```bash
pip install pilkit django-imagekit
```

<br>

### 2. model에 image column 정의

> posts > models.py

```python
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    image = models.ImageField(blank=True)
    # DB 저장 x, 호출하게 되면 잘라서 표현
    image_thumbnail = ImageSpecField(source='image',
                                      processors=[ResizeToFill(300, 300)],
                                      format='JPEG',
                                      options={'quality': 60})
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    #좋아요 기능
    like_users = models.ManyToManyField(settings.AUTH_USER_MODEL,
                                    related_name='like_posts')
```

<br>

### 3. view에 `request.FILES` 추가

> posts > views.py

```python
@login_required
def create(request):
    if request.method == 'POST':
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            post = form.save(commit=False) # 추가함
            post.user = request.user
            post.save()
            return redirect('posts:index')
        messages.warning(request, 'Please check the form submitted')
    else:
        form = PostForm()
    context = {
        'form': form
    }
    return render(request, 'posts/forms.html', context)


def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('posts:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context ={
        'form':form
    }
    return render(request, 'accounts/update.html', context)
```

<br>

### 4. `settings.py` 수정

```python
# media file 저장 경로
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

MEDIA_URL = '/media/'
```

<br>

### 5. `urls.py`에 경로 추가

```python
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('posts/', include('posts.urls')),
    path('accounts/', include('accounts.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

<br>

### 6. Templates 수정

> forms.html

```html
<form action="" method="POST" enctype="multipart/form-data">
```

<br>

> detail.html

```html
    <!--image 출력용-->
    <img src="{{post.image.url}}"/>
    <img src="{{post.image_thumbnail.url}}"/>
```

## migrations

```python
$ python manage.py makemigrations
# default값 없이 NOT NULL를 지정 => 기존 레코드에 값이 필요하다.
You are trying to add a non-nullable field 'image' to article without a default; we can't do that (the database needs something to populate existing rows).
# 2가지 옵션 제시
Please select a fix:
 # 1) 디폴트 값을 지금 설정 => python console
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 # 2) 종료하고 직접 models.py에 default 설정
 2) Quit, and let me add a default in models.py
Select an option: 1
Please enter the default value now, as valid Python
The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now
Type 'exit' to exit this prompt

```

<br>

<br>

## django-imagekit library

> Image 내부적으로 thumbnail에 맞게 자르기

<br>

#### Download & usage

<https://github.com/matthewwithanm/django-imagekit>

<br>

### Installation

```bash
pip install pilkit django-imagekit
```

<br>

### 원본 자체를 잘라서 저장

```python
ProcessedImageField(upload_to='avatars',
                                           processors=[ResizeToFill(100, 50)],
                                           format='JPEG',
                                           options={'quality': 60})
```
