# Ways to Free Up Space on Ubuntu

<br>

<br>

### 1. Clean the APT Cache (and do it regularly)

<br>

> Check how big your apt cache is

```bash
sudo du -sh /var/cache/apt/archives
```

<br>

> Clean the apt cache

```bash
sudo apt-get clean
```

<br><br>

### 2. Remove Old Kernels (if no longer required)

<br>

```bash
sudo apt-get autoremove --purge
```

<br><br>

### 3. Get rid of packages (if no longer required)

<br>

```bash
sudo apt-get autoremove
```

<br><br>

### 4. Clear systemd journal logs

<br>

> Check the log size

```bash
journalctl --disk-usage
```

<br>

> Clear the logs that are older than a certain days (3days in this example!!)

```bash
sudo journalctl --vacuum-time=3d
```

<br>

<br>

### 5.  Clean the thumbnail cache

- Ubuntu automatically creates a thumbnail, for viewing in the file manager.
- It stores those thumbnails in a hidden directory in your user account at the location ~/.cache/thumbnails.

<br>

> Check the size of thumbnail

```bash
du -sh ~/.cache/thumbnails
```

<br>

> Clear the thumbnail cache (every few months or so!)

```bash
rm -rf ~/.cache/thumbnails/*
```
