# Setting up XVnc
This will show you how to set up XVnc.
# Table of Contents
- [Setting up XVnc](#setting-up-xvnc)
- [Table of Contents](#table-of-contents)
- [Installation](#installation)
  - [VNC (server)](#vnc-server)
  - [VNC (client)](#vnc-client)
    - [Windows](#windows)
    - [MacOS](#macos)
    - [Linux](#linux)
- [Configuration](#configuration)
- [Connecting](#connecting)
- [Scripting](#scripting)

# Installation
## VNC (server)
Install `tightvncserver`:
```bash
sudo apt install tightvncserver -y
```
## VNC (client)
### Windows
Download the Viewer from [here](https://www.realvnc.com/en/connect/download/viewer/), and run it.  
### MacOS
Download the Viewer from [here](https://www.realvnc.com/en/connect/download/viewer/), and open the DMG.  
Move the `RealVNC.app` to `/Applications`.
### Linux
Install `xtightvncviewer`:
```bash
sudo apt install xtightvncviewer -y 
```
# Configuration
Run the `vncserver` command, and enter your password when prompted.
```bash
vncserver -geometry 1280x720 -depth 24
```
The resolution `1280x720` can be what you want.
# Connecting
First, get the IP of your server (or WSL VM) by using `ip addr`:
```bash
ip addr
```
The IP address will be one of the last lines. You can connect to that in your VNC client.
# Scripting
Make a script, so it would be easier to launch XVnc.
```bash
#!/bin/bash
OPTS="-geometry 1280x720 -depth 24"
# Kill the VNC server
vncserver -kill :1
# Relaunch the VNC server with options as $OPTS
vncserver $OPTS
export DISPLAY=:1
# Launch dbus as a daemon
dbus-daemon --session
# Launch graphical environment (for later tutorials)
# Go in a loop forever to prevent closing
while true; do sleep 1; done
```
