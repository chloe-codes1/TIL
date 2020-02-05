# 알고리즘 코드 공유를 위한 협업툴 실습

> **branch는 일회용이다!**
>
> **Git Visualizer :** https://git-school.github.io/visualizing-git/



## 1. 규칙

#### 1) 다른 폴더를 건드리지 않는다.

#### 2) master 에서 작업하지 않는다.

#### 3) 본인의 branch 에서 작업한다.

#### 4) 작업 이후 merge request를 보낸다.

#### 5) 권한이 있는 사람이 특정 시점에 merge를 한다.



## 2. 실습 (fast forward merge)

### 1) commands

```shell
$ git clone [주소]
$ git branch # 현재 브랜치 확인
$ git branch [브랜치명] # 브랜칭 생성
$ git switch [이동하고자 하는 브랜치명] # 브랜치로 이동
$ git switch -c [생성 및 이동하고자 하는 브랜치명] # 생성과 이동을 동시에
$ git checkout -b [생성 및 이동하고자 하는 브랜치명] # switch -c 와 동일
$ git merge [병합할 브랜치의 이름] # 합병 기준이 되는 브랜치에서 이동 후 명령어 실행
$ git branch -d [삭제하고자 하는 브랜치명] # 브랜치 삭제 (delete / destroy)
## 브랜치는 일회용이므로 merge 후에는 삭제하고, 필요에 따라 새로운 브랜치를 사용할 것
```

![image-20200205114805881](C:\Users\multicampus\codes\00_TIL\image\image-20200205114805881.png)

![image-20200205114843686](C:\Users\multicampus\codes\00_TIL\image\image-20200205114843686.png)

![image-20200205132036897](C:\Users\multicampus\codes\00_TIL\image\image-20200205132036897.png)

**새로운 브랜치를 만들기 전에는 master가 git log 의 제일 끝단에  와 있음을 반드시 확인할 것.**

![image-20200205131801838](C:\Users\multicampus\codes\00_TIL\image\image-20200205131801838.png)



### 2) practice

1. 새 폴더 생성 후 git init
2. master 에서 파일 생성
3. git add, commit

3. 새 브랜치 생성 후 해당 브랜치로 이동

4. 해당 브랜치에서 파일 생성

5. git add, commit

   ![image-20200205115423936](C:\Users\multicampus\codes\00_TIL\image\image-20200205115423936.png)

6. 해당 브랜치에서 파일 목록 확인

7. master 로 이동 후 파일 목록 확인

   ![image-20200205115535119](C:\Users\multicampus\codes\00_TIL\image\image-20200205115535119.png)

8. merge 후 master 에서 파일 목록 확인

![image-20200205115931712](C:\Users\multicampus\codes\00_TIL\image\image-20200205115931712.png)

http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html

- hotfixes : 급하게 고쳐야 하는 경우
- release/staging/test branches : 해당 코드의 테스트가 가능한 가상 서버에 연결
- develop : 대부분의 큰 단위 개발이 이루어짐
- feature branches : 한 단위/기능별 개발



### 3) branching 이후 master 에 신규 commit 이 있는 경우에 merge 하면? 

- **auto merge**

  - 개별 브랜치의 작업들이 충돌하지 않을 때는 git이 자동으로 merge (auto merge)를 해준다.

  ![image-20200205133216763](C:\Users\multicampus\codes\00_TIL\image\image-20200205133216763.png)

  ![image-20200205133251763](C:\Users\multicampus\codes\00_TIL\image\image-20200205133251763.png)

  ![image-20200205133313941](C:\Users\multicampus\codes\00_TIL\image\image-20200205133313941.png)

  

- **conflict merge**

  - 브랜치 이동은 **working tree clean** 을 확인한 후에 해야 한다.

  ![image-20200205134717510](C:\Users\multicampus\codes\00_TIL\image\image-20200205134717510.png)

  ![image-20200205134748573](C:\Users\multicampus\codes\00_TIL\image\image-20200205134748573.png)

  

  - merge로 인해상충되는 부분이 있을 경우엔 auto merge 가 실패하게 되고, git이 유저에게 의견을 묻는다.
    - Accept Current Change (master 작업내용을 지킨다.)
    - Accept Incoming Change (branch 작업내용을 따른다.)
    - Accept Both Changes (master 와 branch 작업내용을 모두 지킨다. )

  ![image-20200205135536752](C:\Users\multicampus\codes\00_TIL\image\image-20200205135536752.png)

  ![image-20200205140003308](C:\Users\multicampus\codes\00_TIL\image\image-20200205140003308.png)

  ![image-20200205140110947](C:\Users\multicampus\codes\00_TIL\image\image-20200205140110947.png)
  - master 와 branch 의 작업내용 중 어떤 것을 선택할지 결정 후, 새롭게 git add, commit 을 진행한다. (commit message convention "Resolve conflicts")

  ![image-20200205140334797](C:\Users\multicampus\codes\00_TIL\image\image-20200205140334797.png)



### 4) 골든벨 gitlab 사용 테스트

