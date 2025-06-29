# AMI

> AMI 자세-히 알아보기 실무 ver.

<br>

<br>

### What is AMI (Amazon Machine Image)?

- EC2 Instance를 통째로 **backup** 하는 것
- AMI가 backup 되어서 들어가있는 EBS 용량당 비용이 발생한다
  - `EBS Volume`은 **Snapshot**을 가지고 있다
    - Disk만 backup한 것이 **Snapshot**이다!
- Snapshot들은 **S3**에 저장된다
  - **AWS가 관리**하는 S3에 저장된다
  - **증분 backup**을 한다
    - 마치 docker images 처럼...
    - 그래서 두번째 backup은 더 빠르다!  
