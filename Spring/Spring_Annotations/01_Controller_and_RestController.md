# @Controller and @RestController

<br>

## @Controller

### 1. Controller로 View return 하기

- 전통적인 Spring MVC controller
- 주로 View 를 반환하기 위해 사용
  - ViewName을 반환한다!
- Controller가 반환한 ViewName 으로부터 View를 rendering 하기 위해서 `ViewResolver` 가 사용된다
  - ViewResolver 설정에 맞게 View 를 찾아 rendering 한다

<br>

### 2. Controller로 Data return 하기

- View가 아닌, Data를 return 해야 하는 경우, Data 반환을 위해 `@ResponseBody` annotation을 사용해야 한다
  - `@ResponseBody` annotation을 통해 Controller도 JSON 형태로 Data를 return 할 수 있다!
  - Return 되는 객체는 JSON으로 Serialize 되어 사용자에게 반환된다
- Controller를 통해 객체를 반환할 때에는 일반적으로 `ResponseEntity` 로 감싸서 반환한다
  - 객체를 반환하기 위해서는 `ViewResolver` 대신에 `HttpMessageConverter` 가 동작한다
  - `HttpMessageConverter` 에는 여러 Converter가 등록되어 있고, Return 해야하는 data에 따라 사용되는 Converter가 달라진다
    - 문자열의 경우 `StringHttpMessageConverter`
    - 객체의 경우 `MappingJackson2HttpMessageConverter`
- 스프링은 Client의 `Http Accept header` 와 Server의 Controller return type 정보를 조합해 적합한 `HttpMessageConverter` 를 선택하여 이를 처리한다

<br>

## @RestController

- Restful web service controller
- `@Controller` 에 `@ResponseBody` 가 추가된 것
  - HTTP Response Body 가 생성된다
  - 동작 방식 역시 `@Controller` 에 `@ResponseBody` 를 붙인 것과 완벽히 동일하다!
  - method 마다 `@ResponseBody` 선언했던 것을 한번에 사용할 수 있게 한다
- 주 용도는 `JSON 형태`로 객체 data를 반환하는 것!
- REST API를 개발할 때 주로 사용하며, 객체를 `ResponseEntity` 로 감싸서 반환한다
