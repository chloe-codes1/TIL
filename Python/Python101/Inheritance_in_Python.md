# Inheritance in Python

<br>

### 클래스를 상속했을 때 method 실행 방식

- 인스턴스의 메서드를 실행한다고 가정할 때 `__getattribute__()`
로 bound 된 method 를 가져온 후 메서드를 실행한다
- 메서드를 가져오는 순서는 `__mro__`
에 따른다.
  - MRO(method resolution order)는 메소드를 확인하는 순서다
  - 단일상속 혹은 다중상속일 때 어떤 순서로 메서드에 접근할지는 해당 클래스의 `__mro__`에 저장되는데 왼쪽에 있을수록 우선순위가 높다
