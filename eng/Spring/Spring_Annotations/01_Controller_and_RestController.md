# @Controller and @RestController

<br>

## @Controller

### 1. Returning Views with Controller

- Traditional Spring MVC controller
- Mainly used to return Views
  - Returns a ViewName!
- A `ViewResolver` is used to render a View from the ViewName returned by the Controller
  - Finds and renders a View according to the ViewResolver configuration

<br>

### 2. Returning Data with Controller

- When data needs to be returned instead of a View, the `@ResponseBody` annotation must be used for data return
  - The `@ResponseBody` annotation allows a Controller to return data in JSON format!
  - The returned object is serialized to JSON and returned to the user
- When returning objects through a Controller, they are generally wrapped in `ResponseEntity`
  - To return objects, `HttpMessageConverter` operates instead of `ViewResolver`
  - `HttpMessageConverter` has several Converters registered, and the Converter used varies depending on the data to be returned
    - For strings: `StringHttpMessageConverter`
    - For objects: `MappingJackson2HttpMessageConverter`
- Spring combines the client's `Http Accept header` and the server's Controller return type information to select the appropriate `HttpMessageConverter` to process it

<br>

## @RestController

- Restful web service controller
- `@Controller` with `@ResponseBody` added
  - An HTTP Response Body is generated
  - The behavior is exactly the same as attaching `@ResponseBody` to `@Controller`!
  - Allows using `@ResponseBody`, which was previously declared on each method, all at once
- The main purpose is to return object data in `JSON format`!
- Mainly used when developing REST APIs, and objects are wrapped in `ResponseEntity` for return
