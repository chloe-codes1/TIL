# AWS Builders - Cloud Economics

<br>

## Cloud Financial Management

<br>

### Cost Optimization Big 5

1. RIghtsizing

   - 적합한 사이즈의 인스턴스 사용
     - Amazon CloudWatch 지표 분석
     - 비용 탐색기 (cost explorer)

2. Scheduling

   - 사용시간에 알맞게 운영

3. Pricing

   - 다양한 가격정책 활용

     - `온 디멘드`
       - 약정 없이 사용한 EC2 인스턴스에 대한 비용만 지불
         - 알다시피 제일 비쌈,,ㅎ_ㅎ
       - 트래픽 예측 불가 시 적합

     - `예약 인스턴스 (RI: Reversed Instance)`
       - 1년 or 3년 약정
       - 온디맨드 대비 최대 75% 절약 가능
       - 일정/항시 켜두어야 하는 워크로드에 적합
     - `세이빙스 플랜 (SP)`
       - 1년 or 3년 약정
       - 일정/항시 켜두어야 하는 워크로드에 적합
       - **Details**
         - EC2, Fargate 및 Lambda 사용량을 최대 72% 절약할 수 있는 유연한 가격 책정 모델
           - ex) 한 시간 동안 $10을 약정하면, $10까지 할인된 시간당 금액으로 컴퓨팅 리소를 사용
         - 약정 사용량까지 할인된 Savings Plans 요금을 적용, 그 이외 사요은 `on demand`   요금 적용
       - **구매 방법**
         - AWS 비용 관리 들어가면 Savings Plans 있음!
     - `스팟 인스턴스`
       - 예비 컴퓨팅 용량을 통해 온디맨드 대비 최대 90% 절약
       - 시간 제한이 없는 배치성 워크로드

4. Storage

   - 다양한 스토리지 클래스사용

5. Monitoring

   - 목표 설정과 실행
