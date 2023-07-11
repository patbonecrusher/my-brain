---
creation date: 2023-06-12 16:16
modification date: Monday, 12th June 2023, 16:16:55
tags: today_i_leaned
---

# How to setup VNC on a Ubuntu box

```shell
# Install VNC server
sudo apt update
sudo apt install vino

#  Enable the VNC server to start each time you log in
mkdir -p ~/.config/autostart
cp /usr/share/applications/vino-server.desktop ~/.config/autostart

# Configure the VNC server
gsettings set org.gnome.Vino prompt-enabled false
gsettings set org.gnome.Vino require-encryption false

# Set a password to access the VNC server
# Replace thepassword with your desired password 
gsettings set org.gnome.Vino authentication-methods "['vnc']"
gsettings set org.gnome.Vino vnc-password $(echo -n 'thepassword'|base64) 

# Modify /etc/gdm3/custom.conf to contain:
WaylandEnable=false
DefaultSession=gnome-xorg.desktop

# Reboot the system so that the settings take effect
sudo reboot
```
