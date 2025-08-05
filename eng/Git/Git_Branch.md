# Git branch

<br>

<br>

## 1. branch related commands

> Please generate a root-commit to proceed with Git branches.

1. Create branch

    ```bash
    (master) $ git branch {branch_name}
    ```

2. Switch branch

    ```bash
    (master) $ git checkout {branch_name}
    ```

3. Create and switch branch

    ```bash
    (master) $ git checkout -b {branch_name}
    ```

4. Delete branch

    ```bash
    (master) $ git branch -d {branch_name}
    ```

5. List branches

    ```bash
    (master) $ git branch
    ```

6. Merge branch

    ```bash
    (master) $ git merge {branch_name}
    ```

 * Merge {branch_name} from master branch

<br>

<br>

## 2. branch merge scenarios

> Branch-related commands are simple.
>
> You should be able to understand what situation you're in and use them freely in various scenarios.

<br>

### Scenario 1. fast-forward

> Fast-forward is a situation where there are no changes to the master branch after the feature branch is created

1. Create and switch to feature/crud branch

   ```bash
   git branch feature/crud
   git checkout feature/crud
   ```

   * or

   ```bash
   git checkout -b feature/crud
   ```

2. Commit after completing work

   * Create arbitrary files and commit
   * `add`, `commit`

3. Switch to master

   ```bash
   (feature/crud) $ git checkout master
   Switched to branch 'master'
   (master) $
   ```

4. Merge to master

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

5. Result -> fast-forward

   ```bash
   $ git log --oneline
   f219c8c (HEAD -> master, feature/crud) Complete CRUD)
   d66ff92 Init
   ```

6. Delete branch

   ```bash
   git branch -d feature/crud
   ```

---

### Scenario 2. merge commit

> In the process of merging different histories (commits), **different files are modified**
>
> Git performs auto merging and **a commit occurs**.

1. Create and switch to feature/signout branch

   ```bash
   (master)
   $ git checkout -b feature/signout
   Switched to a new branch 'feature/signout'
   (feature/signout) $
   ```

2. Commit after completing work

   ```bash
   touch signout.txt
   git add .
   git commit -m 'Complete'
   ```

3. Switch to master

   ```bash
   (feature/signout)
   $ git checkout master
   Switched to branch 'master'
   (master) $
   ```

4. *Generate additional commits on master!!*

   * **Please modify or create different files!**

5. Merge to master

   ```bash
   $ git merge feature/signout
   Merge made by the 'recursive' strategy.
    signout.txt | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 signout.txt
   ```

6. Result -> *merge commit automatically occurs*

7. Check graph

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

8. Delete branch

   ```bash
   $ git branch -d feature/signout
   Deleted branch feature/signout (was fb74094).
   ```

<br>

<br>

<hr>

### Scenario 3. merge commit conflict

> In the process of merging different histories (commits), **the same part of the same file is modified**
>
> Git cannot perform auto merging and shows a conflict message.
>
> It marks the location in the file according to standard format.
>
> You must manually fix it to the desired form of code and manually create a commit.

<br>

1. Create and switch to feature/signup branch

   ```bash
   (master)
   $ git checkout -b feature/signup
   Switched to a new branch 'feature/signup'
   ```

2. Commit after completing work

   * `add`, `commit`

3. Switch to master

   ```bash
   (feature/signup)
   $ git checkout master
   Switched to branch 'master'
   ```

4. *Generate additional commits on master!!*

   * **Please modify or create the same file!**

```bash
   $ git log --oneline
   3c81134 (HEAD -> master) Hotfix signout urls.py
   2125d5b Merge branch 'feature/signout'
   75f0abd README @ master
   fb74094 Complete signout
   f219c8c Complete CRUD)
   d66ff92 Init
```

5. Merge to master

   ```bash
   (master)
   $ git merge feature/signup
   Auto-merging urls.py
   CONFLICT (content): Merge conflict in urls.py
   Automatic merge failed; fix conflicts and then commit the result.
   
   (master|MERGING)
   ```

6. Result -> *merge conflict occurs*

   > You can check conflicted files with git status command.

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

7. Check and resolve conflicts

   ```
   <<<<<<< HEAD
   # signout
   =======
   # signup
   >>>>>>> feature/signup
   ```

8. Proceed with merge commit

    ```bash
    git commit
    ```

   * Vim editor screen will appear.

   * Check the automatically written commit message, press `esc` and type `:wq` to save and exit.
      * `w` : write
      * `q` : quit

   * Let's check the commit.

9. Check graph

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

10. Delete branch

    ```bash
    git branch -d feature/signup
    ```

    <br> 
