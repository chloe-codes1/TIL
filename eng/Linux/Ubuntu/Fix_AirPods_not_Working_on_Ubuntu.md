# Fix AirPods not Working on Ubuntu

> I bought AirPods Pro!!!! But they wouldn't connect, so here's the solution I found after struggling

<br>

<br>

## 1. Change the `/etc/bluetooth/main.conf` file

<br>

### 1-1. Open a shell and type the following command

```bash
sudo vi /etc/bluetooth/main.conf
```

`main.conf`

<br>

### 1-2. Move to the last line and append the following in it

```bash
ControllerMode = bredr
```

<br>

<br>

## 2.  Restart the Bluetooth

<br>

```bash
sudo /etc/init.d/bluetooth restart
```

<br>

<br>

## 3.  DONE

![image-20200705165824130](../../kor/images/image-20200705165824130.png)

<br>

<br>

<br>

`+`

## Available commands

<br>

### turning on Bluetooth

```bash
sudo /etc/init.d/bluetooth start
```

or

```bash
systemctl start bluetooth
```

<br>

### for turning off Bluetooth

```bash
sudo /etc/init.d/bluetooth stop
```

or

```bash
systemctl stop bluetooth
```

<br>

### for restarting Bluetooth

``` bash
sudo /etc/init.d/bluetooth restart
```

or

```bash
systemctl restart bluetooth
```
