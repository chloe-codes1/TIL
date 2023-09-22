# Unit Testing in Python

> Pytest와 Unittest에 대해 알아보아요

<br>

<br>

## Before getting started

<br>

### Unit testing이란?

: Module이나 application 안에 있는 개별적인 code 단위가 **예상대로 작동**하는지 확인하는 반복적인 행위

<br>

### Unit testing이 필요한 이유

- Code를 **어떻게** 작성하는지 생각하는데 도움을 준다
- **무엇**을 해야하는지에 있어서 구현 선택을 할 때, 그 선택들이 적절한지 알아내는데 도움을 준다
- Bug를 빨리 발견하고, 쉽게 고칠 수 있게 해준다
- Code 의 quality를 향상 시킬 수 있다
- 통합을 간단하게 하고, 설계를 개선할 수 있다
- Debugging process를 간결하게 해준다

<br>

### Python test frameworks

- Unittest
- Doctest
- Pytest

<br>

<br>

## Unittest 란?

- Python 표준 library와 함께 제공되는 기본 test framework
- 다른 third-party test framework만큼 범위가 넓지 않다
  - 대부분의 project에 맞는 단위 테스트를 작성하기 위해 필요한 기능만을 제공한다
- Java의 JUnit testing famework로 부터 영향을 받았다
  - 그래서 test를 위해 class를 만들지 않으면 test function을 작성할 수 없다

<br>

### Unittest example

```python
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```

<br>

### Unittest Fixtures

: Test가 수행되기 전 setup 혹은 종료 후에 clean-up 하는 과정을 의미한다

- **setUp()**

  - 각 method를 호출하기 전에 호출되는 method

- **setUpClass()**

  - 해당 class가 시작되면 단 한 번 호출되는 method

  - method에 `@classmethod` decorator를 달아줘야 하고,  argument로 `cls` 를 넘겨줘야 한다

  - ex)

    ```python
    @classmethod
    def setUpClass(cls):
        ...
    ```

- **tearDown()**

  - 각 test가 끝난 이후에 호출되는 method
  - Test 도중 **exception** 이 발생해도 실행된다
  - 단, **setUp()** method가 성공했을 경우에만 호출된다

- **tearDownClass()**

  - 해당 class가 종료된 이후 단 한 번 호출되는 method

  - 역시 method에 `@classmethod` decorator를 달아줘야 하고,  argument로 `cls` 를 넘겨줘야 한다

  - ex)

    ```python
    @classmethod
    def tearDownClass(cls):
        ...
    ```

<br><br>

## Pytest 란?

- Unittest와 달리 Class가 아닌 module의 특정 명명 규칙을 따르는 함수로 test method 를 생성할 수 있다

<br>

### Pytest Fixtures

- 다른 testing framework 와는 달리 독특한 방식으로 fixture를 제공한다

- 어떤 test가 어떤 fixture를 사용하는지 쉽게 파악할 수 있다

- ex)

  ```python
  from handler import handler
  
  @pytest.fixture()
  def load_file():
      file = None
      try:
          file = open("sample_file.json", "r")
          content = eval(file.read())
      finally:
          if file:
              file.close()
  
      return content
   
  def test_handler(load_file):
     handler(load_file)
  ```

<br>

### XFail

- 해당 test function이 fail 할 것임을 명시할 수 있다

  - 실패해야만 하는 test를 작성할 때 활용할 수 있다
    - ex) 잘못된 데이터 타입을 막기위한 test code

- ex)

  ```python
  from handler import handler
  
  @pytest.fixture()
  def load_wrong_format_file():
      file = None
      try:
          file = open("sample_file.txt", "r")
          content = eval(file.read())
      finally:
          if file:
              file.close()
  
      return content
    
  @pytest.mark.xfail
  def test_handler_with_wrong_format_file(self, load_wrong_format_file):
     handler(load_wrong_format_file)
  ```
