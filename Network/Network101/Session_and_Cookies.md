# Session and Cookies

<br>

### HTTP Protocol

- `client`가 `server`에 **요청**
- `server`는 요청에 대한 처리를 한 후 `client`에 **응답**
- **응답** 후 연결을 해제 >> `STATELESS`
  - 지속적인 연결로 인한 자원 낭비를 줄이기 위해 연결을 해제함
    - but, `client` 와 `server`가 연결 상태를 유지해야 하는 경우 문제 발생 (ex. login info 저장 etc.)
    - 그래서 `client` 단위로 정보를 유지해야 하는 경우 **Cookie** 와 **Session** 이 사용된다!!

<br>

![image-20200421025031089](../images/image-20200421025031089.png)

<br>

### Session & Cookies in Java

|           | Session                                                      | Cookie                                                       |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Type      | javax.servlet.http.HttpSession (`interface`)                 | javax.servlet.http.Cookie (`Class`)                          |
| 저장 위치 | `server`의 memory에 **Object**로 저장<br>(사용자 정의 클래스를 reference 할 수 있음) | `client`의 컴퓨터에 **file**로 저장                          |
| 저장 형식 | **Object**는 모두 가능 <br>(일반적으로 Dto, List등 저장)     | **file**에 저장되기 때문에 **String** 형태                   |
| 사용 예   | Log-In 시 사용자 정보 / 장바구니                             | 최근 본 목록 / ID 저장 (자동 로그인) / pop-up menu에서 '오늘은 그만 보기' |

- 공통점
  - 전역에 저장하기 때문에 project 내의 모든 **JSP**에서 사용 가능
  - **Map** 형식으로 관리하기 때문에 `key 값` 의 중복 불허

<br>
