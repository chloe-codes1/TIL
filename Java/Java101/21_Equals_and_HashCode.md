# == 연산자, equals(), hashCode

> equals와 hashCode는 모든 Java 객체의 부모 객체인 Object class에 정의되어 있다
>
> → 그렇기 때문에 Java의 모든 객체는 Object class에 정의된 equals와 hashCode 함수를 상속받고 있다

<br>

### == 연산자

- 피 연산자가 `primitive type` (int, byte, short, long, float, double, boolean, char) 일 때는 `값을 비교`하고,
- 피 연산자가 그 외 `reference type`일 때는 `가리키는 주소를 비교` 한다

<br>

### equals()

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

- 2개의 객체가 동일한지 검사하기 위해 사용된다
- 2개의 객체가 참조하는 것이 동일한지 확인하여 검사한다
  - 즉, 2개의 객체가 가리키는 곳이 `동일한 메모리 주소` 일 경우에만 동일한 객체가 된다
- 우리가 동일한 문자열 2개를 생성하면, 2개의 문자열은 서로 다른 메모리 상에 할당된다
  - but, equals를 사용하면 true인 이유는 String class에서 equals method를 `override` 하여 문자열 내용이 같으면 true를 return 하도록 재정의했기 때문이다
    - 문자열을 char 단위로 한 글자씩 모두 비교하여 동일하면 true를 return한다
    - 따라서 서로 다른 객체라도 같은 문자열을 가지고 있으면 동일한다고 판단하는 것이다

<br>

### hashCode()

```java
public native int hashCode();
```

- 객체를 식별할 수 있는 하나의 unique한 정수값을 말한다
  - Object class에서는 `heap 메모리에 저장된 객체의 메모리 주소` 를 반환하도록 되어 있다
- `native` 키워드는 method가 `JNI (Java Native Interface)` 라는 native code를 이용해 구현되었음을 의미한다
  - native는 method에만 적용 가능한 키워드로, Java가 아닌 언어로 구현된 부분을 JNI를 통해 Java에서 이용하고자 할 때 사용된다
    - Java에서 다른 언어를 사용할 수 있게 만들어주는 키워드다!
- hashCode는 `HashTable` 과 같은 자료구조를 사용할 때, `데이터가 저장되는 위치를 결정하기 위해 사용`된다
