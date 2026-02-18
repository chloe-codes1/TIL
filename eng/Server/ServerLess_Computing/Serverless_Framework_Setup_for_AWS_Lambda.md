# Serverless Framework Setup for AWS Lambda

> Organizing how to write the serverless.yml file and deploy commands

<br>

## 1. How to Write the serverless.yml File

- The serverless.yml file is created at the root path of the project
- Serverless Framework deploys based on this file

<br>

### ex1)

![serverless-example](../../kor/images/serverless-example.png)

<br>

### **service**

- Project name

<br>

### **provider**

- **name**
  - Enter information about the Cloud service provider
    - Here, since this is a yaml file for deploying to AWS Lambda, *aws* is specified
- **runtime**
  - Enter the runtime version being used
- **stage**
  - Enter the stage you want to deploy to
    - `${opt: stage, 'dev'}`
      - When deploying using the sls command in the local environment, if a stage option is given, that stage is used; otherwise, dev is applied as the default
        - ex) sls deploy -s prod
          - Options for setting the stage
            1. `-s`
            2. `--stage`
- **region**
  - Enter the region information for the lambda being deployed
- **versionFunctions**
  - Set to true if you want versioning
- **memorySize**
  - Enter the memory size
    - The default is set to 1024
- **deploymentBucket**
  - Specify the name of the AWS S3 bucket where the deployment will be stored
    - If not set separately, a new bucket will be created
- **deploymentPrefix**
  - You can specify a prefix to store within the deployed bucket
    - The default is set to serverless

<br>

### package

- **include**
  - Enter the directories to include in the deployment package
- **exclude**
  - Enter the directories to exclude from the deployment package
- **individually**
  - Set to true if you want to package each function separately
    - The default value is false

<br>

### custom

- **pythonRequirements**
  - This section is needed for using the `serverless-python-requirements plugin`
    - **dockerizePip**
      - Set to true if you want to use docker packaging
        - The default is false
    - **layer**
      - Set to true if you want to create the generated dependencies as a Lambda Layer
        - The default is false

<br>

### functions

- **function_name**

  - Function name (this is the function name used in the serverless framework, not the Lambda function name)

    - **name**

      - The function name that will be created in AWS Lambda

        - To create different functions depending on the stage,

          `${opt: stage, 'dev'}`

          was configured

          - The same setting exists in provider > stage above

    - **handler**

      - Enter the file and function name for that function
        - ex) handler.do_optimize
          - That Lambda function is executed from the do_optimize() function in handler.py

    - **layers**

      - Enter the layers to register for that function
        - Here, since the layer created using the serverless-python-requirements plugin is registered as a lambda layer, it was set to `- { Ref: PythonRequirementsLambdaLayer }`

<br>

### plugins

- Enter the serverless plugins you want to use among those installed via npm
  - External plugins must be installed at the root of the project for them to work properly

<br>

<br>

### ex2)

![serverless-vpc](../../kor/images/serverless-vpc.png)

<br>

### provider

- **vpc**
  - Enter VPC information for the Lambda function
- **securityGroupIds**
  - Enter the Security group ID for that lambda function
- **subnetIds**
  - Enter the subnet ID for that lambda function

<br>

`+`

#### Caution

If VPC information is not specified in `serverless.yml`, when performing a full deployment rather than deploying only the lambda function, the VPC information will be **reset** and you will need to reconfigure it in the AWS Console!

Make sure to include VPC information in serverless.yml!

<br>

<br>

## 2. Deploy commands

Only some of the commands are organized here, so refer to the reference materials below to check the full list of commands

<br>

### Stage

- `--stage` or `-s`
  - You can set the stage you want to deploy to
    - ex)
      - sls deploy -s prod

### Function

- `--function` or `-f`
  - You can deploy a specific function only
    - In the example above, since a Lambda Layer is created and deployed together, on redeployment after the initial deployment, if only the code has changed, the layer does not need to be recreated, so you can use this option
      - ex)
        - sls deploy -f do_optimize

<br>

<br>

<br>

`+`

### Reference Materials

- [Serverless.yml Reference](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml/)
- [Serverless Python Requirements Plugin](https://www.serverless.com/plugins/serverless-python-requirements)
- [Serverless deploy commands](https://www.serverless.com/framework/docs/providers/aws/cli-reference/deploy/)
