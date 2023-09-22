# Git branch

<br>

<br>

## 1. branch 관련 명령어

> Git 브랜치를 위해 root-commit을 발생시키고 진행하세요.

1. 브랜치 생성

    ```bash
    (master) $ git branch {브랜치명}
    ```

2. 브랜치 이동

    ```bash
    (master) $ git checkout {브랜치명}
    ```

3. 브랜치 생성 및 이동

    ```bash
    (master) $ git checkout -b {브랜치명}
    ```

4. 브랜치 삭제

    ```bash
    (master) $ git branch -d {브랜치명}
    ```

5. 브랜치 목록

    ```bash
    (master) $ git branch
    ```

6. 브랜치 병합

    ```bash
    (master) $ git merge {브랜치명}
    ```

 * master 브랜치에서 {브랜치명}을 병합

<br>

<br>

## 2. branch 병합 시나리오

> branch 관련된 명령어는 간단하다.
>
> 다양한 시나리오 속에서 어떤 상황인지 파악하고 자유롭게 활용할 수 있어야 한다.

<br>

### 상황 1. fast-foward

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

1. feature/crud branch 생성 및 이동

   ```bash
   git branch feature/crud
   git checkout feature/crud
   ```

   * 혹은

   ```bash
   git checkout -b feature/crud
   ```

2. 작업 완료 후 commit

   * 임의의 파일을 만들고, commit
   * `add` , `commit`

3. master 이동

   ```bash
   (feature/crud) $ git checkout master
   Switched to branch 'master'
   (master) $
   ```

4. master에 병합

   ```bash
   $ git merge feature/crud
   Updating d66ff92..f219c8c
   # Fast-forward!!!
   Fast-forward
    crud.html | 0
    urls.py   | 1 +
    views.py  | 1 +
    3 files changed, 2 insertions(+)
    create mode 100644 crud.html
    create mode 100644 urls.py
    create mode 100644 views.py
   
   ```

5. 결과 -> fast-foward

   ```bash
   $ git log --oneline
   f219c8c (HEAD -> master, feature/crud) Complete CRUD)
   d66ff92 Init
   ```

6. branch 삭제

   ```bash
   git branch -d feature/crud
   ```

---

### 상황 2. merge commit

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **다른 파일이 수정**되어 있는 상황
>
> git이 auto merging을 진행하고, **commit이 발생된다.**

1. feature/signout branch 생성 및 이동

   ```bash
   (master)
   $ git checkout -b feature/signout
   Switched to a new branch 'feature/signout'
   (feature/signout) $
   ```

2. 작업 완료 후 commit

   ```bash
   touch signout.txt
   git add .
   git commit -m 'Complete'
   ```

3. master 이동

   ```bash
   (feature/signout)
   $ git checkout master
   Switched to branch 'master'
   (master) $
   ```

4. *master에 추가 commit 이 발생시키기!!*

   * **다른 파일을 수정 혹은 생성하세요!**

5. master에 병합

   ```bash
   $ git merge feature/signout
   Merge made by the 'recursive' strategy.
    signout.txt | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 signout.txt
   ```

6. 결과 -> 자동으로 *merge commit 발생*

7. 그래프 확인하기

   ```bash
   $ git log --oneline --graph
   *   2125d5b (HEAD -> master) Merge branch 'feature/signout'
   |\
   | * fb74094 (feature/signout) Complete signout
   * | 75f0abd README @ master
   |/
   * f219c8c Complete CRUD)
   * d66ff92 Init
   ```

   ```bash
   $ git log -1 --oneline
   2125d5b (HEAD -> master) Merge branch 'feature/signout'
   ```

8. branch 삭제

   ```bash
   $ git branch -d feature/signout
   Deleted branch feature/signout (was fb74094).
   ```

<br>

<br>

<hr>

### 상황 3. merge commit 충돌

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **같은 파일의 동일한 부분이 수정**되어 있는 상황
>
> git이 auto merging을 하지 못하고, 충돌 메시지가 뜬다.
>
> 해당 파일의 위치에 표준형식에 따라 표시 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 직접 commit을 발생 시켜야 한다.

<br>

1. feature/signup branch 생성 및 이동

   ```bash
   (master)
   $ git checkout -b feature/signup
   Switched to a new branch 'feature/signup'
   ```

2. 작업 완료 후 commit

   * `add`, `commit`

3. master 이동

   ```bash
   (feature/signup)
   $ git checkout master
   Switched to branch 'master'
   ```

4. *master에 추가 commit 이 발생시키기!!*

   * **동일 파일을 수정 혹은 생성하세요!**

```bash
   $ git log --oneline
   3c81134 (HEAD -> master) Hotfix signout urls.py
   2125d5b Merge branch 'feature/signout'
   75f0abd README @ master
   fb74094 Complete signout
   f219c8c Complete CRUD)
   d66ff92 Init
```

5. master에 병합

   ```bash
   (master)
   $ git merge feature/signup
   Auto-merging urls.py
   CONFLICT (content): Merge conflict in urls.py
   Automatic merge failed; fix conflicts and then commit the result.
   
   (master|MERGING)
   ```

6. 결과 -> *merge conflict발생*

   > git status 명령어로 충돌 파일을 확인할 수 있음.

   ```bash
   (master|MERGING)
   $ git status
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")
     (use "git merge --abort" to abort the merge)
   
   Changes to be committed:
           new file:   signup.txt
   
   Unmerged paths:
     (use "git add <file>..." to mark resolution)
           both modified:   urls.py
   ```

7. 충돌 확인 및 해결

   ```
   <<<<<<< HEAD
   # signout
   =======
   # signup
   >>>>>>> feature/signup
   ```

8. merge commit 진행

    ```bash
    git commit
    ```

   * vim 편집기 화면이 나타납니다.

   * 자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:wq`를 입력하여 저장 및 종료를 합니다.
      * `w` : write
      * `q` : quit

   * 커밋이  확인 해봅시다.

9. 그래프 확인하기

   ```bash
   (master)
   $ git log --oneline --graph
   *   4e55ba7 (HEAD -> master) Merge branch 'feature/signup'
   |\
   | * fc7f0d8 (feature/signup) Complete signup
   * | 3c81134 Hotfix signout urls.py
   |/
   *   2125d5b Merge branch 'feature/signout'
   |\
   | * fb74094 Complete signout
   * | 75f0abd README @ master
   |/
   * f219c8c Complete CRUD)
   * d66ff92 Init
   
   ```

10. branch 삭제

    ```bash
    git branch -d feature/signup
    ```

    <br>
