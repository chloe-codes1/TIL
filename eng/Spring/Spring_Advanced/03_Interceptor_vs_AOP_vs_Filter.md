# Interceptor vs AOP vs Filter

<br>

## Interceptor

- A technology provided by Spring
- Provides functionality to reference or manipulate requests and responses before and after the `Dispatcher Servlet` `calls` the `controller`
- Operates in the `Spring Context`

## Interceptor vs AOP

- Instead of using an Interceptor, additional functionality to be applied to Controllers can be made as advice using `AOP` (Aspect Oriented Programming)
- However, for the following reasons, it is better to use Interceptors for `additional functionality` applied to the `controller invocation process`
    1. Since Spring controllers have different types and execution methods, writing `Pointcuts` (selecting methods to apply) is difficult
    2. Spring Controllers have inconsistent parameters and return values

## Filter

- Provides functionality to process `additional tasks` for all requests matching a URL pattern before/after the request reaches the `Dispatcher Servlet`
- Since the Dispatcher Servlet is the front controller at the very front of Spring, Filters are processed `outside the scope of Spring`
  - Filters operate in the `Web context`
