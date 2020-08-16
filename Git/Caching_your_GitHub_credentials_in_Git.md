# Caching your GitHub credentials in Git

> Git  username과 password를 입력하기 귀찮은 나 같은 누군가를 위한 짧은 글
>
> Reference: [github docs](https://docs.github.com/en/github/using-git/caching-your-github-credentials-in-git)

<br>

### 1. Turn on credential helper

```bash
$ git config --global credential.helper cache
```

- **credential helper**가 입력한 `password`를 저장해놓는다.
- default로 **15분**동안 저장되지만, 변경을 원하면 아래의 명령으로 저장되는 시간을 바꾸면 된다

<br>

### 2. Change the default password cache timeout

```bash
 $ git config --global credential.helper 'cache --timeout 3600'
```

- An hour - 3600
- 1 day - 86,400
- 7 days - 604,800
- 30 days - 2,592,000