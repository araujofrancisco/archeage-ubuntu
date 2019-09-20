# archeage-ubuntu
This document describes how to install/setup Wine on Ubuntu 18.04 (Bionic) to being able to run and play Archeage game. It assumes a fully patched ubuntu system running. This guide is mostly based on reddit post (https://www.reddit.com/r/archeage/comments/9c5jr7/archeage_on_linux_september_2018_without_steam/) with some fixes required to get this running in Ubuntu.

### Adding extra sources
```
wget -nc https://dl.winehq.org/wine-builds/winehq.key
sudo bash
apt-key add winehq.key
add-apt-repository https://dl.winehq.org/wine-builds/ubuntu
add-apt-repository ppa:cybermax-dexter/sdl2-backport
apt update
```

### Installation of 32-bit libraries, wine and support libraries
```
dpkg --add-architecture i386
apt install libasound2
apt install --install-recommends winehq-staging
apt install winetricks
apt install ttf-mscorefonts-installer
apt install winbind libntlm0
exit  # following steps do not require privileged user so exit
```  

### Install dxvk for improving graphics performance
```
mkdir ~/games
cd ~/games  
# In your browser, go to https://github.com/doitsujin/dxvk/releases/latest download the  
# dxvk-<latest-release>.tar.gz and unpack it into ~/games, alternatively you can download
# the version 1.3.4 that was the one tested while creating this document
wget https://github.com/doitsujin/dxvk/releases/download/v1.3.4/dxvk-1.3.4.tar.gz -O ~/Downloads/dxvk-1.3.4.tar.gz
```

### Create Windows installation
```
export WINEPREFIX=/home/user/games/Archeage   # *user* corresponds to your user login name
winetricks corefonts                          # if this is the first time it will ask you to install wine-mono (.NET 
                                              # Framework for Linux), also you will be asked to install Gecko package
winetricks directx9
if ! winetricks --force dxvk-1.3.4/setupdxvk.verb ; then dxvk-1.3.4/setup_dxvk.sh install ; fi
winecfg
```
When wine configuration windows opens change Windows Version to Windows 10.

### Install Archeage
```
# First you will need to obtain a copy of the Glyph client for Windows from https://glyph.trionworlds.com
# you can try next instruction to get the file, if it fails it probably got relocated
wget http://download.dyn.triongames.com/GlyphInstall-9999-1001.exe -O ~/Downloads/GlyphInstall-9999-1001.exe
wine ~/Downloads/GlyphInstall-9999-1001.exe
```
Install Glyph/Archeage using default location. Once Glyph installation completes is recommended to reboot, shortcut to Glyph should be now in the desktop, it will ask for trust confirmation on first execution.
