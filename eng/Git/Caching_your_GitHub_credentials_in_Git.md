# Caching your GitHub credentials in Git

> A short article for someone like me who finds it annoying to enter Git username and password
>
> Reference: [github docs](https://docs.github.com/en/github/using-git/caching-your-github-credentials-in-git)

<br>

### 1. Turn on credential helper

```bash
$ git config --global credential.helper cache
```

- **credential helper** stores the entered `password`.
- By default, it's stored for **15 minutes**, but if you want to change it, you can change the storage time with the command below

<br>

### 2. Change the default password cache timeout

```bash
 $ git config --global credential.helper 'cache --timeout 3600'
```

- An hour - 3600
- 1 day - 86,400
- 7 days - 604,800
- 30 days - 2,592,000 
