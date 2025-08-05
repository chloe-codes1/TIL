# Git Tips & Tricks

> Let's become a Git master

<br>

<br>

## 1. Git Basics

<br>

### (1) Start project management with Git : `git init`

- Create a `TIL` folder to record what you learn going forward. Create this folder at the top level
- After moving to the `TIL` folder in `git bash`, start `git` management with the following command

```bash
git init
```

<br>

### (2) Staging for Commit : `git add`

- Select files to take a snapshot of the current code state (== Add files to Staging Area)

``` bash
git add [filename] # . uploads all changes to staging area
```

<br>

### (3) Save snapshot for version management : `git commit`

- `commit` the snapshot of the current state to proceed with version management.

``` bash
git commit -m "commit message"
```

<br>

### (4) Add remote repository information : `git remote`

- Create a Github remote repository and connect it with the `TIL` folder
- Enter only when a new remote repository is added.

```bash
git remote add origin [github remote repository address]
```

<br>

### (5) Pull code to local repository `git pull`

- Pull code from Github remote repository and apply `commits` for each `branch`.

```bash
git pull

git pull [remote repository name] (specify a remote to pull from)
```

<br>

### (5) Push code to remote repository `git push`

- Finally push to Github remote repository.

```bash
git push

git push origin master
```

#### Tip

: If the current branch is the branch of the repo you want to push to, you only need to enter `$ git push` command!

<br>

### (6) Other commands

- Check current `git` status `git status`

````bash
git status
````

- Check version management history

```bash
git log
```

- `git` configuration (user.name & user.email) : **Set once at the beginning**

```bash
git config --global user.name "Chloe Kim"
git config --global user.email "juhyun.kim@lindsey.edu"
```

- Undo `git add` before commit

```bash
git reset
```

<br><br>

## 2. `README.md`

> A markdown document that records information about remote repository. Generally describes how to use the project.

<br>

### (1) Create `README.md` file

- Create `README.md` file in the `TIL` folder (top level). The name must be set to **README.md**.

```bash
touch README.md
```

<br>

### (2) Add simple content about (your own) principles

- Write the `README.md` file based on what you learned and practiced in the markdown writing pdf.
- Write freely in format but follow markdown syntax (semantic).

<br>

### (3) Save and version management : `add`, `commit`, `push`

- When writing is complete, leave commit history and push to remote repository with the following commands.

```bash
git add README.md
git commit -m "add README.md"
git push origin master
```

<br>

<br>

## 3. Shared Repository

<br>

> Fast forward merge practice

```bash
# Check branch
$ git branch

# Create new branch
$ git branch [branch name]

# Move to another branch
$ git switch [branch name to move to]

# Move to another branch ver2)
$ git checkout [branch name to move to]


# Delete branch
$ git branch -d [branch name to delete]

# FF(=Fast Forward) merge
# : Move to the main branch and proceed (ex. move to master and create chloe)
$ git merge [branch name to merge]

# Create new branch and move
$ git switch -c [new branch to create]

# Create new branch and move ver2)
$ git checkout -b ashley  # -b means branch


# View git log as graph
$ git log --oneline --graph


```

<br>

<br>

## 4. Go back to specific point

<br>

> Go back based on specific commit

```bash
git checkout f008d8f
```

<br>

> Create test branch and move

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

> Check reference log

```bash
git reflog
```

<br>

> Check where head is

```bash
$ git log --oneline
fc58709 (HEAD -> master, origin/master, origin/HEAD) Add README.md
fd2e992 06 | Article C with ModelForm
f008d8f (test) 05 | Article Index
c2be3bc 04 | Article Model
0d28d53 03 | startapp articles
5afc6a9 02 | settings
a046911 01 | startproject
```

<br>

> Go back to test branch

```bash
$ git checkout test
Switched to branch 'test'
```

<br>

<br>

## 5. Revert commits uploaded to remote repository

<br>

### Method 1) Revert commit locally then force Push

> Revert commit with `$ git reset`

```bash
git reset --hard HEAD       (going back to HEAD)

git reset --hard HEAD^      (going back to the commit before HEAD)

git reset --hard HEAD~2     (going back two commits before HEAD)
git reset --hard HEAD^^    (another syntax for going back two commits)
```

<br>

> Force Push with `-f` or `--force` command

```bash
git push -f origin master

git push --force origin master
```

<br>

<br>

### Method 2) Use `git revert`

- Method 1 has the problem of forcibly manipulating remote repository commit history
- but, using `git revert` treats the work of reverting commits as one commit and adds it to commit history

<br>

>Create another commit that removes changes from specific commit

```bash
git revert --no-commit [hash of commit to revert]     

git revert --no-commmit [range of commits to revert]

git revert --no-commit Head~3
```

<br>

<br>

`+`

- Content in `master` branch is automatically deployed
  - `master` is in deployable state

<br>

### Clone only specific branch

```bash
git clone -b {branch_name} --single-branch {repository URL}
```

<br>

### Get specific branch from remote repository

> First check what branches exist in remote repository

```bash
git branch -r
```

<br>

> Check remote repository + local branches

```bash
git branch -a
```

<br>

#### Get branch from remote repository with **same name**

```bash
git checkout -t [origin/remote repository branch name to get]
```

<br>

#### Get branch from remote repository with name change

``` bash
git checkout -b [branch name to create][remote repository branch name to get]
```

<br>

#### Modify unpushed Commit message

```bash
git commit --amend
```

<br>

### `git fetch`

> Can check how far remote branch has gone

- git pull == git fetch && merge

<br>

### `git rebase`

> Reposition

- Adding `-i` at the end allows interactive execution

<br>

<br>

## 6. Using Submodule

<br>

### What is Submodule?

- Having another sub repo inside Git main repo
  - main repo does not manage sub repo!

- Using **Submodule** allows sharing commonly used logic between projects!

<br>

### Add Submodule

```bash
git submoduel add [repo address]
```

- After this, you can commit without separate `git add`

<br>

### Update Submodule

#### Update main repo

```,
git pull
```

- Running the following command at main repo root updates main repo

<br>

#### Update sub repo

```bash
git submodule update --remote --merge
```

- Running the above command at main repo root updates sub repo according to the relationship between updated main repo and sub repo 
