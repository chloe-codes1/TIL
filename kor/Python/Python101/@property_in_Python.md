# @property in Python

> References: [책] 파이썬 코딩의 기술 - <sub>브렛 슬라킨 지음</sub>

<br>

## Access Modifier

<br>

- Python 에는 `private` ,`public`, `protected`, `default` 등의 keyword access modifier가 존재하지 않고, 작명법 (naming)으로 제어한다

- 파이썬에서 선언되는 모든 variable과 method는 `public` 이기 때문에 `getter` 나 `setter` method가 없다!

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

### 1. Get, Set method 직접 만들어 보기

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

- 간단하지만 Pythonic 하지 않다!

<br>

<br>

### 2. `@property` , `@__.setter` decorator 사용하기

> 직접 구현할 때 보다 더 직관적으로 표현 가능!

<br>

### property class란?

- special descriptor object를 생성하는 class

  - 내부에 `getter`, `setter`,  `deleter` method를 가지고 있음

    ex)

    ```python
    p = property()
    
    print(p)
    print(p.getter)
    print(p.setter)
    print(p.deleter)
    ```

    > 실행 결과

    ![image-20200726133346788](../images/image-20200726133346788.png)

<br>

#### property decorator 사용하기

- Instance 객체의 variable 접근을 method로 제약하기 위해서는 **property 객체**로 Instance 객체의 variable을 **wrapping** 해야함

<br>

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
- method 위에 `@property` decorator를 붙이면 내부적으로 해당 method명의 instance가 만들어지고, 그 내부에 이 method가 **getter**로 등록됨

<br>

#### `@[getter_method_name].setter`

- setter의 역할

<br>

#### @property 가 setter보다 위에 있어야 한다

- `@property` 없이 @함수명.setter 만 있으면 error가 발생한다
- but, setter 없이 `@property` 만 사용하여 getter만 선언 하는 것은 가능하다
  - 이렇게 하면 **읽기 전용** private data 가 된다

<br>

<br>

### 3. `@property` decorator 를 사용하는 이유

> 제대로 대답하지 못한 것이 계속 생각나서 다시 정리,,,,흑흑 시간을 돌리고싶엉

1. 사용자가 속성에 직접 접근을 막기 위해 사용
   - `Encapsulation` 을 위해 사용
     - Class를 정의할 때 내부의 속성과 method를 묶어서 하나의 단위로 처리할 수 있는데, 이렇게 하나의 단위로 묶어서 class를 만드는 것을 `Encapsulation`이라고 한다
     - Class instance 내부에서 사용되는 변수를 **보호**하기 위한 것
       - why?
         - 외부에서 변수를 마음대로 조작이 가능하면, class 가 정해놓은 logic대로 작동하지 않고 error가 발생할 가능성이 높기 때문
         - 그래서 OOP에서는 Encapsulation 을 통해 함수 내부에서 사용되는 변수와 외부에서 사용되는 변수를 구분한다!
2. 나중에 속성을 설정할 때 특별한 동작이 일어나야 하면

3. 부모 class의 속성을 불변 (immutable) 으로 만드는 데 사용

    ex)

   ```python
   class FixedResistance(Resistor):
       # ...
       @property
       def data(self):
           return self.__data
       
       @data.setter
       def data(self, data):
           if hasattr(self, '__data'):
               raise AttributeError('You are not allowed to set attribute!')
           self.__data = data
   ```

   - 위의 객체를 생성하고 property에 할당하려고 하면 error가 발생하는 것 확인 가능

<br>

<br>

### 4. Better way to use `@property`

- @property method로 getter, setter를 구현할 때 예상과 다르게 동작하지 않도록 주의해야 함
  - getter @property method에서 다른 attribute를 설정하지 말아야 함
    - **@property.setter** method 에서만 관련 객체의 상태를 수정하기!!

- **재사용성** 은 파이썬에 내장된 @property 의 가장 큰 문제점

  - @property로 decorate 하는 method를 같은 class에  속한 여러 속성에서 사용 할 수 없다

    `+`  관련 없는 class에서도 재사용 할 수 없다

  - 그래서 **재사용** 가능한 @property method에서는 **descriptor protocol** 을 사용하는 것이 좋다

<br>

`+`

#### Descriptor Protocol

- **Descriptor class**는 반복 코드 없이도 method를 재사용 할 수 있게 해주는 `__get__` 과 `__set__` method 를 제공 할 수 있다
- 하나의 class의 서로 다른 많은 속성에 같은 logic을 재사용 할 수 있다
