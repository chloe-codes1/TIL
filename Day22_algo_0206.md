# Day 22 - Algorithm (2/6)



### Ground Rules for Shared GitLab Repository

1. Master에 commit X
2. 항상 작업 시작 전에 본인의 branch 확인
3. merge 된 master pull 이후에는 본인 branch 삭제 후, 재 생성
4. 1-3 반복





### squash commit



> # How to squash commits



When submitting a pull request to WP Rig, we ask that you squash your commits before we merge.

Some applications that interact with git repos will provide a user interface for squashing. Refer to your application's document for more information.

If you're familiar with Terminal, you can do the following:

- Make sure your branch is up to date with the master branch.
- Run `git rebase -i master`.
- You should see a list of commits, each commit starting with the word "pick".
- Make sure the first commit says "pick" and change the rest from "pick" to "squash". -- This will squash each commit into the previous commit, which will continue until every commit is squashed into the first commit.
- Save and close the editor.
- It will give you the opportunity to change the commit message.
- Save and close the editor again.
- Then you have to force push the final, squashed commit: `git push --force-with-lease origin`.

Squashing commits can be a tricky process but once you figure it out, it's really helpful and keeps our repo concise and clean.











Cherry Picking....    -> look it up!





#### Things to do in the morning

```bash
# working tree clean 한 지 확인
$ git status  

# pull 하기
$ git pull origin master

# 기존 branch 삭제
$ git branch -d chloe

# 새로 branch 만들기
$ git branch chloe
```







### 재귀

1. Base case : 정답을 찾았을 때, 못 찾았을 때
2. Recursive Step : 계속 가야할 때

3. 재귀가 계속될 때 마다 누적되는 변수   => 재귀함수의 parameter(argument)



<br/>



### 부분집합의 수

> 집합의 원소 n개일 때, 공집합을 포함한 부분집합의 수 2n 개

















### 전수 나열 (Exhaustive Enumerate)

