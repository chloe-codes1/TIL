# ENTRYPOINT vs CMD

가장 큰 차이점은 컨테이너 시작 시 실행 명령에 대한 default 지정 여부이다

### ENTRYPOINT

> 항상 실행되는 기본 명령을 정의
>
- 해당 컨테이너가 실행될 때 반드시 최초에 실행되어야 하는 명령어가 있을 때 사용
- `docker run` 명령어에 인자값을 전달하여 실행해도 기존의 명령이 실행된다

### CMD

> ENTRYPOINT 명령의 기본 parameter 정의 / docker run 시 다시 쓰기 가능
>
- 컨테이너 실행 시 실행되는 명령어지만, 변경할 수 있을 때 사용
- `docker run` 명령어에 인자값을 전달하여 실행하면 `CMD` 에 명시된 명령어와 인자값은 무시된다
