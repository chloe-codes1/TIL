# @Qualifier

> Reference: [Spring Docs - @Qualifier](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Qualifier.html)
>

## What is @Qualifier?

Used to explicitly specify which bean to select when injecting beans in the Spring Framework

## Problem

- Autowire Need for Disambiguation
  - Dependencies can be injected with the `@Autowired` annotation, but there are a few things to be cautious about
  - If more than one bean of the same type exists in the container, Spring will throw a `NoUniqueBeanDefinitionException`

## Solution

The @Qualifier annotation can be used to specify the target to autowire

## Things to Note When Using @Qualifier

If a bean object with the qualifier value specified in @Qualifier does not exist, a `NoSuchBeanDefinitionException` is thrown
