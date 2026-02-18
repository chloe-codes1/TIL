# Introduction to Terraform

> Reference: [Terraform docs](https://www.terraform.io/intro/index.html), [blog.naver.com/alice_k106](https://blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=221489260596&parentCategoryNo=&categoryNo=24&viewDate=&isShowPopularPosts=false&from=postView), [Inflearn] DevOps: Infrastructure as Code with Terraform and AWS Course by Song Juyoung

<br>

<br>

## Before getting started

> Content added after taking the Inflearn course

<br>

### IaC (Infrastructure as Code)

- Building infrastructure components such as servers, middleware, services through code
  - IaC has the advantages of code:
    - Ease of writing
      - Writing becomes faster!
    - Reusability
    - Maintainability, etc.

<br>

### Terraform by Hashicorp

> Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently

- Terraform is a tool made for IaC to create, change, and record infrastructure,
  - With easy syntax making it relatively easy to use, and a very large user base providing many examples for reference
- Uses the `.tf` file extension
- Supports not only Public Clouds like AWS, Azure, GCP but also various other Providers

<br>

### Basic Components of Terraform

- **provider**

  - The type of infrastructure to create with Terraform

    - Terraform supports a truly diverse range of providers!

  - Usually created as a `provider.tf` file

  - ex)

    ```yaml
    provider "aws" {
     region = "ap-northeast-2"
     version = "~> 3.0"
    }
    ```

    - Contains various arguments within the Provider
    - Plays the role of downloading files needed to work with AWS resources

<br>

- **resource**

  - The actual infrastructure resource to create with Terraform

  - Use any desired file name

  - ex)

    ```yaml
    resource "aws_vpc" "example" {
     cidr_block = "10.0.0.0/16"  # Many other arguments exist besides cidr_block
    }
    ```

  - This is code to create a VPC with Terraform
  - VPC also has various arguments and other components

<br>

- **state**

  - The state of resources created through Terraform

    - The actual result of executing Terraform code
    - Has the filename `terraform.tfstate`
      - The code can actually be very long in practice

  - ex)

    ```yaml
    {
     "version": 4,
     "terraform_version": "0.12.24",
     "serial": 3,
     "lineage": "3c77xxxx-2de4-7736-1447-038974a3c187",
     "outputs": {},
     "resources": [
      {...},
      {...}
     ]
    }
    ```

    - This is Terraform's state
      - It does not represent the current state of the infrastructure!!
        - It is the result of resources created using Terraform commands, not the actual state of the infrastructure!!
          - That is why it is important to keep the **state file** and the **actual infrastructure state** in sync!
    - State can be stored in a remote storage **backend**
      - Most teams in production currently use backends

<br>

- **output**

  - Saving resources created with Terraform as variables in the state file

  - ex)

    ```yaml
    resource "aws_vpc" "default" {
     cidr_block = "10.0.0.0/16"  # Many other arguments exist besides cidr_block
    }

    output "vpc_id" {
     value = aws_vpc.default.id
    }

    output "cidr_block" {
     value = aws_vpc.default.cidr_block
    }
    ```

    - Referencing vpc id or cidr values and saving them as a variable called `vpc_id` in the **state** file
    - Parts extracted as output can later be reused using `remote state`

<br>

- **backend**
  - The section specifying where to store Terraform state
    - The **space** for storing **state files** generated as variables through **output**
  - Using a backend stores the latest deployed state externally, enabling **collaboration** with others!
    - A representative example is AWS S3

- **module**

  - Defining commonly usable code literally in module form

    - Has strengths in reuse

  - Think of it as a kind of **function**

    - Means creating **one module** from multiple terraform code pieces by only changing **variables**

  - ex)

    ```yaml
    module "vpc" {
     source = ":./_modulesvpc"

     cidr_block = "1.0.0.0/16"
    }
    ```

    - Mainly used when creating the same form repeatedly from a single Terraform code

<br>

- **remote state**

  - Referencing state from another path

    - A concept of remote referencing
    - Mainly used when loading `output` variables

  - Using remote state allows referencing shared services like `VPC`, `IAM` from other services

    - If you specify the backend information where the **tfstate file (latest terraform state information)** is stored,
      - Output information is retrieved from that backend

  - ex)

    ```yaml
    data "terraform_remote_state" "vpc"{
     backend = "remote"

     config = {
      bucket  = "terraform-s3-bucket"
    region  = "ap-northeast-2"
      key    = "terraform/vpc/terraform.tfstate"
     }
    }
    ```

    - remote state retrieves variables generated through output from the **state** specified in the key value

<br>

### How Terraform Works

- There are 3 types of configuration states in Terraform:
  1. **Local code**
     - Code that the developer is currently writing/modifying
  2. **Actual AWS infrastructure**
     - Infrastructure actually deployed on AWS
  3. **State stored in backend**
     - The most recently deployed terraform code configuration
       - `tfstate` file
- The most important thing here is to **make the `actual AWS infrastructure` and `state stored in backend` 100% consistent**!!!
  - While operating Terraform, it is important to keep these two as close to 100% identical as possible,
    - Terraform provides various commands like **import** and **state** for this purpose
- Infrastructure definition starts from `local code` first
  - The developer defines terraform code locally, then
  - Provisions the code to actual infrastructure
    - At this point, a backend is configured to store the latest code

<br>

### Basic Terraform Commands

#### init

- Performs various setup tasks for using Terraform commands
  - Creates a `.tfstate` file for storing state in the specified backend
    - The most recently applied terraform history is stored here
  - When init is complete, a `.terraform` file containing the contents defined in `.tfstate` is created locally
  - If another developer has already defined infrastructure in `.tfstate`, other developers can **sync** locally through the **init** task

#### plan

- Shows the predicted result of how the code written in Terraform will actually be created
  - However, even if there are no errors in the plan, errors may occur when actually applied, so be careful!
  - **The plan command does not make changes to any configuration**

#### apply

- The command to actually create infrastructure based on Terraform code
  - When **apply** completes, the actual infrastructure is created on AWS,
    - And the work results are saved in the backend's `.tfstate` file
      - The results are also saved in the local `.terraform` file
  - Since this command affects actual infrastructure, it must be executed carefully!
    - That's why you should always run `plan` before `apply`!

#### import

- A command to move already-created resources into a `terraform state` file

  - Used when you want to move already-created resources into code

  - Plays the role of saving **state information** of the resource to the local `.terraform`

    - However, **it does not generate code!!**
      - It is not saved to the backend until apply
      - If you run plan after import, it will show results saying the resource will be deleted or changed **because the code does not exist locally**
        - Based on this result, you can write the code

  - ex)

    ```bash
    terraform import [options] ADDRESS ID
    ```

#### state

- A command to manage Terraform state

  - You can view actually created infrastructure

    - ex)

      ```bash
      terraform state list
      ```

  - Has sub-commands like mv, push, etc.

#### destroy

- A method to delete all created resources based on the state file

#### workspace

- A command used for workspace management

  - ex1)

    ```bash
    $ terraform workspace list
      default
    * product
    ```

    - Shows the list of workspaces
    - The currently active workspace is marked with an asterisk (`*`)

  - ex2)

    ```bash
    terraform workspace select [NAME]
    ```

    - Used to switch to a different workspace

  - ex3)

    ```bash
    terraform workspace new [NAME]
    ```

    - Used to create a new workspace

<br>

<br>

## What is Terraform?

> Content organized from Terraform docs and blog references

<br>

- A tool to safely and efficiently **build**, **modify**, and **version** infrastructure
- While you might think Terraform is similar to `Ansible` or `Chef`, Terraform differs in that it is focused on **specific cloud environments**
  - `Ansible` can deploy **identical environments** via SSH to regular servers, virtual machines, or even Raspberry Pi,
  - While `Terraform` is primarily used for deploying environments on cloud platforms like AWS, GCP, etc.
    - The concept of defining infrastructure as code is the same as environment deployment tools like `Ansible`,
    - The difference is that it deploys environment as code tailored to specific **cloud platforms** rather than general **bare metal servers**

<br>

### Defining Infrastructure as Code & Reproducible Infrastructure

- What Terraform's website emphasizes is
  - **Infrastructure as a Code**
  - **Reproducible Infrastructure**
- This means that by defining and using cloud infrastructure environments as code, whether AWS, GCP, or Azure, **identical infrastructure** can be reproduced
  - Within the same cloud!

- Since cloud infrastructure is explicitly defined in code, running it dozens of times will always produce the **same environment**.

<br>

### Workflow When Adopting Terraform

- Using pre-prepared Terraform templates, you can deploy the desired environment to the cloud
  - For example, save VPC in a `vpc.tf` file, EC2 instances in an `instance.tf` file, and subnets in a `subnet.tf` file, then simply run **Terraform** to perfectly reproduce the same environment in the cloud
  - This cloud environment configuration is not done manually by people, but by inputting code written in **HCL (Hashicorp Configuration Language)** into Terraform
- Since all cloud settings are explicitly written in code, it becomes possible to **deploy cloud infrastructure identically**
- Multiple versions of code can be written to suit various requirements, managing cloud infrastructure **revisions**
  - Simply using pre-prepared Terraform configuration files with Terraform allows you to create complex AWS cloud environments all at once and delete them all at once

<br>

<br>

## Terraform Quickstart

<br>

### 0. Structure of Terraform Files

- Terraform files (`.tf` files) are generally structured as follows:

![image-20200921011906162](../../kor/images/image-20200921011906162.png)

- **resource**
  - The object type used in Terraform files
    - `resource` representing variables
    - `data` representing Data, etc.
- **aws_key_pair**
  - The resource name for AWS SSH key pairs
    - The name Terraform uses to refer to objects used in AWS
    - These names are documented in the official Terraform docs
- **terraform-key**
  - The name that will uniquely identify this object in the Terraform file
    - It is best to use names that are unique across all files whenever possible

<br>

### 1. tf init

- Execute at the root of the terraform project

- Terraform requires an **initialization** step before use

  - Use the **terraform init** command to initialize the terraform directory

- Used when:

  1. Starting a project for the first time
  2. When `modules` have changed

- ex)

  ```bash
  ~/workspace/monocoque/dev-musinsa-main master* ⇣ 17s
  ❯ tf init
  Initializing modules...

  Initializing the backend...

  Initializing provider plugins...

  Terraform has been successfully initialized!

  You may now begin working with Terraform. Try running "terraform plan" to see
  any changes that are required for your infrastructure. All Terraform commands
  should now work.

  If you ever set or change modules or backend configuration for Terraform,
  rerun this command to reinitialize your working directory. If you forget, other
  commands will detect it and remind you to do so if necessary.
  ```

<br>

### 2. tf workspace

- Also execute at the root path of the project

- Commands

  - `tf workspace list`

    - View workspace list

      ex)

      ```bash
      ~/workspace/monocoque/dev-musinsa-main master* ⇣
      ❯ tf workspace list
      * default
        main
      ```

  - `tf workspace select main`

    - Select a workspace

      ex)

      ```bash
      ~/workspace/monocoque/dev-musinsa-main master* ⇣
      ❯ tf workspace select main
      Switched to workspace "main".
      ```

<br>

### 3. tf plan

- Also execute at the root path of the project

- The process of **verifying** whether the contents of all `.tf` files in the Terraform project directory can actually be applied is called a plan

- When the **terraform plan** command is executed:

  - It shows the plan of which resources will be created,
  - Modified, and
  - Deleted

- ex)

  ```bash
      ~/workspace/monocoque/dev-musinsa-main master*
      ❯ tf plan
      Refreshing Terraform state in-memory prior to plan...
      The refreshed state will be used to calculate this plan, but will not be
      persisted to local or remote state storage.

    ...

      Plan: 6 to add, 0 to change, 0 to destroy.

      ------------------------------------------------------------------------

      Note: You didn't specify an "-out" parameter to save this plan, so Terraform
      can't guarantee that exactly these actions will be performed if
      "terraform apply" is subsequently run.
  ```

- Review the execution results to confirm everything is being created as planned

<br>

### 4. tf apply

- Also execute at the project root path
- The process of **creating**, **modifying**, and **deleting** resources according to the contents of all `.tf` files in the Terraform project directory is called **applying**
- Before running this command, pending changes can be verified using the **plan** command above

<br>

### 5. tf force-unlock [ID]

- Used when terraform state lock occurs
- Enter the ID value after tf force-unlock when the following error message is displayed

```bash
Error: Error locking state: Error acquiring the state lock: ConditionalCheckFailedException: The conditional request failed
Lock Info:
  ID:        ID value
  Path:      PATH
  Operation: OperationTypePlan
  Who:       chloe@Chloes-MacBookPro.local
  Version:   0.12.26
  Created:   2021-02-05 03:26:02.065859 +0000 UTC
  Info:


Terraform acquires a state lock to protect the state from being written
by multiple users at the same time. Please resolve the issue above and try
again. For most commands, you can disable locking with the "-lock=false"
flag, but this is not recommended.
```
