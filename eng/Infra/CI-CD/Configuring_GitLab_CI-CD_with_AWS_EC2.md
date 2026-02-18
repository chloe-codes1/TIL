# Configuring GitLab CI/CD with AWS EC2

> Improving the ultimate inefficiency through deployment automation!!
>
> [Previously](https://github.com/chloe-codes1/TIL/blob/master/Server/Deployment/Deploying_a_SpringBoot-React_project_on_AWS_EC2.md), in the approach of deploying both backend and frontend servers on a single EC2 instance provided by SSAFY, redeployment required pulling the git repo and running a series of deployment commands sequentially, which was extremely inefficient and I wanted to fix it quickly.
>
> So while looking into CI/CD, since SSAFY uses GitLab instead of Github, I decided to use GitLab's own GitLab CI/CD for deployment automation!
>
> References: [namioto.ip.or.kr](https://namioto.ip.or.kr/2018/07/16/gitlab-ci%EB%A1%9C-%EC%9E%90%EB%8F%99%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0/)

<br>

## 0. Getting started with GitLab CI/CD

<br>

![GitLab CI/CD Flow~](../../kor/images/image-20200802144417101.png)

### What is GitLab CI/CD?

- GitLab CI/CD runs on Docker containers and deploys to connected Kubernetes
- When a push is made with a `gitlab-ci.yml` file present in the project root, the **Pipeline** (a bundle of tasks) specified in that file is executed

<br>

### Pipeline Components

- `Test`
  - Unit Test
  - Integration Test
  - E2E Test
  - Test Coverage measurement
- `Lint`
  - Code quality measurement
  - Code convention checking
- `Build`
  - Build
  - Bundling
  - Dockerfile build
  - Container registry push
- `Deploy`
  - Helm Chart
    - **What is Helm Chart?**
      - `helm` is a Kubernetes package manager
      - `helm chart` is a package format consisting of files needed to install an application!
  - KNative Functions
    - **What is KNative?**
      - An open source community project that adds components to Kubernetes for deploying, running, and managing serverless cloud native applications
  - KNative App (container) deployment

<br>

<br>

## 1. GitLab Runner

- GitLab Runner executes tasks on configured Stages when a push is made to the remote branch!
- For this to work, `GitLab Runner` must be installed on the remote repository

<br>

### 1-1. Add GitLab Official Repository

```bash
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash
```

<br>

### 1-2. Install Latest Version of GitLab Runner

``` bash
sudo apt-get install gitlab-runner
```

<br>

### 1-3. Registering Runners

> To run directly from the root account, skip steps 1 and 2!

#### 1. Create Account

```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

- Creates an account named `gitlab-runner`

#### 2. Install

``` bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
```

#### 3. Run

``` bash
sudo gitlab-runner start
```

#### 4. Register GitLab Runner

``` bash
sudo gitlab-runner register
```

- After entering the command above, you need to interactively enter 5 items

  ```bash
  # 1. Enter GitLab server URL
  Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com )

  # 2. Enter GitLab CI Token
  #   -> Can be found at Settings > CI/CD > Runners settings > Specific Runners!
  Please enter the gitlab-ci token for this runner:

  # 3. Enter Runner description
  Please enter the gitlab-ci description for this runner:

  # 4. Set Runner Tag
  #   -> Remember this as you need to write it in the gitlab-ci.yml file!!!! Important!!!!
  Please enter the gitlab-ci tags for this runner (comma separated):

  # 5. Set how the Runner will operate
  #   -> I chose Shell since I was going to use Shell Script
  Please enter the executor: docker-ssh, ssh, virtualbox, docker, parallels, shell, docker+machine, docker-ssh+machine, kubernetes:
  ```

<br>

### 1-4. Verify Registered Runner

- You can verify the registered Runner at **Settings > CI/CD > Runners settings > Specific Runners** as shown below

![image-20200801231330664](../../kor/images/image-20200801231330664.png)

<br>

<br>

## 2. Writing the `.gitlab-ci.yml` File

> Write the `.gitlab-ci.yml` file in the project root

<br>

#### Note

- This is a script I wrote for deployment automation of a SpringBoot - React project!!
- This yml file is the result of an enormous amount of trial and error, but since it is my first GitLab CI/CD file and there may be better approaches, please use it as reference only! (There probably are! I'm still looking into it!)
  - I will update when I find a more efficient method!!

ex)

```yaml
deploy-to-server:
  stage: deploy
  only:
    - master
  before_script:
    - echo 'start deployment'
    - whoami
  script:
    - cd /home/ubuntu/s03p12a112/
    - git pull origin master
    - cd backend
    - kill $(lsof -t -i:8000)
    - sudo mvn package
    - cd /home/ubuntu/s03p12a112/backend/target/
    - setsid nohup java -jar backend-0.0.1-SNAPSHOT.jar > /dev/null 2>&1 &
    - cd /home/ubuntu/s03p12a112/frontend/
    - sudo npm install
    - sudo npm run build
    - sudo service nginx restart
  after_script:
    - echo 'deployment is done'
  tags:
    - deploy
```

<br>

### YAML File Explanation

- `deploy-to-server`
  - The JOB name given when registering the GitLab Runner
- `stage`
  - As explained above, GitLab has groups that can perform specific tasks by Stage, and this indicates it is a **deploy** stage
- `only`
  - Configured so the **pipeline** is activated only when an event occurs on the **master** branch
- `before_script`
  - Literally the script to be executed before the shell script run by the runner
    - `whoami` command
      - Added to check if the configuration is correct since the GitLab Runner was registered with a separately created account (`gitlab-runner`) instead of the root account!
- `script`
  - Shell script to be executed by the GitLab Runner
  - Executed in the order of backend build then redeploy, frontend build then redeploy!
    - `kill $(lsof -t -i:8000)`
      - Terminates port 8000, which is the port used by the backend server
    - `setsid nohup java -jar backend-0.0.1-SNAPSHOT.jar > /dev/null 2>&1 &`
    - This was the part with the most trial and error
      - Initially, I activated the pipeline with `nohup -jar backend-0.0.1-SNAPSHOT.jar &` to run the existing jar file in the background, but the Job kept running without terminating
      - Changed to `nohup -jar backend-0.0.1-SNAPSHOT.jar > nohup.out &` but got a permission denied error
      - After many more modifications, I eventually changed it to write the .out file to `/dev`, a virtual filesystem in the Linux directory structure where device files are stored (it is not actually written! It is a directory that does not occupy physical space!)
      - As a result, the Runner's Job terminated successfully, and I confirmed the Jar file was running in the background!
- `after_script`
  - Literally the script to be executed after the script completes
- `tags`
  - Allows commands to be sent to Runners with a specific Tag
    - Remember the Tag set when registering the GitLab Runner and write it here!

<br>

<br>

## 3. Running the Pipeline

> As specified in the `.gitlab-ci.yml` file, the pipeline runs when an event occurs on the master branch

<br>

### Checking Job Execution Results

- You can check the executed pipelines at **CI/CD > Pipelines**

![The millionth and twenty-first attempt](../../kor/images/image-20200802155601932.png)

<br>

- Click on a **Pipeline** to see the executed **Job**
- When the Job executes successfully, you will see the following screen

![image-20200802155345341](../../kor/images/image-20200802155345341.png)

<br>

*Job succeeded!*

<br>

<br>

<br>

`+`

## Granting Sudo Privileges to the gitlab-runner Account

<br>

Initially, when running the Job, the newly created `gitlab-runner` account did not have sudo privileges, so I granted them

```bash
sudo visudo
```

- After entering the command above, I added the following content

  ```
  gitlab-runner ALL=(ALL) NOPASSWD: ALL
  ```

<br>

<br>

`+`

### Todos

- I am thinking about writing a `Dockerfile` and configuring a GitLab CI/CD Job that runs a docker image instead of this approach!
- Also looking into methods using Kubernetes! It's fun!
