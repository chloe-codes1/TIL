# Amazon S3 - Creating a Bucket

> Back to basics!
>
> Summary of how to create an S3 bucket

<br>

<br>

## 1. Creating a Bucket

- Click **Create bucket** in `S3` on the `AWS Management Console`

<br>

### 1-1. Create Bucket

![image-20200805205352264](../../../kor/images/image-20200805205352264.png)

- Set only the bucket name and create everything else with default settings

<br>

### 1-2. Disable Block Public Access

![image-20200805210012807](../../../kor/images/image-20200805210012807.png)

<br>

<br>

## 2. Getting Keys

- Click **Add user** in `IAM` on the `AWS Management Console`

<br>

### 2-1. Add User

![image-20200730115846806](../../../kor/images/image-20200730115846806.png)

- Specify a username, select the checkbox above, then proceed to the next step

<br>

### 2-2. Create Group

![image-20200730121203017](../../../kor/images/image-20200730121203017.png)

- If you don't have an existing group, create a new group
- Select `Administrator Access` as the policy, then click Create group

<br>

### 2-3. Add User to Group

![image-20200730123058215](../../../kor/images/image-20200730123058215.png)

- Add the user to the group created above

<br>

### 2-4. Review and Download Credentials (.csv)

![image-20200730125450176](../../../kor/images/image-20200730125450176.png)

- After reviewing your final settings, click **Create user**
- Once the user is created, download the `.csv` file containing **credentials**
  - This credentials file contains the **Access Key ID** and **Secret Access Key**
    - Download it and store it in a safe place!!!!!

<br>

### 2-5. Add User Permissions

![](../../../kor/images/image-20200730130524225.png)

- Click **Add permissions** to add `S3` bucket permissions to the user created above

<br>

![image-20200730130657514](../../../kor/images/image-20200730130657514.png)

- Click **Attach existing policies directly**
- Search for `S3` in the search bar
- Select the `AmazonS3FullAccess` policy from the search results
- Click **Next**

<br>

### 2-6. Review Permission Addition

![image-20200730131039462](../../../kor/images/image-20200730131039462.png)

- After reviewing the added permissions, click **Add permissions**

<br>

*Done! So simple!* 
