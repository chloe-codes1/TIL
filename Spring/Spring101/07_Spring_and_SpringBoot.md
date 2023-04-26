# Spring and SpringBoot

### Spring Framework 사용 이유

> Spring의 핵심 컨셉

- 스프링은 자바 언어 기반의 프레임워크다
- 자바 언어의 가장 큰 특징 → `객체 지향 언어`
- 스프링은 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크
- 스프링은 `좋은 객체 지향 어플리케이션` 을 개발할 수 있게 도와주는 프레임워크다!

<br/>

### SpringBoot와 Spring의 차이
>
> 왜 Boot를 쓸까?

스프링부트는 스프링을 편리하게 사용할 수 있도록 지원
(최근에는 기본으로 사용)

- 손쉬운 `의존성` 관리 → `starter`
  - 손쉬운 빌드 구성을 위한 `starter` dependency 제공
- `Auto Configuration`
  - 개발에 필요한 모든 내부 `dependency` 를 관리한다
- `내장 WAS`
  - `Tomcat` 같은 WAS를 내장해서 별도의 WAS를 설치하지 않아도 됨
- 스프링과 3rd parth (외부) 라이브러리 자동 구성
  - 외부 라이브러리 사용 시, 스프링부트가 버전까지 지정을 알아서 해줌
- metric, 상태 확인 외부 구성 같은 프로덕션 준비 기능 제공
