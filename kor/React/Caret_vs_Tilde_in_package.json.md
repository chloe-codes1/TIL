# Caret vs Tilde in package.json

> 궁금했던 내용을 정리해요
>
> Reference: [blog.outsider.ne.kr](https://blog.outsider.ne.kr/1041)

<br>

<br>

### tilde (~)

: ***Approximately equivalent to version***

- 현재 지정한 version의 마지막 자리 내의 범위에서만 자동으로 update 한다
- `npm install MODULE_NAME --save` 또는 `npm install MODULE_NAME --save-dev` 를 사용하면 자동으로 **package.json** 에 의존성을 추가할 수 있는데 그때 기본값으로 사용하는 방법이 tilde(`~`) 방식이다
- ex)
  - `~0.0.1` : `>=0.0.1 <0.1.0`
  - `~0.1.1` : `>=0.1.1 <0.2.0`
  - `~0.1` : `>=0.1.0 <0.2.0`
  - `~0` : `>=0.0 <1.0`
- 다양한 방식으로 version을 명시했을 때 위와 같은 범위 내에서 자동으로 update한다

<br>

<br>

### caret (^)

: ***Compatible with version***

- Caret을 설명하기 위해서는 먼저 **Semantic Versioning (SemVer)** 을 알아야 한다

  - Node.js를 비릇한 npm module은 모두 `SemVer` 를 따르고 있다

- #### npm version의 의미

      ```
      {MAJOR}.{MINOR}.{PATCH}
      ```

      - MAJOR: 하위 호환성이 보장되지 않는 변경사항이 발생할 때
      - MINOR: 하위 호환성을 보장하면서 기능을 추가할 때
      - PATCH: 하위 호환성을 보장하면서 버그를 수정할 때

- Caret(`^`)은 Node.js module이 `SemVer` 를 따른다는 것을 신뢰한다는 가정하에 동작한다

  - 그래서 MINOR나 PATCH version은 **하위 호환성**이 보장되어야 하므로 update를 한다
    - ex)
      - `^1.0.2` : `>=1.0.2 <2.0`
      - `^1.0` : `>=1.0.0 <2.0`
      - `^1` : `>=1.0.0 <2.0`
  - Tilde와 비교해보면 차이점은 명확한데 `1.x.x` 내에서는 하위 호환성이 보장되므로 그 내에서는 모두 update 하겠다는 의미이다

<br>

<br>

#### Wrap-up

- `~version`
  - ***Approximately equivalent to version***
  - MINOR version의 증가 없이, 미래의 PATCH를 update 한다
  - ex)
    - `~1.2.3`: will use releases from `1.2.3`  to  `<1.3.0`
- `^version`
  - ***Compatible with version***
  - MAJOR version의 증가 없니, 미래의 MINOR/PATCH를 update 한다
  - ex)
    - `^2.3.4`: will use releases from `2.3.4` to `<3.0.0`
