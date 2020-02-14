# AWS Serverless Meet-up - 2/13



### 서버리스 아키텍쳐 특징

- 관리할 서버가 없다 (NoOps)
- 필요할 때마다 필요한 부분만 필요한 만큼 사용할 수 있다
- 컴퓨팅 리소스는 Lambda or Fargate
  - Lambda의 경우 자체적으로 connection을 유지할 수 없다!



#### Fargate

: a serverless compute engine for containers that works with both [Amazon Elastic Container Service (ECS)](https://aws.amazon.com/ecs/) and [Amazon Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/)



#### Lambda

: a compute service that lets you run code without provisioning or managing servers 





### 서버리스 아키텍쳐도 리얼타임 기능 만들 수 있다! 



####  How?

: by using API Gateway websocket or Pubsub 

- API Gateway 에서 websocket을 지원함
- Connection 기반의 solution은 아니지만 PubSub Solution도 가능하기는 함

<br/>

#### It's possible, but ...

- Front-end & Back-end 간의 통신을 위한 Data structure 정의 해야함
- Data 주고 받을 때의 Validation 필요
- Front & Back 양측에서 개발이 이루어져야 함
- Back-end 신경써야 할 것이 많음
  - High availality
  - reliability
  - scalability 

<br/>

####    ---> AppSync 를 사용하여 극복 가능!







## AWS AppSync

- Strong typing으로 인해 Validation 코드 거의 생략 가능 ( `GraphQL`의 특징 )
- Real-time 통신을 위해서 Back-end에서 해야할 것은 Subscription 을 스키마에 선언해두는 것 밖에 없음
  - Schema에 해당 기능을 쓸거라고 명시만 해놓으면 된다!
- Frontend  측에서는 `AppSync SDK`나 `Amplify`를 사용하면 간단히 Subscription이 가능하다!



<br/>



### Pros of AppSync

1. GraphQL에서 빠른 prototype 생성 및 개발
2. 실시간 협업 mobile & web app
3. 원활한 오프라인 작업
4. 안전한 데이터 액세스
5. 여러 원본의 데이터 결합
6. 데이터 충돌 감지 및 충돌 해결





### AppSync Realtime Architecture

(사진 참고)





### Serverless Streaming Architectures

1. DynamoDB Streams -> Lambda

   - 전형적인 서버리스 데이터 스트리밍 패턴 중 하나
   - Eventual Consistency or Event-driven processing 등을 처리하기에 적합
   - 병렬도가 매우 높은 작업에 대해서는 실시간성을 보장하지 않으므로 Kinesis DS가 좋음
   - DynamoDB Streams는 최대 24시간의 데이터 보존, 데이터 변경의 순번이 보증 가능한 서비스

   

2. RDS -> DMS -> Kinesis -> Lambda

   - RDS를 사용한 경우에도 스트리밍 처리가 가능함
   - Kinesis Data Stream은 샤드를 적절히 컨트롤 할 수 있어야함



#### Lambda로 불러온 후







AppSync를 Subscription의 용도로만 쓸거라면 굳이 Appsync용 DB 연결할 필요 없이 DynamicDB Stream를 쓰면 됨



- AppSync 구축 시에는 Serverless Framework를 추천
- Subscription 을 Schemaㅔ 추가하는 것만으로도 client 측에서 Subscription이 가능 (백앤드 작업 x)
- 필요한 기능은 mutation, subscription 뿐이지만, query를 schema에 등록하지 않으면 grapql schema 에러가 되므로 간단한 query 하나를 추가해야함



Lambda -> Appsync

- 실서비스용 SDK











*** 당근마켓도 GraphQL 쓴다고 함! 속닥속닥

​			-> admin 만들 때 개꿀이라고 함! 한번에 모든 데이터 받아올 수 있어서!

​            -> GraphQL 쓰면 node.js에서 data를 저장하는 방식이 빠를 수가 없는 방식임!

​            -> 당근마켓이 gRPC 쓰는 이유 = 개빠름..ㅎ_ㅎ 좋네





## GraphQL 발표





#### GraphQL이 느린 이유						

- http 라서

- resolver 때문
  - 이 부분은 해결 가능



​            





Look it up

-  gRPC

-  apollo gateway

-  3factor app
   - realtime GraphQL



## 



