# Many to Many (M:N)

<br>

### 단순 모델링

```python
class Doctor(models.Model):
    name = models.CharField(max_length=10)

class Patient(models.Model):
    name = models.CharField(max_length=10)

class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

* 환자/의사 생성

  ```python
  d1 = Doctor.objects.create(name='dr.john')
  d2 = Doctor.objects.create(name='dr.kim')
  
  p1 = Patient.objects.create(name='구름')
  p2 = Patient.objects.create(name='근제')
  ```

* 예약 만들기

  ```python
  Reservation.objects.create(doctor=d1, patient=p1)
  Reservation.objects.create(doctor=d1, patient=p2)
  Reservation.objects.create(doctor=d2, patient=p1)
  ```

* 1번 의사의 예약 목록

  ```python
  d1.reservation_set.all()
  ```

* 1번 환자의 예약 목록

  ```python
  p1.reservation_set.all()
  ```

* 1번 의사의 환자 출력

  ```python
  for reservation in d1.reservation_set.all():
      print(reservation.patient.name)
  ```

<br>

<br>

### 중개 모델 활용

> 의사 - 환자들 / 환자 - 의사들로 직접 접근하기 위해서는 `ManyToManyField`를 사용한다.
>
> `through`  옵션을 통해 중개 모델을 선언한다.

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

* 마이그레이션 파일을 만들거나, migrate를 할 필요가 없다.

  * 즉, 데이터베이스에 전혀 변경되는 것은 없고, ORM 조작에서의 차이만 존재한다.

* 의사, 환자 오브젝트 가져오기

  ```python
  p1 = Patient.objects.get(pk=1)
  d1 = Doctor.objects.get(pk=1)
  ```

* 1번 환자의 의사 목록

  > `ManyToManyField` 가 정의된 `Patient` 는 직접 참조

  ```python
  p1.doctors.all()
  ```

* 1번 의사의 환자 목록

  > `Doctor` 는 직접 참조가 아니라 `Patient` 모델의 역참조.
  >
  > 즉, 기본 naming convention에 따라 참조

  ```python
  d1.patient_set.all()                                                                   
  ```

  * `related_name` : 역참조 옵션

    * 기본 값은 `{model 이름}_set` 

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

```shell
In [1]: d1 = Doctor.objects.create(name='dr.kim')                                                                  
In [2]: d2 = Doctor.objects.create(name='dr.lee')                                                                  
In [3]: p1 = Patient.objects.create(name='chloe')                                                                                                                           
In [5]: p2 = Patient.objects.create(name='camila')  
```

<br>

```shell
In [8]: Reservation.objects.create(doctor=d1, patient=p1)                                                          
Out[8]: <Reservation: Reservation object (1)>

In [9]: Reservation.objects.create(doctor=d2, patient=p2)                                                          
Out[9]: <Reservation: Reservation object (2)>
```

<br>

```shell
In [2]: pa = Patient.objects.get(pk=1)                                                                             
In [3]: pa.doctors.all()                                                                                           
Out[3]: <QuerySet [<Doctor: Doctor object (1)>]>
```



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