# @Qualifier

> Reference: [Spring Docs - @Qualifier](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Qualifier.html)
>

## @Qualifier 란?

Spring Framework에서 bean을 주입할 때 어떤 bean을 선택할지 명시적으로 지정하기 위해 사용한다

## Problem

- Autowire Need for Disambigution
  - `@Autowired` annotation 으로 의존성을 주입할 수 있지만, 몇가지 주의할 점이 있다
  - 만약 같은 type을 가진 한개 이상의 bean이 container에 존재한다면, 스프링은 `NoUniqueBeanDefinitionException` 을 발생시킬 것이다

## Solution

@Qualifier annotation을 사용하여 autowire 하고자 하는 대상을 특정할 수 있다

## @Qualifier 사용 시 주의할 점

@Qualifier 에 지정한 한정자 값을 갖는 bean 객체가 존재하지 않으면 `NoSuchBeanDefinitionException`이 발생한다
