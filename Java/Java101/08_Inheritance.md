# Inheritance in Java

<br>

## Inheritance

- Extends keyword 사용
- Java는 Single Inheritance 를 한다
  - 한번에 하나만 상속 받을 수 있다

- ex) Dog extends Animal

  => Dog라는 class는 Animal Class를 상속 받는다

- super keyword로 부모 class에 접근 가능하다 

  => super();

- 생략해도 자동 호출되는 super()는 부모의 기본 생성자를 호출한다

- 모든 객체의 부모 생성자는 object다!!!!!!!!

- 메모리에 얹어질 때는 상단에 부모, 하단에 자식

- data를 search 할 때는 하단의 자식부터 상단의 부모쪽으로 올라가는 형식 

  => 밑에서부터 찾아서 없으면 올라가는 형식

- ex) data type이 Dog이면 Animal, Object 모두 접근 가능하다-

- super를 사용하면 자식 class 하나를 jump해서 부모부터 search 할 수 있다

- is a 관계  

  => 모든 객체의 Data Type은 부모가 될 수 있다

  - data 호환은 상하 관계에서만 가능하다
    - 형제 관계에서는 안됨!
  - 부모 type은 하단부에 있는 자식 data에 접근 불가

<br>

### `super();`

- 부모의 생성자를 호출한다.
  - 지워도 자동으로 들어감!
  - 없어도 자동호출 됨!

- 안보이면 생략되어있는 것임!
- this() method처럼 first statement에만 허용된다!
  - 그래서 this() method가 사용된 생성자에서는 super() 가 없는 것을 알 수 있음
  - super.______ 하면 자식이 아니라 부모영역부터 search 할 수 있다!
- `this. Keyword`와 `super. Keyword` 모두 **heap영역**에서만 사용 가능하다!!!!

<br>

![img](https://lh5.googleusercontent.com/6Tv949yM4OxWABprfuItlzqQYXbhSzxR-EYGptVGBXO-39xikX6xOlJbM_9ZcJLff61_Y8rOeWoF4hb_YW3dwqvvPpKCJcm06_T6Hq-LHINf_uJ_cw7oo9LJX8yxgH1-20iJNeGc)

<br>

<br>

## Method Overloading

- 하나의 클래스 안에는 동일한 이름의 method가 여러개 존재할 수 있다
  - 단, method의 parameter의 type이나 개수가 달라야한다!

<br>

<br>

## Constructor

- 객체 생성시에 만들어지는 함수

- 생성자 함수의 이름은 class명과 동일-
- return type에 대해 언급하면 안됨- method overloading이 적용된다
- 생성자들도 method name으로 호출 가능하다
  - this();
- 매개변수가 없는 생성자 = default (기본) 생성자
- public을 붙일 수도 안 붙일 수도 있다
- 접근 지정자를 정할 수 있다

<br>

<br>

## Overriding in Java

> In any object-oriented programming language, Overriding is a feature that allows a subclass or child class to provide a specific implementation of a method that is already provided by one of its super-classes or parent classes. When a method in a subclass has the same name, same parameters or signature and same return type(or sub-type) as a method in its super-class, then the method in the subclass is said to *override* the method in the super-class.

<br>

- 부모로부터 물려 받은 기능을 다시 재정의 하는 것!
- method 선언부를 그대로 가져오면 됨!
- overriding에는 강제성이 없다!
  - 그래서 에러 안뜸.. 알아서 고쳐라~
  - <br>

![overriding in java](https://lh6.googleusercontent.com/i42VjCn-_E1fOx1xyW73cCB6vZI5ClO3yBporRbLONAslhZMBz9BBWCBysDcR2vgkoW5VdHsclYkzUo1-_6ig4FrlO1fbfGT5R0v3714e340RmjkyOZchdZqOkDp-_U4Rz_l9eLB)

<br>

**![img](https://lh6.googleusercontent.com/cATWBSmNqpRxlCjGU_ixiGLNwIvBbha-_mb0WW-9m6PUIKYs5mfdqUsuZlH8uJKaIrBjBNpd6e7FKAu3W8cGAjXooOW73DwWYVN67WxXe-do0aoKrVCpkXIxixRSeiYkjM9WvSM6)**

- 상속에 대해 언급하지 않으면 java.lang.object를 자동으로 상속받는 것을 알 수 있음!
- Class Animal extends **Object** 다!
- `Object` = 모든 객체가 사용 가능한 method
  - 그 어떤 객체도 최상단에는 Object!

<br>

### Is a

- 모든 객체의 Data Type은 부모가 될 수 있다!!
  - 모든 객체의 Data Type은 Object다!
    - why? Java의 모든 객체의 메모리의 최 상단부에는 Object가 있기 때문!  

<br>

ex1)

```java
Animal a = new Animal();
Object
```

- Animal의 부모 객체는 Object이기 때문에 객체 선언 시 data type으로 Object도 쓸 수 있다! 
- 하지만 Object type이면, Animal 안에 있는 data는 접근 할 수 없고, access 할 수 있는 type이 최상단부 만 가능!!

<br>

 ex2)

```java
Animal d = new Dog();
Dog 
    Object
```

- Dog의 부모 객체로 Animal 이 있기 때문에 객체 선언 시 Animal, Object 할 수 있다!
  - Animal로 선언시, Dog은 접근 불가, Animal 이상(Animal + Object) 접근 가능

- Java에 있는 모든 객체는 Object type이 될 수 있지만, access 할 수 있는 정보가 제한적임!

- Type casting을 통해서 부모 객체에 접근 가능하다!

  => 객체에서의 캐스팅 -> Up casting

  Ex) ((Animal)d).kind;

  ​ => 원래 Dog인 것Dog를 Animal로 up casting하면 한번에 Animal로 접근 가능

<br>

![img](https://lh4.googleusercontent.com/VmrL993swpj5LtVtY29bTA1VVKoKnle6KNYuGfUUTtjlpxIUSWVUyevCkv5u53F2C9TzuD35JKflEneZKjjBdFlXtHVLUoT-lHJNBOLmgp6f08vxjCfT9SoMYN53Jr-clXQFqMlZ) <br><br>
![img](https://lh4.googleusercontent.com/khSU0qSc8P28hUS4iJogUIISKPCj7niL8JNQDzkOcbJG9omJj-jvBKvKUfjfSNQCK8A982-KFHxTO9dxJWRoQJlBknWSBTlFwr73o73mt0_0xAjEHdzBXXQ3sI4YiKAIVN7Nk2Q2) <br>

<br>

### Annotations

: a tag that represents the metadata i.e. attached with class, interface, methods or fields to indicate some additional information which can be used by java compiler and JVM.

-> ex) `@Override`

<br>

### Polymorphism (다형성)

- the ability of an object to take on many forms  
  - overriding 기술을 접목하여 method는 하나인데 다양한 type의 객체를 받을 수 있음!

<br>
