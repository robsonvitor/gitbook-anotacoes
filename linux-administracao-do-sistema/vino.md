---
description: VNC Server
---

# Vino

#### Instalar

`sudo apt install vino`

~~`export DISPLAY=":0"`~~ 

`gsettings set org.gnome.Vino require-encryption false` 

`gsettings set org.gnome.Vino prompt-enabled false` 

`gsettings set org.gnome.Vino authentication-methods "['vnc']"` 

`gsettings set org.gnome.Vino vnc-password "$(echo -n "your_password" | base64)"`

dconf-editor: org-&gt;gnome-&gt;desktop-&gt;remote-access

sudo vi /etc/xdg/autostart/vino-server.desktop

`[Desktop Entry]   
Name=Desktop Sharing   
Comment=GNOME Desktop Sharing Server   
Keywords=vnc;share;remote;   
NoDisplay=true   
Exec=/usr/lib/vino/vino-server --sm-disable   
Icon=preferences-desktop-remote-desktop   
Terminal=false   
Type=Application   
X-GNOME-Autostart-Phase=Applications   
X-GNOME-AutoRestart=true   
X-GNOME-UsesNotifications=true   
X-Ubuntu-Gettext-Domain=vino`

