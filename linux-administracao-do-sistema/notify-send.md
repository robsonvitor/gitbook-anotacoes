# notify-send

O comando notify-send faz parte do pacote libnotify-bin

Uso normal:

```text
notify-send 'Hora de almoçar!' 'Levante e corra para o RU' --icon=dialog-information
```

Enviar mensagem via cron:

```text
sudo -u X_user DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/X_userid/bus notify-send 'Acabou o dia!' 'Hora de ir para casa'
```

| Diretiva | Descrição |
| :--- | :--- |
| -u, --urgency=NIVEL | especifica o nível de urgência \(low, normal, critical\) |
| -t, --expire-time=TEMPO | especifica a duração, em milisegundos, em que a notificação aparecerá na tela |
| -i, --icon=ICON | especifica o nome do ícone a ser exibido na notificação. |
| -c, --category=TIPO\[,TIPO,...\] | especifica a categoria da notificação |

A diretiva -i busca os ícones disponíveis no diretório`/usr/share/icons/gnome/32x32` Neste diretório existem diversos subdiretórios: _actions, animations, apps, categories, devices, emblems, emotes, mimetypes, places, status_. Basta escolher o tipo de ícone a ser exibido na notificação.

Fonte: [http://www.dicas-l.com.br/arquivo/notify-send\_notificacoes\_no\_desktop.php\#.WlJZdXWnHiz](http://www.dicas-l.com.br/arquivo/notify-send_notificacoes_no_desktop.php#.WlJZdXWnHiz)

