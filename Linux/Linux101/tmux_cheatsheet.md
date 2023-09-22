# tmux cheatsheet

> tmux 쓸꺼야!
>
> Reference: [tmux shotcuts & cheatsheet](https://gist.github.com/MohamedAlaa/2961058)

<br>

<br>

## What is tmux?

<br>

### tmux

- Terminal Multiplexer
- 하나의 terminal을 분할하여 여러 program을 실행하고, 실행한 program을 background mode로 전환 및 복귀할 수 있도록 한다

<br>

Linux shell을 사용할 때 겪는 아래와 같은 어려움을 tmux를 통해 해결할 수 있다

1. SSH Client shell의 sesion timeout
2. 하나의 ssh connection을 여러개의 shell에서 사용하고 싶음
3. Shell window를 switch 하는 것이 번거로움
4. Shell을 종료했다가 다시 실행 했을 때 이전의 작업들이 남아있었으면 좋겠음

<br>

### Key features

- 하나의 terminal window에서 다수의 windows와 pane을 사용하게 해준다
- windows와 pane이 session에 유지되도록 해준다
  - Internet이 disconnect 되어도 session이 유지될 수 있다!
- Session을 공유할 수 있다

<br>

### Sessions, Windows, and Panes

#### Sessions

- tmux를 실행하는 기본 단위로
- 여러 window로 구성된다
- 가상화된 하나의 console을 생성한 것으로 볼 수 있다

#### Windows

- terminal 화면
- session 내에서 tab 처럼 사용 가능하다

#### Panes

- 하나의 window 내에서의 화면 분할

<br>

<br>

## Essential tmux commands

<br>

start new session:

```bash
tmux
```

start new with session name:

```bash
tmux new -s SESSION_NAME
```

attach:

```bash
tmux a  #  (or at, or attach)
```

attach to named:

```bash
tmux a -t SESSION_NAME
```

list sessions:

```bash
tmux ls
```

exit tmux:

```bash
ctrl d
```

kill session:

```bash
tmux kill-session -t SESSION_NAME
```

Kill all the tmux sessions:

```bash
tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill
```

<br>

<br>

## Prefix & Shortcuts

<br>

### Prefix

- `.tmux.conf` 에서 따로 설정을 하지 않으면, default prefix는 `ctrl + b` 이다
- prefix 와 아래의 commands 를 조합하여 사용한다

<br>

#### prefix 변경하기

vi editor로 $HOME 경로에 ~/.tmux.conf file 열기

```bash
sudo vi ~/.tmux.conf
```

`.tmux.conf` 에 추가할 내용:

```bash
# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
```

변경된 `.tmux.conf` 적용:

```bash
tmux source-file ~/.tmux.conf
```

<br>

### Sessions

```bash
s  # list sessions
$  # name session
```

<br>

### Windows (tabs)

```bash
c  # create window
w  # list windows
n  # next window
p  # previous window
f  # find window
,  # name window
&  # kill window
```

<br>

### Panes (splits)

```bash
%  # vertical split
"  # horizontal split
o  # swap panes
q  # show pane numbers
x  # kill pane
+  # break pane into window (e.g. to select text by mouse to copy)
-  # restore pane from window
⍽  # space - toggle between layouts
q  # Show pane numbers, when the numbers show up type the key to goto that pane
{  # Move the current pane left
}  # Move the current pane right
z  # toggle pane zoom
```

<br>

### Misc

```bash
d  # detach
t  # big clock
?  # list shortcuts
:  # prompt
```
