# Linux commands

## Sudo User

Create a sudo user that isn't root. 

```bash
su root
useradd -m -d /home/banjo banjo
usermod -aG sudo banjo
passwd banjo
su banjo
sudo usermod -s /bin/bash banjo
su banjo
cd ~
```

## Screen

Use screen to maintain a session even though you might be disconnected.

`screen`

To list all active directories: `screen -ls`

To connect to a directory: `screen -r 9432` (replace the number with the one you want to use)

To use settings, press `ctrl+a`.
* `d` to detach
* `q` close all but the active one

## IP settings

Get IP addresses by writing: `ifconfig`


