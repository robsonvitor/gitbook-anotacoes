# Instalação Debian

* Instalação do sistema básico

> Seguir o instalador e na seleção de pacotes do tasksel, marcar somente "VER O NOME"

* Instalação de interface gráfica

> ```text
> apt install xserver-xorg gdm3 gnome-shell
> ```

* Instalação de pacotes para desenvolvimento

> ```text
> apt install build-essentials
> ```

* Instalação de pacotes úteis

> ```text
> apt install gnome-shell-pomodoro
> ```

* Extensões gnome-shell

| Extensão | Função | URL |
| :--- | :--- | :--- |
| No topleft hot corner | Desabilitar chamar o dash quando o mouse é colocado canto superior esquerdo | [https://extensions.gnome.org/extension/118/no-topleft-hot-corner/](https://extensions.gnome.org/extension/118/no-topleft-hot-corner/) |
| Simple Dock | Criar um Dock do Menu lateral | [https://extensions.gnome.org/extension/815/simple-dock/](https://extensions.gnome.org/extension/815/simple-dock/) |
| Top Icons Plus |  |  |
|  |  |  |

## Headset Bluetooth

```text
systemctl stop bluetooth.service
```

```text
apt install pulseaudio pulseaudio-module-bluetooth pavucontrol bluez-firmware blueman
```

In order to prevent GDM from capturing the A2DP sink on session start, edit /var/lib/gdm3/.config/pulse/client.conf \(or create it, if it doesn't exist\):

```text
autospawn = no
daemon-binary = /bin/true
```

After that you have to grant access to this file to Debian-gdm user:

```text
chown Debian-gdm:Debian-gdm /var/lib/gdm3/.config/pulse/client.conf
```

You will also need to disable pulseaudio startup:

```text
rm /var/lib/gdm3/.config/systemd/user/sockets.target.wants/pulseaudio.socket
```

In order to auto-connect a2dp for some devices, add this to /etc/pulse/default.pa:

```text
load-module module-switch-on-connect
```

Modify /etc/bluetooth/audio.conf to auto select A2DP profile \(instead of HSP/HFP\):

```text
[General]
Disable=Headset # Add this
```

Ajuste de permissão:

```text
setfacl -m u:Debian-gdm:r /usr/bin/pulseaudio
```

Reiniciar após a configuração.

draft:

Modify /etc/bluetooth/main.conf

```text
[General]
AutoConnect=true #add
MultiProfile = multiple #add
```

[https://wiki.debian.org/BluetoothUser/a2dp](https://wiki.debian.org/BluetoothUser/a2dp)

