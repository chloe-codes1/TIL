# Working with Datetime Objects and Timezones in Python

> Sharing how to change timezones in Python

<br>

<br>

### Converting ISO 8601 Format to datetime (KST)

![python-datetime](../../kor/images/python-datetime.png)

<br>

#### Example Explanation

```python
non_kst_date = '2020-10-23T10:36:05+03:00'
```

- This is a string in **ISO 8601 Format** with UTC +03:00

<br>

```python
seoul_timezone = pytz.timezone('Asia/Seoul')
```

- You can set the timezone using the **pytz** library

<br>

```python
parsed_date = datetime.strptime(non_kst_date, '%Y-%m-%dT%H:%M:%S%z')
```

- Converts the string format to a **datetime object**

<br>

```python
kst_date = parsed_date.astimezone(seoul_timezone)
```

- Converts the datetime object to the **Asia/Seoul timezone**

<v>

Done!
