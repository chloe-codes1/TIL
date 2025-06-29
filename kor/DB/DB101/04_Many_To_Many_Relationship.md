# Many to Many (M:N)

<br>

## M:N

- M has many N
- N has many M

<br>

### Naming convention

- `1:N`

  - **정의**: 모델 단수형 (.user)
  - **역참조**: 모델_set (.article_set)

- `M:N`

  - **정의 및 역참조**:  모델 복수형(.like_users, like_articles)

<br>

### M:N 관계 접근

![image-20200428192056085](../images/image-20200428192056085.png)

<br>

### 1. 단순 직관적 모델링

> 위의 도식화한 애용 models.py로 옮겨보기

```python
class Doctor(models.Model):
    name = models.CharField(max_length=10)

class Patient(models.Model):
    name = models.CharField(max_length=10)

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

- 환자/의사 생성

  ```python
  d1 = Doctor.objects.create(name='dr.john')
  d2 = Doctor.objects.create(name='dr.kim')
  
  p1 = Patient.objects.create(name='구름')
  p2 = Patient.objects.create(name='근제')
  ```

- 예약 만들기

  ```python
  Reservation.objects.create(doctor=d1, patient=p1)
  Reservation.objects.create(doctor=d1, patient=p2)
  Reservation.objects.create(doctor=d2, patient=p1)
  ```

- 1번 의사의 예약 목록

  ```python
  d1.reservation_set.all()
  ```

- 1번 환자의 예약 목록

  ```python
  p1.reservation_set.all()
  ```

- 1번 의사의 환자 출력

  ```python
  for reservation in d1.reservation_set.all():
      print(reservation.patient.name)
  ```

<br>

<br>

### 2. 중개 모델 활용

> 의사 - 환자들 / 환자 - 의사들로 직접 접근하기 위해서는 `ManyToManyField`를 사용한다.
>
> `through`  옵션을 통해 중개 모델을 선언한다.

<br>

![image-20200428192226753](../images/image-20200428192226753.png)

<br>

```python
class Doctor(models.Model):
    name = models.CharField(max_length=10)

class Patient(models.Model):
    name = models.CharField(max_length=10)
    # M:N 필드! reservation 통해서, Doctor에 접근을 의미
    doctors = models.ManyToManyField(Doctor, 
                                    through='Reservation')

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

- 마이그레이션 파일을 만들거나, migrate를 할 필요가 없다.

  - 즉, 데이터베이스에 전혀 변경되는 것은 없고, ORM 조작에서의 차이만 존재한다.

- 의사, 환자 오브젝트 가져오기

  ```python
  p1 = Patient.objects.get(pk=1)
  d1 = Doctor.objects.get(pk=1)
  ```

- 1번 환자의 의사 목록

  > `ManyToManyField` 가 정의된 `Patient` 는 직접 참조

  ```python
  p1.doctors.all()
  ```

- 1번 의사의 환자 목록

  > `Doctor` 는 직접 참조가 아니라 `Patient` 모델의 역참조.
  >
  > 즉, 기본 naming convention에 따라 참조

  ```python
  d1.patient_set.all()                                                                   
  ```

- ##### `related_name` : 역참조 옵션

    <br>

    **기본 값은 `{model 이름}_set`**

    ![image-20200428192427702](../images/image-20200428192427702.png)

    - 역참조 설정이 반드시 설정되어야 하는 상황이 있다
      - `django`에서 **makemigrations** 하는 경우 직접 오류를 발생시켜 준다
      - ex) 작성자(User)-게시글(Article), 좋아요누른사람(User)-게시글(Article)
        - 위의 관계 설정시 모두 Article 클래스에 related_name 없이 정의를 하게 된다면, 역참조 이슈 발생

    ```python
    class Doctor(models.Model):
        name = models.TextField()
    
    class Patient(models.Model):
        name = models.TextField()
        # 역참조 설정. related_name
        doctors = models.ManyToManyField(Doctor, 
                            through='Reservation',
                            related_name='patients')
    
    class Reservation(models.Model):
        doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
        patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    ```

<br>

<br>

### 3. 중개 모델 없이 설정

> 일반적으로 추가 필드 구성이 필요 없이 id 값만 존재하는 경우는 아래와 같이 선언한다.

```python
class Doctor(models.Model):
    name = models.TextField()

class Patient(models.Model):
    name = models.TextField()
    doctors = models.ManyToManyField(Doctor, 
                        related_name='patients')
```

- 이 경우 앱이름_patient_doctors 로 테이블이 생성된다.

- 해당 테이블에 Create/Delete를 위해서는 (예약을 생성하거나 삭제하기 위해서는) 아래의 메소드를 활용한다.

  ```python
  d1.patients.add(p1)
  # 각각 조회 해보자.
  d1.patients.all()
  p1.doctors.all()
  ```

  ```python
  d1.patients.remove(p1)
  # 각각 조회 해보자.
  d1.patients.all()
  p1.doctors.all()
  ```

### 결론

- 중개  model이 필요 없는 경우
  - 특정 Class에 `ManyToManyField` 선언 (중개 table 자동선언)
- 중개 model이 필요한 경우 (추가 정보가 필요한 경우)
  - 중개 model 정의 후
  - 특정 Class에 `ManyToManyField`에 `through` option을 통해 조작

`+`

- `ManyToMany` 에서는 반디스 복수형의 표현으로 `related_name`을 선언하자!!

<br><br>

### id로 원하는 값 불러오기

```shell
In [13]: Reservation.objects.filter(doctor_id=3)                                                                   
Out[13]: <QuerySet [<Reservation: Reservation object (3)>]>
```

<br><br>

### Delete

> 불편한 ver.

```shell
In [18]: Reservation.objects.filter(patient_id=1,doctor_id=1).delete()                                             
Out[18]: (1, {'manytomany.Reservation': 1})
```

<br>

<br>

## 좋아요 기능

<br>

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
    users = models.ManyToManyField(settings.AUTH_USER_MODEL,
                                    related_name='like_posts')
```

<br>

```bash
$ python manage.py makemigrations
SystemCheckError: System check identified some issues:

ERRORS:
posts.Post.user: (fields.E304) Reverse accessor for 'Post.user' clashes with reverse accessor for 'Post.users'.
        HINT: Add or change a related_name argument to the definition for 'Post.user' or 'Post.users'.
posts.Post.users: (fields.E304) Reverse accessor for 'Post.users' clashes with reverse accessor for 'Post.user'.
        HINT: Add or change a related_name argument to the definition for 'Post.users' or 'Post.user'.
```

<br>

- URL - variable routing
- View - 좋아요 눌렀으면 취소, 안눌렀으면 좋아요 (Toggle)

<br>

<br>

## 팔로우 기능

<br>

- URL - variable routing
  - accoutns/1/follow
- View
  - follow 되어있는 경우 add
  - 안되어 있는 경우 remove
- Template(응답)
  - User detail redirect

<br>

<br>
