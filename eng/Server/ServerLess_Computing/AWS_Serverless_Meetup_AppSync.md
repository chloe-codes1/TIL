# AWS Serverless Meet-up - 2/13

> Real-time Serverless Architecture Using AppSync
>
> Speaker :  Kim Taewoo   <https://dev.classmethod.jp/author/kim-taewoo/>

<br><br>

### Characteristics of Serverless Architecture

- No servers to manage (NoOps)
- You can use only what you need, when you need it, as much as you need
- Computing resources are `Lambda` or `Fargate`
  - In the case of Lambda, it cannot maintain a connection on its own!

<br>

#### Fargate

: a *serverless compute engine* for containers that works with both [Amazon Elastic Container Service (ECS)](https://aws.amazon.com/ecs/) and [Amazon Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/)

<br>

#### Lambda

: a compute service that lets you run code without provisioning or managing servers

<br>

<br>

### Serverless Architecture Can Also Build Real-time Features

<br>

#### How?

: by using `API Gateway websocket` or `Pubsub`

- API Gateway supports websocket
- Although it is not a connection-based solution, PubSub Solution is also possible

<br/>

#### It's possible, but

- Need to define Data structure for communication between Front-end and Back-end
- Validation is needed when exchanging Data
- Development needs to happen on both Front & Back sides
- Many things to consider on the Back-end
  - High availability
  - reliability
  - scalability

<br/>

#### ---> Can be overcome by using AppSync

<br>

<br>

## AWS AppSync

- Validation code can be almost eliminated due to **Strong typing** (a feature of `GraphQL`)
- For **Real-time communication**, all you need to do on the Back-end is declare `Subscription` in the schema
  - You just need to specify in the Schema that you will use that feature!
- On the Frontend side, you can easily subscribe using `AppSync SDK` or `Amplify`!

<br>

### Pros of AppSync

1. Rapid prototype creation and development with GraphQL
2. Real-time collaborative mobile & web apps
3. Seamless offline operation
4. Secure data access
5. Combining data from multiple sources
6. Data conflict detection and resolution

<br>

<br/>

### AppSync Architecture for Real-time Data Communication

<br>

![image-20200307010708273](../../kor/images/image-20200307010708273.png)

<br>

### Serverless Streaming Architecture

<br>

![image-20200307011320581](../../kor/images/image-20200307011320581.png)

<br>

- One of the typical serverless data streaming patterns
- Suitable for handling `Eventual Consistency` or `Event-driven processing`
- **Scalable** & **Reliable** & **Cost Effective**
- For tasks with very high parallelism where real-time performance is not guaranteed, `Kinesis DS` is recommended
- `DynamoDB Streams` is a service that retains data for up to 24 hours and guarantees the order of data changes

<br>

<br>

![image-20200307012139759](../../kor/images/image-20200307012139759.png)

<br>

- Streaming processing is also possible when using RDS

- **Kinesis Data Streams** requires proper control of **shards**

  - `Shard`

    : A sequence of data records that is uniquely identified in a stream

- There is no need to necessarily connect **Kinesis Data Streams** to **Lambda**

  - but, for the purpose of integrating with **AppSync**, **Lambda** is sufficient!

- There are also methods to directly trigger **Lambda** from a DB (MySQL, PostgreSQL, etc.)

<br>

<br>

![image-20200307013708527](../../kor/images/image-20200307013708527.png)

1. Pattern where SQL connects to Lambda

2. Pattern where Kinesis connects to Lambda

3. Pattern where API Gateway connects to Lambda

4. Pattern where CloudWatch Alarms connects to Lambda

5. Pattern where CloudWatch Events connects to Lambda

   ... and a lot more!

<br>

<br>

### After Calling via Lambda

<br>

![image-20200307014333774](../../kor/images/image-20200307014333774.png)

<br>

## Demo Project Architecture

<br>

![image-20200307014508453](../../kor/images/image-20200307014508453.png)

<br>*If you only want to use AppSync for Subscription purposes, you don't need to connect a DB specifically for AppSync - you can just use DynamoDB Streams!*

<br>

### Microservice

- `API Gateway` -> `Lambda` -> `DynamoDB` configuration
- The most commonly used Serverless Architecture API back-end pattern
- Demo code written using a service that processes a simple input form as an example

<br>

<br>

### AWS AppSync

<br>

- *Serverless Framework* is recommended when building AppSync
- Just adding Subscription to the Schema enables client-side Subscription
  - No back-end work required
- The only needed features are **mutation** and **subscription**, but since not registering a query in the schema results in a `GraphQL schema error`, a simple query needs to be added
  - Write getOrder
- To perform **Mutation**, create **DynamoDB** as a Data source and set `TTL (Time-To-Live)`
  - Declare **expiresAt** as the **AWSTimestamp** type

<br>

<br>

### DynamoDB Streams -> Lambda

<br>

- DynamoDB Streams is a service that retains data for up to 24 hours and guarantees the order of data changes
  - but, for Realtime Services, the 24-hour data retention doesn't have much significance
- To increase parallelism, adjust the batch size!

<br>

<br>

### Lambda -> Appsync

<br>

- The only officially released AppSync Client SDK for production is the JavaScript version, so Amplify is recommended
- Points to note when running AppSync Client SDK on Lambda
  - You need to import `isomorphic-fetch`
  - You need to change `disableOffline` to true

<br>

<br>

## What Else Could Be Done with AppSync?

<br>

### State Management by AppSync

- Serverless Architecture patterns aim for a **Rich Client**
  - but, it is not good for the complexity of Front-end code to increase excessively
- **State Management** contributes significantly to the code complexity of the Front-end
- Could the code complexity introduced by **State Management** be resolved by relying on `AppSync Subscription`?
  - but, this creates a dependency on Network speed/stability
- However, in the 5G era, wouldn't this not be a big problem?

<br>

<br>

##

`+`

#### Why GraphQL is Slow

- Because it uses http

- Because of the resolver
  - This part can be resolved

​         <br>

Karrot (Danggeun Market) also uses GraphQL! (whisper whisper)

-> They say it's great for building admin panels! Because you can fetch all data at once!

-> When using GraphQL, the way node.js stores data can't be fast!

<br>

The reason Karrot uses gRPC == the speed is incredibly fast

<br><br>

`+`

#### Looked up after the meetup

1. `gRPC`

   <br>

   ![image-20200307032408544](../../kor/images/image-20200307032408544.png)

   <br>

   - *gRPC (gRPC Remote Procedure Calls)* is an open source remote procedure call (RPC) system initially developed at Google in 2015
   - In gRPC, a client application can directly call a method on a server application on a different machine as if it were a local object, making it easier for you to create distributed applications and services.
   - As in many RPC systems, gRPC is based around the idea of defining a service, specifying the methods that can be called remotely with their parameters and return types.
   - On the **server side**, the server implements this interface and runs a gRPC server to handle client calls.
   - On the **client side**, the client has a stub (referred to as just a client in some languages) that provides the same methods as the server.

<br>

2. `apollo gateway`

   <br>

   ![image-20200307032923930](../../kor/images/image-20200307032923930.png)

   <br>

   - Apollo is an implementation of `GraphQL` designed for the needs of product engineering teams building modern, data-driven applications.
   - It encourages an `agile`, incremental approach and takes special care to avoid requiring any changes to existing APIs and services.
   - Apollo puts particular emphasis on tooling and workflows.
   - Apollo is best used as a new layer in your stack that sits between your services and your applications.
   - It's a combination of open source components, commercial extensions, and cloud services.

<br>

<br>

3. `3factor app`

   <br>

   - 3factor app is an architecture pattern for modern full-stack apps.
   - Today, it is possible to build apps that have high feature velocity and scalability from the get go.
   - An architecture pattern which is composed of **3 factors**:

     1. Realtime GraphQL
     2. Reliable eventing
     3. Async serverless

<br>
