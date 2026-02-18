# Vim Commands Summary

> Vim is so cool....
>
> Reference: [keycdn.com](https://www.keycdn.com/blog/vim-commands), [velog.io/@recordboy](https://velog.io/@recordboy/VIM-%EB%AA%85%EB%A0%B9%EC%96%B4)

<br>

<br>

### Opening Files

| Command          | Description                             |
| ---------------- | --------------------------------------- |
| vi FILE          | Open a file                             |
| vi FILE_1 FILE_2 | Open two files sequentially             |
| view FILE        | Open in read-only mode (method 1)       |
| vi -R FILE       | Open in read-only mode (method 2)       |
| vi + FILE        | Open with cursor at the last line       |
| vi  +n FILE      | Open with cursor at line n              |
| vi -r FILE       | Recover a damaged file                  |

<br>

### Insert modes

| Command | Description                                      |
| ------- | ------------------------------------------------ |
| i       | Switch to insert mode at cursor position         |
| l       | Insert character to the left of cursor           |
| a       | Switch to insert mode at the end of cursor's line|
| A       | Insert character to the right of cursor          |
| o       | Insert a blank line below the cursor's line      |
| O       | Insert a blank line above the cursor's line      |
| R       | Switch to Replace mode                           |

<br>

### Moving the Cursor

| Command | Description                      |
| ------- | -------------------------------- |
| ^       | Move to the beginning of line (method 1) |
| 0       | Move to the beginning of line (method 2) |
| $       | Move to the end of line          |
| H       | Move to the top                  |
| M       | Move to the middle               |
| L       | Move to the bottom               |
| w       | Move to the start of next word   |
| e       | Move to the end of next word     |
| b       | Move to the previous word        |
