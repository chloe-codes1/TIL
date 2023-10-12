# @Column

- Table의 column
- 따로 선언하지 않아도 `@Entity` annotation 이 붙은 Class의 field는 모두 Column 이 된다
- 사용하는 이유
  - default 외에 추가로 변경이 필요한 Option이 있을 경우에 해당 annotation을 사용한다
    - 문자열 default 값은 VARCHAR(255) 인데, size를 늘리고 싶을 때 사용하면 된다
- Options
  - `columndefinition`
    - VARCHAR: 1 ~ 255개의 문자
    - TEXT: 최대 2^16
    - MEDIUMTEXT: 최대 2^24
    - LONGTEXT: 최대 2^32
