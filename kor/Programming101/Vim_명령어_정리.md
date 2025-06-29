# Vim 명령어 정리

> Vim 멋있어....
>
> Reference: [keycdn.com](https://www.keycdn.com/blog/vim-commands), [velog.io/@recordboy](https://velog.io/@recordboy/VIM-%EB%AA%85%EB%A0%B9%EC%96%B4)

<br>

<br>

### 실행하기

| Command          | Description                             |
| ---------------- | --------------------------------------- |
| vi FILE          | file 열기                               |
| vi FILE_1 FILE_2 | file 두 개를 차례로 열기                |
| view FILE        | 읽기 모드로 열기1                       |
| vi -R FILE       | 읽기 모드로 열기2                       |
| vi + FILE        | cursor가 가장 마지막 행에 위치하게 열기 |
| vi  +n FILE      | cursor가 n행에 위치하게 열기            |
| vi -r FILE       | 손상된 file 회복                        |

<br>

### Insert modes

| Command | Description                                   |
| ------- | --------------------------------------------- |
| i       | cursor 위치에서 insert mode 전환              |
| l       | cursor 왼쪽에 문자 삽입                       |
| a       | cursor 위치한 줄의 맨 끝에서 insert mode 전환 |
| A       | cursor 오른쪽에 문자 삽입                     |
| o       | cursor 있는 줄 아래에 빈 줄 삽입              |
| O       | cursor 있는 줄 위에 빈 줄 삽입                |
| R       | Replace mode 전환                             |

<br>

### Cursor 이동하기

| Command | Description               |
| ------- | ------------------------- |
| ^       | 줄의 처음으로 이동1       |
| 0       | 줄의 처음으로 이동2       |
| $       | 줄 끝으로 이동            |
| H       | 맨 위로 이동              |
| M       | 중간으로 이동             |
| L       | 맨 아래로 이동            |
| w       | 다음 단어 시작점으로 이동 |
| e       | 다음 단어 끝으로 이동     |
| b       | 이전 단어로 이동          |
