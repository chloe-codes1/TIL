# Working with Datetime Objects and Timezones in Python

> Python에서 Timezone을 변경하는 방법을 공유해요

<br>

<br>

### ISO 8601 Format을 datetime (KST) 으로 변경하기

![python-datetime](../images/python-datetime.png)

<br>

#### 예시 설명

```python
non_kst_date = '2020-10-23T10:36:05+03:00'
```

- **ISO 8601 Format**의 UTC +03:00인 문자열이다

<br>

```python
seoul_timezone = pytz.timezone('Asia/Seoul')
```

- **pytz** library를 활용하여 timezone을 설정할 수 있다

<br>

```python
parsed_date = datetime.strptime(non_kst_date, '%Y-%m-%dT%H:%M:%S%z')
```

- String format을 **datetime object** 로 변환한다

<br>

```python
kst_date = parsed_date.astimezone(seoul_timezone)
```

- Datetime object를 **Asia/Seoul timezone**으로 변환한다

<v>

끝!
