# Authentication

<br>

<br>

## 회원 가입

- 비밀번호 제공 및 확인
  - `UserCreateionForm`추가 column 정의
  - 저장 logic에서 일치하는지 확인
- 비밀번호 암호화 저장
  - `User.objects.create_user(username, email=None, password=None)`
  - `user.set_password(password)`

<br>

<br>

## 로그인

<br>

*사용자가 로그인 한 사람이다?*

<br>

### Stateless & Connectless

- 매 요청이 독립 사건
  - `cookie`가 이걸 이어준다!

<br>

<br>

## User Object

```python
from django.contrib.auth.models import User
```

- core of the **authentication system**
- [`'superusers'`](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.User.is_superuser) or admin [`'staff'`](https://docs.djangoproject.com/en/3.0/ref/contrib/auth/#django.contrib.auth.models.User.is_staff) users are just user objects with special attributes set, not different classes of user objects

<br>

<img src="../images/image-20200418162725783.png" alt="image-20200418162725783" style="zoom:50%;" />

<br>

- `AbstractBaseUser`
- `AbstractUser`
- `User`

<br>

![image-20200414200102509](../images/image-20200414200102509.png)

<br>

### Primary attributes of default user

- `username`
- `password`
- `email`
- `first_name`
- `last_name`

<br>

<br>

### Creating Users

```python
from django.contrib.auth.models import User
user = User.objects.create_user('chloe', 'email-address@gmail.com', 'password-goes-here')

# At this point, user is a User object that has already been saved to the database. 

# You can continue to change its attributes, if you want to change other fields.
user.last_name = 'kim'
user.save()
```

<br>

<br>

### Changing Password

#### 1. Using command line

```bash
$ python manage.py changepassword haha
Changing password for user 'haha'
Password: 
Password (again): 
```

<br>

#### 2. Using `set_password()`

```shell
In [6]: ha = User.objects.get(username='haha')                                                                  

In [7]: ha                                                                                                      
Out[7]: <User: haha>

In [8]: ha.set_password('dkgkgkgk')                                                                             
In [9]: ha.save()             
```

<br>

<br>

### Authenticating Users

<br>

#### authenticate(*request*=None, ***credentials*)

- use it to verify a set of credentials
- takes credentials as keyword arguments
  - **username** and **password** for the default cases
- returns `User` object if credentials are valid for a backend

```python
from django.contrib.auth import authenticate
user = authenticate(username='chloe', password='dkgkgkgk')
if user is not None:
    # A backend authenticated the credentials
else:
    # No backend authenticated the credentials
```

<br>

<br>

<br>

장바구니

1. 사용자  ---> 장바구니 ---> 쿠팡
2. 사용자  <---    쿠키    <--- 쿠팡

- 장바구니 == `cookie`
- 구매내역 == `data`

<br>

*로그인 == create*

*로그아웃 == delete*

<br>

<br>

### 로그인 Form

```python
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
```

- `AutehticationForm`은 **ModelForm** 이 아니라 그냥 **Form** 이다!

<br>

### 로그인 함수

```python
from django.contrib.auth import get_user_model, login
```

<br>

```python
def signin(request):
    if request.method == 'POST':
        # 사용자가 보낸 값 -> form
        form = AuthenticationForm(request, request.POST)
        # 검증
        # -> 검증 완료 시 로그인
        if form.is_valid():
            login(request, form.get_user())
            return redirect('accounts:index')
    else:    
        form = AuthenticationForm()
    context = {
        'form':form 
    }
    return render(request, 'accounts/signin.html', context)
```

- `else`문 처리를 매끄럽게 하기 위해 첫번째 `if`로 **POST**를 먼저 거른다
  - why?
    - 만약 **GET**을 먼저 거르면, **POST**에서 `.is_valid()`에 걸리지 않고 `else` 로 떨어지면 다시 render하는 코드 써줘야해서!
    - 즉, *code의 경제성을 위해 **POST** 를 먼저 쓴다!

`+`

#### `POST` 로 먼저 분기하는 이유

1. 코드의 간결성
2. REST API 대응

- 현재 우리는 GET & POST만 대응하고 있는데 이후에 RESTful 하게 메소드 구성할 경우 GET/POST/PUT/DELETE 여러개의 메소드가 오게 되고 GET method가 마지막에에 핸들링되는 형태가 가장 간결한 코드 구성이 가능!

<br>

<br>

## Message Framework

**new**

-> 글 작성 페이지 (form)

**create**

-> DB에저장

-> render

-> redirect(성공여부)

-> redirect('articles:index')

<br>

*HTTP는 request와 response의 반복이다!*

<br>

#### HTTP

- stateless (무 상태성)
  - 한번 요청을 보내면 상태(과거)를 알 수 없음
  - 모든 요청 & 응답은 일회성이다
  - HTTP는 단절적인 protocol
- connectionless (무 연결성)

<br>

### Message Framework

- 이전의 상태를 다음 `Request` & `Response`에 넘겨준다는 것이 의미가 있다
  - Fallback Storage
    - Cookie 가 안되면 Session

<br>

<br>

## Dynamic view

<br>

Article CRUD

- title, content, create_at, updated_at

User CRUD (직접 < Django)

<br><br>

`+`

- in memory cache -> ram에 띄워놓는 cache라고 생각하면 됨
  - memcached
  - redis

- 구글 광고 아이디......gdpr
- macaddress = 기기정보
