# @RequestParam

> Reference: [Spring Docs - RequestParam](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html)
>

<br>

### What is @RequestParam?

- An annotation that retrieves parameters passed from external sources to an API
- Used to bind HTTP request parameters to method parameters
- Mainly used when receiving parameter values from client requests as Controller method parameters for processing
- ex)

  ```java
  @RequestParam("name") String name
  ```

  Stores the parameter passed externally with the name "name" into the method parameter name (String name)

<br>

### Using @RequestParam

- Spring MVC
  - Maps to query parameters, form data, and parts of multipart requests
  - This occurs because the Servlet API combines query parameters and form data into a single map called `parameters`, which includes automatic parsing of the request body
- Spring WebFlux
  - Maps only to query parameters
  - To handle all three types -- query parameters, form data, and multipart -- you can use data binding to a command object annotated with `ModelAttribute`
- Things to know
  - If the method parameter type is Map and a request parameter name is specified, the request parameter value is converted to a Map when an appropriate conversion strategy exists
  - If the method parameter is **`Map<String, String>`** or **`MultiValueMap<String, String>`** and no parameter name is specified, the map parameter is populated with all request parameter names and values

<br>

### Attributes of @RequestParam

- **`name`**
  - Specifies the name of the request parameter
- **`required`**
  - Specifies whether the request parameter is required
  - Default value is **`true`**
  - If **`required=true`** and the parameter is not present in the request, an exception is thrown
- **`defaultValue`**
  - Specifies the default value to use when the request parameter is not provided
- **`value`**
  - Alias for name()
