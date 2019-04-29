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

To create a named session: `screen -s name`

To use settings, press `ctrl+a`.
* `d` to detach
* `q` close all but the active one

## IP settings

Get IP addresses by writing: `ifconfig`

## Configure PLEX as localhost

The initial setup of Plex has to be done via an SSH tunnel, as the configuration is only allowed from localhost:

On Linux or MacOS computers, you can create the tunnel with the following command:

`ssh root@plex.server.ip -L 8888:localhost:32400`

On Windows computers, you can create the tunnel by using PuttY:

Open PuTTY, enter your server IP address in the hostname and SSH port. Or, if you already have your server session setup and saved, just load the existing session.
* Go to Connection > SSH > Tunnels.
* Fill in Source port as 8888 and Destination as localhost:32400.
* Click on the Add button.
* Navigate back to the session homepage now and click the Save button, then Open to connect to the server.
* Open a web browser on your local computer and navigate to http://localhost:8888/web.

## Update UBUNTU

* `sudo apt-get update        # Fetches the list of available updates`
* `sudo apt-get upgrade       # Strictly upgrades the current packages`
* `sudo apt-get dist-upgrade  # Installs updates (new ones)`
