# tmux cheatsheet

> Let's use tmux!
>
> Reference: [tmux shotcuts & cheatsheet](https://gist.github.com/MohamedAlaa/2961058)

<br>

<br>

## What is tmux?

<br>

### tmux

- Terminal Multiplexer
- Allows you to split a single terminal to run multiple programs, and switch running programs to background mode and back

<br>

tmux can help resolve the following difficulties encountered when using a Linux shell:

1. SSH Client shell session timeout
2. Wanting to use one SSH connection across multiple shells
3. Switching between shell windows is cumbersome
4. Wanting previous work to remain when you close and reopen the shell

<br>

### Key features

- Allows using multiple windows and panes in a single terminal window
- Keeps windows and panes maintained in a session
  - Sessions can persist even if the Internet disconnects!
- Sessions can be shared

<br>

### Sessions, Windows, and Panes

#### Sessions

- The basic unit for running tmux
- Composed of multiple windows
- Can be thought of as creating a single virtualized console

#### Windows

- A terminal screen
- Can be used like tabs within a session

#### Panes

- Screen splits within a single window

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

- If no separate settings are configured in `.tmux.conf`, the default prefix is `ctrl + b`
- Combine the prefix with the commands below to use them

<br>

#### Changing the prefix

Open the ~/.tmux.conf file at the $HOME path with vi editor

```bash
sudo vi ~/.tmux.conf
```

Content to add to `.tmux.conf`:

```bash
# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
```

Apply the modified `.tmux.conf`:

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
