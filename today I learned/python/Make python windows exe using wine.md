---
creation date: 2024-02-28 21:12
modification date: Wednesday, 28th February 2024, 21:12:49
tags:
  - today_i_learned
  - computer/language/python
  - engineering/coding/python
---
```
# Setup apt to have the wine source repo
sudo apt update
sudo mkdir -pm755 /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
sudo apt update

# Install wine
sudo DEBIAN_FRONTEND="noninteractive" apt install --install-recommends winehq-stable -y
sudo wget -nv -O /usr/bin/winetricks https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks
sudo chmod +x /usr/bin/winetricks

# Configure win10, this downloads .net and other required things.
# This will prompt a UI make sure you have X forward over ssh setup if doing over ssh
winetricks -q win10

# Test wine install
wine notepad

# Get and install python
wget -NP $HOME https://www.python.org/ftp/python/3.10.7/python-3.10.7-amd64.exe
wine $HOME/python-3.10.7-amd64.exe 
wine $(find $HOME/.wine -iname pip.exe) install pyinstaller

# Cd in your repo
wine $(find $HOME/.wine -iname pip.exe) install .
wine ${HOME}/.wine/drive_c/users/winehq/AppData/Local/Programs/Python/Python310/python.exe -m PyInstaller --onefile --hidden-import=configparser -n desired_exe_name app\\__main__.py

# If all goes well, you will have the exe in the dist folder.
ls dist
wine dist/desired_exe_name.exe

```