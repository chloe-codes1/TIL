# Guidelines for Selecting a GC

<br>

- Application의 성능이 가장 중요하고, 일시 정지 시간이 1초 이상이어도 상관없는 경우
  - VM이 알아서 collector를 선택하게 놔둔다
  - VM이 알아서 잘 선택하겠지만 수동으로 선택하고 싶다면 `XX:+UseParallelGC` option을 켠다
- 응답 시간이 전체 처리량보다 중요하고, 일시 정지 시간이 1 sec 이하여야 하는 경우
  - Concurrent Collector를 사용해 본다
    - `XX:+UseConcMarkSweepGC` 옵션이나 `XX:+UseG1GC` 옵션을 켠다
- 그래도 성능이 부족하다면
  - heap 사이즈와 generation 사이즈를 조절해 볼 것
