# Settings for XDG user dirs

<br>

<br>

### $HOME/.config/user-dirs.dirs file

- Text file that contains the **user-specific values** for the XDG user dirs
- It is created and updated by the `xdg-user-dirs-update` command.

<br>

### Open `user-dirs.dir`

> Terminal

```bash
gedit ~/.config/user-dirs.dirs
```

<br>

> .config > user-dirs.dirs

```
XDG_DESKTOP_DIR="$HOME/Desktop"

XDG_DOWNLOAD_DIR="$HOME/Downloads"

XDG_TEMPLATES_DIR="$HOME/"

XDG_PUBLICSHARE_DIR="$HOME/Share"

XDG_DOCUMENTS_DIR="$HOME/Documents"

XDG_MUSIC_DIR="$HOME/Music"

XDG_PICTURES_DIR="$HOME/Pictures"

XDG_VIDEOS_DIR="$HOME/Videos"
```

<br>

### Restart `nautilus` without logging out

```bash
killall nautilus

nautilus -q
```

- Both of them works!

<br>

`+`

### **nautilus**

: a file manager, designed for the GNOME 3 desktop.
