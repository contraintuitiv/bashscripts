Für den Automount brauchte es zwei Dinge, einen `/etc/fstab` Eintrag:

UUID herausfinden: `lsblk -lf /dev/sda`

```
UUID=6878DA3978DA062A   /mnt/Elements ntfs noauto,uid=1000,gid=1000,umask=022 0 0

```

Und einen automount service (filename muss `mnt-Elements` sein)

`/etc/systemd/system/mnt-external-elements.automount`

```
[Unit]
Description=Elements Externe Festplatte Automount

[Automount]
Where=/mnt/Elements
TimeoutIdleSec=10

[Install]
WantedBy=multi-user.target


```

enable start normal mit `systemctl`
