# Caret vs Tilde in package.json

> Organizing content I was curious about
>
> Reference: [blog.outsider.ne.kr](https://blog.outsider.ne.kr/1041)

<br>

<br>

### tilde (~)

: ***Approximately equivalent to version***

- Automatically updates only within the range of the last digit of the currently specified version
- When you use `npm install MODULE_NAME --save` or `npm install MODULE_NAME --save-dev` to automatically add dependencies to **package.json**, the default method used is the tilde(`~`) approach
- ex)
  - `~0.0.1` : `>=0.0.1 <0.1.0`
  - `~0.1.1` : `>=0.1.1 <0.2.0`
  - `~0.1` : `>=0.1.0 <0.2.0`
  - `~0` : `>=0.0 <1.0`
- When the version is specified in various ways, it automatically updates within the ranges shown above

<br>

<br>

### caret (^)

: ***Compatible with version***

- To explain Caret, you first need to know about **Semantic Versioning (SemVer)**

  - Node.js and all npm modules follow `SemVer`

- #### Meaning of npm version

      ```
      {MAJOR}.{MINOR}.{PATCH}
      ```

      - MAJOR: When there are changes that break backward compatibility
      - MINOR: When adding functionality while maintaining backward compatibility
      - PATCH: When fixing bugs while maintaining backward compatibility

- Caret(`^`) operates under the assumption that the Node.js module follows `SemVer`

  - Therefore, MINOR or PATCH versions should maintain **backward compatibility**, so they are updated
    - ex)
      - `^1.0.2` : `>=1.0.2 <2.0`
      - `^1.0` : `>=1.0.0 <2.0`
      - `^1` : `>=1.0.0 <2.0`
  - Comparing with Tilde, the difference is clear: since backward compatibility is guaranteed within `1.x.x`, it means it will update everything within that range

<br>

<br>

#### Wrap-up

- `~version`
  - ***Approximately equivalent to version***
  - Updates future PATCHes without increasing the MINOR version
  - ex)
    - `~1.2.3`: will use releases from `1.2.3`  to  `<1.3.0`
- `^version`
  - ***Compatible with version***
  - Updates future MINOR/PATCHes without increasing the MAJOR version
  - ex)
    - `^2.3.4`: will use releases from `2.3.4` to `<3.0.0`
