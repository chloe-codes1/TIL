# Python Coding Convention

> PEP8이 궁금해져서 찾아보다가 급 정리
>
> References: [책] 파이썬 코딩의 기술

<br>

<br>

## PEP8 이란?

> Python Enhancement Proposal 8 (PEP8)

-  Python code를 어떻게 구성할지 알려주는 스타일 가이드
  - 코딩을 할 때 특정 형식으로 작성하자는 약속
    - 일관성 있는 스타일을 사용하면 **유지보수**가 더욱 쉬워지고 **가독성**도 높아진다!
-  [python.org](https://www.python.org/dev/peps/pep-0008/) 에 자세히 정리되어 있음!

<br>

<br>

## PEP8 중 반드시 따라하야 하는 몇 가지 규칙

<br>

### 1. Whitespace 

> Python에서 whitespace는 문법적으로 의미가 있음
>
> 파이썬 프로그래머는 특히 코드의 명료성 때문에 whitespace의 영향에 민감하다!

- Tab이 아닌 **Space**로 들여쓴다
- 문법적으로 의미 있는 들여쓰기는 각 수준마다 **space 4개**를 사용한다
- 한 줄의 문자 길이가 **79자** 이하여야 한다
- 표현식이 길어서 다음 줄로 이어지면 일반적인 들여쓰기 수준에 **추가로 Space 4개**를 사용한다
- 파일에서 `함수`와 `class`는 **빈 줄 두 개**로 구분해야 한다

- Class에서 method는 빈 줄 하나로 구분해야 한다
- `List index`, `함수 호출`, `keyword 인수 할당` 에는 **space를 사용하지 않는다**

<br>

### 2. Naming Conventions

> PEP 8 은 언어의 부분별로 독자적인 명명 규칙을 제안한다
>
> 코드를 읽을 때 각 이름에 대응하는 타입을 구별하기 쉽게 해준다!

- `함수`, `변수`, `속성`은 **lowercase_unserscore** 형식을 따른다
- `protected` instance 속성은 **_leading_underscore** 형식을 따른다
- `private` instance 속성은 **__double_leading_underscore** 형식을 따른다
- Class와 Exception은 **CaplitalizeWord** 형식을 따른다
- Module 수준의 tkdtnsms **ALL_CAPS** 형식을 따른다
- `Class instance`의 method에서 첫 번째 parameter (해당 객체를 참조) 의 이름을 **self**로 지정한다
- `Class method`에서는 첫 번째 parameter (해당 class를 참조)의 이름을 **cls** 로 지정한다

<br>

### 3. 표현식과 문장

> 파이썬의 계명 (The Zen of Python)에는 "어떤 일을 하는 확실한 방법이 (될 수 있으면 하나만) 있어야 한다" 는 표현이 있다
>
> PEP 8은 표현식과 문장의 본보기로 이 스타일을 정리하고 있다

- 긍정 표현식의 부정 ( `if not a is b` ) 대신에 인라인 부정 ( `if a is not b` ) 을 사용한다
- 길이를 확인 ( `if len(somelist) == 0` ) 하여 빈 값( `[]` or `''` ) 을 확인하지 않는다
  - `if not somelist` 를 사용하고, 빈 값은 암시적으로 **False**가 된다고 가정한다
  - 비어있지 않은 값에도 같은 방식이 적용된다! 
    - 비어있지 않은 값은 `if somelist`  문이 암시적으로 **True** 가 된다
- 한 줄로 된 `if 문`, `for와 while loop`, `except 복합문` 을 쓰지 않는다
  - 이런 문장은 여러 줄로 나누어서 명료하게 작성하기!
- 항상 파일의 맨 위에 import문을 놓는다
- **module을 import** 할 때는 항상 module의 절대 이름을 사용하며 현재 모듈의 경로를 기준으로 상대 경로로 된 이름을 사용하지 않는다
  - ex) `import foo` 가 아니라 `from bar import foo` 로 사용하기!
- 상대적인 import를 해야 한다면 명시적인 구문을 써서 `from . import foo` 라고 한다
- import는 `표준 라이브러리 모듈`, `third party 모듈`, `자신이 만든 모듈` 순으로 구분해야 한다
  - 각각의 하위 section에서는 alphabetic order로 import 한다



<br>

<br>

## PEP8을 잘 따르고 있는지 확인하는 방법

> pylint와 PEP8 설치하여 사용하기!

<br>

### 1. pylint

```bash
$ pip install pylint
```

<br>

### 2. PEP8

```bash
$ pip install pep8
```



