# Git Tips & Tricks

> Git의 달인이 되자

<br>

<br>

## 1. Git Basics

<br>

### (1) Git으로 프로젝트 관리 시작 : `git init`

- 자신이 앞으로 학습한 내용을 기로한 `TIL` 폴더를 하나 생성한다. 이때 해당 폴더는 최상단에 생성한다
- `git bash` 에서 `TIL` 폴더로 이동한 이후에 아래의 명령어로 `git` 관리를 시작한다

```bash
$ git init
```

<br>

### (2) Commit을 위한 Staging : ` git add`

- 현재 코드 상태의 스냅샷을 찍기 위한 파일 선택 (== Staging Area에 파일 추가)

``` bash
$ git add [파일이름] # .은 모든 변경 사항을 staging area로 올림
```

<br>

### (3) 버전 관리를 위한 스냅샷 저장 : `git commit`

- 현재 상테에 대한 스냅샷을 `commit` 하여, 버전 관리를 진행한다.

``` bash
$ git commit -m "commit message"
```

<br>

### (4) 원격 저장소 정보 추가 : `git remote`

- Github 원격(remote) 저장소(repository)를 생성하고 `TIL` 폴더와 연결한다
- 새로운 원격 저장소가 추가될 때만 입력한다.

```bash
$ git remote add origin [github 원격 저장소 주소]
```

<br>

### (5) 원격 저장소로 코드 `git push`

- 최종적으로 Github 원격 저장소에 push 한다.

```bash
$ git push origin master
```

<br>

### (6) 그 외 명령어

- 현재 `git`의 상태를 조회 `git status`

````bash
$ git status
````

- 버전관리 이력을 조회

```bash
$ git log
```

- `git` 설정 (user.name & user.email) : **최초 1회 설정**

```bash
$ git config --global user.name "Chloe Kim"
$ git config --global user.email "juhyun.kim@lindsey.edu"
```



<br><br>

## 2. `README.md`

> 원격(remote) 저장소(repository)에 대한 정보를 기록하는 마크다운 문서. 일반적으로 해당 프로젝트를 사용하기 위한 방법 등을 기재한다.

<br>

### (1) `README.md` 파일 생성

- `README.md` 파일을 `TIL` 폴더 (최상단)에 생성한다. 이름은 반드시 **README.md**로 설정한다.

```bash
$ touch README.md
```

<br>

### (2) (자신만의)  원칙에 대한 간단한 내용 추가

- 마크다운 작성법 pdf에서 배우고 실습한 내용을 토대로 `README.md` 파일을 작성한다.
- 형식은 자유롭게 작성하되 마크다운 문법(의미론적)을 지켜서 작성한다.

<br>

### (3) 저장 후 버전관리 : `add`, `commit`, `push`

- 작성이 완료되면 아래의 명령어를 통해 commit 이력을 남기고 원격 저장소로 push 한다.

```bash
$ git add README.md
$ git commit -m "add README.md"
$ git push origin master
```

<br>

<br>

## 3. Shared Repository

<br>

> Fast forward merge 실습

```bash
# branch 확인
$ git branch

# 새 branch 만들기
$ git branch [branch 명]

# 다른 branch로 이동하기
$ git switch [이동하고자 하는 branch 명]

# 다른 branch 이동 ver2)
$ git checkout [이동하고자 하는 branch 명]


# branch 삭제하기
$ git branch -d [지우고자 하는 branch 명]

# FF(=Fast Forward) merge 하기
# : 주체가 되는 branch로 이동 후 진행 (ex. master로 이동 후 chloe 만들기)
$ git merge [병합할 branch 이름]

# 새 branch 만들면서 이동하기
$ git switch -c [새로 만들 branch]

# 새 branch 만들면서 이동 ver2)
$ git checkout -b ashley  # -b는 branch 뜻함


# git log graph로 보기
$ git log --oneline --graph


```



