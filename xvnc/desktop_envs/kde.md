# Configuring KDE for XVNC
This will show you how to add KDE to your `xvnc` script.
## Warning
Guide is a WIP, it doesn't work yet, tested on a WSL vm.
# Table of Contents
- [Configuring KDE for XVNC](#configuring-kde-for-xvnc)
  - [Warning](#warning)
- [Table of Contents](#table-of-contents)
- [Installing KDE](#installing-kde)
- [Adding KDE Support](#adding-kde-support)
# Installing KDE
On Ubuntu, install `kubuntu-desktop`:
```bash
sudo apt install kubuntu-desktop -y
```
# Adding KDE Support
Open your XVNC script in your favorite text editor.
Go to the line that says `# Launch graphical environment (for later tutorials)`.
Add the following lines:
```bash
dbus-launch startplasma-x11 &
sleep 3s
kwin --replace
```