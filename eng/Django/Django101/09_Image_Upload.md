# Image Upload

<br>

### 1. Install required packages

#### 1-1. ImageField

- To use simple ImageField, `pillow` package is absolutely required.

```bash
pip install pillow
```

#### 1-2. resizing

- For resizing, pilkit and django-imagekit packages are required.

```bash
pip install pilkit django-imagekit
```

<br>

### 2. Define image column in model

> posts > models.py

```python
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    image = models.ImageField(blank=True)
    # Not saved in DB, cropped and displayed when called
    image_thumbnail = ImageSpecField(source='image',
                                      processors=[ResizeToFill(300, 300)],
                                      format='JPEG',
                                      options={'quality': 60})
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    # Like functionality
    like_users = models.ManyToManyField(settings.AUTH_USER_MODEL,
                                    related_name='like_posts')
```

<br>

### 3. Add `request.FILES` to view

> posts > views.py

```python
@login_required
def create(request):
    if request.method == 'POST':
        form = PostForm(request.POST, request.FILES)
        if form.is_valid():
            post = form.save(commit=False) # Added
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

### 4. Modify `settings.py`

```python
# Media file storage path
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

MEDIA_URL = '/media/'
```

<br>

### 5. Add path to `urls.py`

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

### 6. Modify Templates

> forms.html

```html
<form action="" method="POST" enctype="multipart/form-data">
```

<br>

> detail.html

```html
    <!--For image output-->
    <img src="{{post.image.url}}"/>
    <img src="{{post.image_thumbnail.url}}"/>
```

## migrations

```python
$ python manage.py makemigrations
# Specifying NOT NULL without default value => existing records need values.
You are trying to add a non-nullable field 'image' to article without a default; we can't do that (the database needs something to populate existing rows).
# 2 options provided
Please select a fix:
 # 1) Set default value now => python console
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 # 2) Exit and set default in models.py directly
 2) Quit, and let me add a default in models.py
Select an option: 1
Please enter the default value now, as valid Python
The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now
Type 'exit' to exit this prompt

```

<br>

<br>

## django-imagekit library

> Crop images internally to fit thumbnails

<br>

#### Download & usage

<https://github.com/matthewwithanm/django-imagekit>

<br>

### Installation

```bash
pip install pilkit django-imagekit
```

<br>

### Crop and save the original itself

```python
ProcessedImageField(upload_to='avatars',
                                           processors=[ResizeToFill(100, 50)],
                                           format='JPEG',
                                           options={'quality': 60})
``` 
