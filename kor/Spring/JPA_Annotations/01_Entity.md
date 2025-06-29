# @Entity

- 실제 DB Table과 매칭될 Class
  - Entity Class 라고도 한다
- 기본 값으로 로 Class의 `Camel Case` 네이밍을 `Underscore(_)` 네이밍으로 table 이름 매칭한다
  - ex)
    - SalesManager.java → sales_mana
- Entity Class에서는 Setter method를 만들지 않는다
  - why?
    - 해당 Class의 인스턴스 값들이 언제 어디서 변해야 하는지 코드상으로 명확히 구분할 수 없기 때문
  - 필드 값 변경이 필요하다면, 명확한 목적과 의도를 드러내는 method를 추가해야 한다
    - ex) 주문 상태인 status를 set 하는 함수 → setStatus (x), cancelOrder(o)
- Entity Class는 기본적으로 `생성자` 를 통해 값을 채우고 DB에 INSERT 한다
  - 값 변경이 필요한 경우에는, 해당 event에 맞는 public method를 호출하여 변경한다
- 생성자 대신 `Builder` 를 이용하여 어느 field에 어느 값을 넣어야 하는지 더 명확하게 할 수 있다
  - ex)
    - 아래 코드에서는 Example(a,b)와 Example(b, a)의 결과가 다를 것이다

      ```java
      public Example(String a,String b) {
        this.a=a; this.b=b;
      }
      ```

    - `Builder` 를 사용하면 순서가 상관없게 된다
