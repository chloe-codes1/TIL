# Final Keyword
>
> final keyword를 붙이면 무언가를 제한한다는 의미를 가지는 것이 공통적 성격이다
>

<br>

### Final Class

- 다른 클래스에서 `상속`하지 못한다
- String class도 final 이다!
  - String class를 상속하려고 하면 오류가 난다

<br>

### Final Method

- 다른 method에서 `overriding` 하지 못한다
  - 더 이상 method를 변형시킬 수 없다
- sub class로 확장하면서 더 이상 method 형태를 변형시키지 않게 한다
  - 자식 class에서 재정의 할 수 없는 method로, 자식 class가 부모 class의 method 동작을 변경하지 못하도록 방지할 수 있다
  - 이를 통해 프로그램의 일관성을 유지하고 버그를 방지할 수 있다!

<br>

### Final Variable

- 변하지 않는 `상수값`이 되어 새로 할당할 수 없는 변수가 된다
- 수정될 수 없기 때문에 초기화 값은 필수적이다
  - but, 객체 안의 변수라면, `생성자` , `static block` 을 통한 초기화 까지는 허용한다
- 수정할 수 없다는 값의 범위는 그 `변수의 값` 에 한정한다
  - 즉 다른 객체를 참조할 때, 참조하는 객체의 내부의 값은 변경할 수 있다
- `public static final`
  - 인스턴스가 필요 없는 class 상수이다
  - class가 memory에 load 되면 사용할 수 있다
    - `class.상수` 의 방식으로 사용한다
  - 마찬가지로 선언과 동시에 초기화를 해야한다
