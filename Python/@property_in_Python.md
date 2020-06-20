# @property in Python

<br>

## Access Modifier

<br>

- Python 에는 `private` ,`public`, `protected`, `default` 등의 keyword access modifier가 존재하지 않고, 작명법 (naming)으로 제어한다 

  - 첫 언어가 Java인 나에게 새로웠던 Python 의 특징!

  <br>
  
  | public             | protected               | private                  |
| ------------------ | ----------------------- | ------------------------ |
  | 접두사에 밑줄 없음 | 접두사에 밑줄 한 개 (_) | 접두사에 밑줄 두 개 (__) |

   ex)
  
  ```python
  class AcessModifiers:
      
      def __init__(self):
          pass
      
      def public(self):
          print('Public called!')
          
      def _protected(self):
          print('Protected called~~')
     	
      def __private(self):
          print('Private called!!!')
  ```

<br>

<br>

## Getters and Setters in Python

<br>

### 1. Get, Set method 만들어 보기

> 직접 구현

ex)

```python
class Student:
    def __init__(self):
        self.__name = 'chloe'
    
    def get_name(self):
        return self.__name
    
    def set_name(self):
        return self.__name = name
```

<br>

<br>

### 2. `@property` , `@__.setter` 사용하기

> 직접 구현할 때 보다 더 직관적으로 표현 가능!

ex)

```python
class Student:
    def __init__(self):
        self.__name = 'chloe'
    
    @property
    def name(self):
        return self.__name
    
    @name.setter
    def name(self, name):
        return self.__name = name
```

<br>

#### `@property`

- getter의 역할

<br>

#### `@[getter_method_name].setter`

- setter의 역할

<br>

*property 가 setter보다 위에 있어야 한다!*

<br>