# Install Sketchup2017 via wine sur LMDE2

Distro version

```
~ % cat /etc/linuxmint/info
RELEASE=2
CODENAME=betsy
EDITION="MATE 64-bit"
DESCRIPTION="LMDE 2 Betsy"
DESKTOP=MATE
TOOLKIT=GTK
GRUB_TITLE=LMDE 2 MATE 64-bit
```

## Install wine [1]

`sudo apt-get install --install-recommends winehq-devel`

## Install winetricks [2]

```
wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks
chmod +x winetricks
sudo mv winetricks /usr/local/bin
```

## Forces en présences

```
~ % wine --version ; winetricks --version
wine-2.19
20171018-next - sha256sum: e586dbf0ebdd7969b558e1e03372bfd7e735a98a33e95bdad32d831e6b2cc2db
```

## Download proprietary shit

[.NET Framework 4.5.2](https://www.microsoft.com/en-us/download/details.aspx?id=42642) (offline version)

`wget http://dl.trimble.com/sketchup/SketchUpMake-en-x64.exe`

## Get the job done

```
export WINEPREFIX=~/sketchup
export WINEARCH=win64
winetricks vcrun2015
winetricks corefonts

(Special DLL bonus install [3])

winetricks mfc40
winetricks settings win7
```

### .NET install

`wine start /unix NDP452-KB2901907-x86-x64-AllOS-ENU.exe`

### Sketchup install

Open _SketchUpMake-fr-x64.exe_ in Archive Manager and extract _SketchUp2017-x64.msi_

`wine start /unix SketchUp2017-x64.msi`

The installer will prompt you for the file path to save sketchup and for some reason it will default to the 32bit directory. Change it to `Program Files/` instead of `Program Files (x86)/`

## Launch Sketchup

`wine ~/sketchup/drive_c/Program Files/SketchUp/SketchUp 2017/SketchUp.exe`

## Desktop/Menu link

`env WINEPREFIX="/home/user/sketchup" wine /home/user/sketchup/drive_c/Program\ Files/SketchUp/SketchUp\ 2017/SketchUp.exe`

## Icône

`/home/user/.local/share/icons/hicolor/48x48/apps/6EBD_SketchUpIcon.0.png`
_ _ _

[1]: https://wiki.winehq.org/Debian "WineHQ - Installing WineHQ packages"
[2]: https://wiki.winehq.org/Winetricks#Getting_winetricks "WineHQ - Getting winetricks"
[3]: https://forum.ubuntu-fr.org/viewtopic.php?id=1967291 "Wine/winetricks/POL, pb avec installation librairie mfc40"

#### Ressources:

* [WineHQ - Sketchup 2017](https://appdb.winehq.org/objectManager.php?sClass=version&iId=34500)
* [WineHQ - Installing WineHQ packages](https://wiki.winehq.org/Debian)
* [WineHQ - Getting winetricks](https://wiki.winehq.org/Winetricks#Getting_winetricks)
* [Wine/winetricks/POL, pb avec installation librairie mfc40](https://forum.ubuntu-fr.org/viewtopic.php?id=1967291)
