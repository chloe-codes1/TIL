# Generic

<br>

- Generic은 Java에서 `안정성`을 맡고 있다고 할 수 있다
- 다양한 타입의 객체들을 다루는 `method`나 `collection class`에서 사용하는 것으로, compile 과정에서 `type check`를 해주는 기능이다
- 객체의 `type을 compile 시에 체크`하기 때문에 객체의 type 안전성을 높이고 `형변환`의 번거로움을 줄여준다
  - 자연스럽게 코드도 더 간결해진다
- ex)
  - `Collection 에 특정 객체만 추가될 수 있도록`, 또는 특정한 class의 특징을 갖고 있는 경우에만 추가될 수 있도록 하는 것이 Generic이다
    - 이로 인한 장점은 collection 내부에서 `들어온 값이 내가 원하는 값인지 확인하는 별도의 logic을 구현할 필요가 없어`진다
  - API 를 설계하는데 있어서 보다 `명확한 의사전달`이 가능해진다
