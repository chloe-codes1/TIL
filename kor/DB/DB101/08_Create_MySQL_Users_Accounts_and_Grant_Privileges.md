# Create MySQL Users Accounts and Grant Privileges

> 적는자가 살아남는다.........

<br>

### MySQL 계정 생성하기

```
mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

- 다른 Host로부터의 접속을 허용하려면 **localhost** 위치에 **IP Address** 적으면 된다
- 모든 Host로부터의 접속을 허용하려면 **'%'** wildcard를 사용한다

<br>

### grant 명령어로 사용자 권한 설정하기

<br>

#### 사용자 권한 설정

```
mysql> GRANT ALL PRIVILEGES ON dbname.table TO 'userID'@'host' IDENTIFIED BY 'password';
```

#### 모든 db 및 table에 접근 권한 설정

```
mysql> GRANT ALL PRIVILEGES ON *.* TO userID@host IDENTIFIED BY 'password';
```

#### 모든 db 및 테이블에 권한을 주고 로컬 및 리모트에서도 접속가능하도록 설정

```
mysql> GRANT ALL PRIVILEGES ON *.* to userID@'%' IDENTIFIED BY 'password';
```

#### 설정한 권한 적용

```
mysql> FLUSH PRIVILEGES;
```

- 실행해야 적용된다!

#### 권한 삭제

```
mysql> REVOKE ALL ON dbname.table FROM userID@host
```

#### 권한 조회

```
mysql> SHOW GRANTS FOR userID@host
```
