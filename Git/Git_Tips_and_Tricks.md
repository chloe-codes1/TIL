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

### (5) 로컬 저장소로 코드 불러오기 `git pull`

- Github 원격 저장소에 있은 코드를 불러오고 각 `branch`에 해당되는 `commit`들을 적용한다.

```bash
$ git pull

$ git pull [원격 저장소 이름] (specify a remote to pull from)
```

<br>

### (5) 원격 저장소로 코드 `git push`

- 최종적으로 Github 원격 저장소에 push 한다.

```bash
$ git push

$ git push origin master
```

#### Tip

: 만약 현재 branch가 push 하려는 repo의 branch 이면 `$ git push` 명령어만 입력해도 된다!

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

- Undo `git add` before commit

```bash
$ git reset
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



<br>

<br>

## 4. 특정 시점으로 돌아가기

<br>

> 특정 commit을 기준으로 돌아가기

```bash
$ git checkout f008d8f
```

<br>

> test branch 만들면서 이동하기

```bash
$ git checkout -b test
$ git log --oneline
f008d8f (HEAD -> test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> reference log 확인

```bash
$ git reflog
```

<br>

> 어디에 head 있는지 확인

```bash
$ git log --oneline
fc58709 (HEAD -> master, origin/master, origin/HEAD) README.md 추가
fd2e992 06 | Article C with ModelForm
f008d8f (test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> 다시 test branch로 돌아가기

```bash
$ git checkout test
Switched to branch 'test'
```

<br>

<br>

## 5. 원격 저장소에 올라간 커밋 되돌리기

<br>

### 방법 1) Local에서 commit 되돌린 후 강제 Push 하기

> `$ git reset` 으로 commit 되돌리기

```bash
$ git reset --hard HEAD       (going back to HEAD)

$ git reset --hard HEAD^      (going back to the commit before HEAD)

$ git reset --hard HEAD~2     (going back two commits before HEAD)
$ git reset --hard HEAD^^    (another syntax for going back two commits)
```

<br>

> `-f`  or  `--force` 명령어로 강제로 Push 하기

```bash
$ git push -f origin master

$ git push --force origin master
```

<br>

<br>

### 방법 2) `git revert` 사용하기

- 방법 1은 원격 저장소 commit history를 강제로 조작한다는 문제점이 있음
- but, `git revert`를 사용하면 commit을 되돌리는 작업도 하나의 commit으로 간주하여 commit history에 추가하게 됨

<br>

>특정 commit에서의 변경 사항을 제거하는 또 다른 commit 생성하기

```bash
$ git revert --no-commit [되돌리고 싶은 commit의 hash]     

$ git revert --no-commmit [되돌리고 싶은 커밋의 범위]

$ git revert --no-commit Head~3
```

<br>

<br>



`+`

- `master` branch에 있는 내용은 자동으로 배포가 됨
  - `master`는 배포 가능한 상태

<br>

### 특정  branch 만 clone 하기

```bash
$ git clone -b {branch_name} --single-branch {저장소 URL}
```

<br>

### 원격 저장소의 특정 branch 가져오기

> 우선 원격 저장소에 어떤 branch 있는지 확인

```bash
$ git branch -r
```

<br>

> 원격저장소 + 로컬 branch 확인

```bash
$ git branch -a
```

<br>

#### 원격 저장소의 branch를 **동일한 이름으로** 가져오기

```bash
$ git checkout -t [origin/가져올 원격 저장소 branch 이름]
```

<br>

#### 원격 저장소의 branch를 이름을 변경하여 가져오기

``` bash
$ git checkout -b [생성할 branch 이름][가져올 원격 저장소 branch 이름]
```

<br>

<br>

### `git fetch`

> remote branch 가 어디까지 가있는지 확인 가능

- git pull == git fetch && merge

<br>

### `git rebase`

> 재 배치하기

- 뒤에 `-i` 를 붙이면 interactive 하게 (대화형으로) 실행 가능

<br>

<br>

## 6. Submodule 사용하기

<br>

### Submodule 이란?

- Git main repo 안에 다른 sub repo가 있는 것
  - main repo에서는 sub repo를 관리하지 않는다!

- **Submodule**을 사용하면 프로젝트 간에 공통으로 사용되는 logic을 공유 할 수 있다!

<br>

### Add Submodule 

```bash
$ git submoduel add [repo 주소]
```

- 이후에 따로 `git add` 없이 commit 할 수 있음

<br>

### Update Submodule

#### Update main repo

```,
$ git pull
```

- main repo root에서 다음 명령어를 실행하면 main repo 가 update 됨

<br>

#### Update sub repo

```bash
$ git submodule update --remote --merge
```

- main repo의 root에서 위의 명령어를 실행하면 update된 main repo와 sub repo의 관계에 따라 sub repo를 업데이트 해야한다