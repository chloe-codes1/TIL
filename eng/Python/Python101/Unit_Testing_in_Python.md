# Unit Testing in Python

> Let's learn about Pytest and Unittest

<br>

<br>

## Before getting started

<br>

### What is Unit Testing?

: A repetitive activity of verifying that individual code units within a module or application **work as expected**

<br>

### Why Unit Testing is Necessary

- Helps you think about **how** to write code
- Helps determine whether implementation choices are appropriate when deciding **what** needs to be done
- Allows you to find bugs quickly and fix them easily
- Can improve code **quality**
- Simplifies integration and improves design
- Streamlines the debugging process

<br>

### Python test frameworks

- Unittest
- Doctest
- Pytest

<br>

<br>

## What is Unittest?

- The default test framework that comes with the Python standard library
- Not as broad in scope as other third-party test frameworks
  - Provides only the functionality needed to write unit tests suitable for most projects
- Was influenced by Java's JUnit testing framework
  - Therefore, you cannot write test functions without creating a class for testing

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

: Refers to the process of setup before a test is run or clean-up after it finishes

- **setUp()**

  - A method called before each test method is invoked

- **setUpClass()**

  - A method called only once when the class starts

  - The method must have the `@classmethod` decorator and `cls` must be passed as an argument

  - ex)

    ```python
    @classmethod
    def setUpClass(cls):
        ...
    ```

- **tearDown()**

  - A method called after each test finishes
  - Runs even if an **exception** occurs during the test
  - However, it is only called if the **setUp()** method was successful

- **tearDownClass()**

  - A method called only once after the class finishes

  - Similarly, the method must have the `@classmethod` decorator and `cls` must be passed as an argument

  - ex)

    ```python
    @classmethod
    def tearDownClass(cls):
        ...
    ```

<br><br>

## What is Pytest?

- Unlike Unittest, Pytest allows you to create test methods as functions that follow specific naming conventions in a module, rather than requiring a Class

<br>

### Pytest Fixtures

- Provides fixtures in a unique way unlike other testing frameworks

- Makes it easy to identify which test uses which fixture

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

- Allows you to indicate that a test function is expected to fail

  - Can be used when writing tests that are supposed to fail
    - ex) Test code to prevent incorrect data types

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
