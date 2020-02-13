# AWS Serverless Meet-up - 2/13



### 서버리스 아키텍쳐 특징

- 관리할 서버가 없다 (NoOps)
- 필요할 때마다 필요한 부분만 필요한 만큼 사용할 수 있다



### 서버리스 아키텍쳐도 리얼타임 만들 수 있다! 

  -> How?   : API Gateway websocket or Pubsub 
  -> It’s possible, but…
          => AWS AppSync 로 가능해진다!

<br/>

### AWS AppSync

- Strong typing으로 인해 Validation 코드 거의 생략 가능 (GraphQL의 특징)
- 리얼타임 통신을 위해서 백엔드에서 해야할것은 Subscription 을 스키마에 선언해두는 것 밖에 없음
  - Schema에 해당 기능을 쓸거라고 명시만 해놓으면 된다!
- Frontend  측에서는 AppSnc SDK나 Amplify를 사용하면 간단히 Subscription



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

- apollo gateway

- 3factor app
  - realtime GraphQL



## 



