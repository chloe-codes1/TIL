# Jenkins Build and ECR Push

> Docker build with Jenkins and push to Amazon ECR!

<br>

<br>

### Before getting started

- [Learn about Docker](../../Docker/01_Getting_Started_with_Docker.md)
- [Learn about Amazon ECR](../../AWS/AWS_Services/Amazon_ECR.md)

<br>

<br>

### Docker Build & Push with Jenkins

<br>

#### 1. Include a `Dockerfile` in the service's source code

#### 2. Configure the `jenkins` server to be able to access ECR

#### 3. Create a deployment Job for the service in `jenkins`, and set the Job to build a new image using the pre-included Dockerfile when executed

#### 4. Build a new docker image on the `jenkins` server and then push the image to ECR

#### 5. Finally, on the test server, pull the new image from ECR, delete the existing container, and create a new container

<br>

<br>

### Configure Jenkins job example

<br>

#### ex1) Discard old builds

![image-20201020130511370](../../kor/images/image-20201020130511370.png)

- **Discard old builds**

  - With the settings shown in the example above, Build History is stored for 10 days and a maximum of 20 build histories are kept

    ex)

    ![image-20201022013851907](../../kor/images/image-20201022013851907.png)

<br>

#### ex2) Invoke Gradle script

![image-20201022014231728](../../kor/images/image-20201022014231728.png)

- For Java projects built with Gradle, you can specify Tasks as shown above

<br>

#### ex3) Execute shell

![image-20201022014449325](../../kor/images/image-20201022014449325.png)

- You can write shell scripts to be executed during the Jenkins job build as shown above

<br>

#### ex4) Post-build Actions

![image-20201022014706282](../../kor/images/image-20201022014706282.png)

- To save artifacts after the build, you can configure settings as shown above
