# @RequestParam

> Reference: [Spring Docs - RequestParam](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html)
>

<br>

### @RequestParam 이란?

- 외부에서 API로 넘긴 parameter를 가져오는 annotation
- HTTP 요청의 parameter를 method parameter로 binding 하는데 사용된다
- 주로 client가 전달한 요청의 parameter 값을 Controller method의 parameter로 받아와서 처리할 때 사용한다
- ex)

  ```java
  @RequestParam("name") String name
  ```

  외부에서 name이란 이름으로 넘긴 parameter를 method parameter name (String name) 에 저장한다

<br>

### @RequestParam 사용하기

- Spring MVC
  - query parameter, form data, multipart 요청의 parts와 매핑된다
  - 이는 Servlet API가 query parameter와 form data를 `parameters` 라는 하나의 map으로 결합하기 때문에 발생하며, 이것은 request body의 자동 파싱을 포함한다
- Spring WebFlux
  - query parameter만을 매핑한다
  - query parameter, form data, multipart 3개의 타입을 다루려면 `ModelAttribute` 로 annotate 된 명령 객체 (command object)에 data binding을 사용할 수 있따
- 알아두기
  - method parameter type이 Map이고 request parameter 이름이 지정된 경우, 적절한 변환 전략이 있을 때 request parameter 값이 Map으로 변환된다
  - 만약 method parameter가 **`Map<String, String>`** or **`MultiValueMap<String, String>`** 이고 parameter 이름이 지정되지 않은 경우, map parameter는 모든 request parameter 이름과 값으로 채워진다

<br>

### @RequestParam 의 속성

- **`name`**
  - 요청 파라미터의 이름을 지정한다
- **`required`**
  - 요청 파라미터가 필수인지 여부를 지정한다
  - 기본값은 **`true`**
  - 만약 **`required=true`** 이고 해당 parameter가 요청에 없는 경우 예외가 발생한다
- **`defaultValue`**
  - 요청 parameter가 전달되지 않았을 때 사용할 기본값을 지정한다
- **`value`**
  - name() 의 alias
