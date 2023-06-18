# CompletableFuture

<br>

### CompletableFuture 란?

- Java에서 비동기 프로그래밍을 지원한다
- Future와 CompletionStage를 구현한 class다
  - `Future`란?
    - 비동기적인 연산의 결과를 표현하는 클래스
      - 예약된 작업에 대한 결과를 알 수 있다
    - multi-thread 환경에서 처리된 데이터를 다른 thread에 전달할 수 있다
    - 내부적으로 `Thread-Safe` 하게 구현되어 있기 때문에 `synchronized block` 을 사용하지 않아도 된다
- Future에서 하기 어려웠던 아래의 작업을 수월하게 할 수 있게 해준다
  - Future를 외부에서 완료시킬 수 없다
    - 취소하거나, get()에 타임아웃을 설정할 수 없다
  - 블로킹 코드 (get())를 사용하지 않고서는 작업이 끝났을 때 콜백을 실행할 수 없다
    - Future를 통해 결과값을 만들고 무언가를 하는 작업은 get() 이후에 와야한다
  - 여러 Future를 조합할 수 없다
    - ex) 이벤트 정보를 가져온 다음에 이벤트에 참여한 회원 목록 가져오기
  - 예외 처리용 API를 제공하지 않는다
