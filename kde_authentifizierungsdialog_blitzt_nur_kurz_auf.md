1. Sockets deaktivieren und maskieren

Dadurch wird verhindert, dass systemd den Helper auf die fehlerhafte Art startet.
Bash

sudo systemctl stop polkit-agent-helper.socket
sudo systemctl disable polkit-agent-helper.socket
sudo systemctl mask polkit-agent-helper.socket

2. Service-Datei sichern

Da du die Datei jetzt gefunden hast (/usr/lib/systemd/system/polkit-agent-helper@.service), verschiebe sie, um den automatischen Start durch systemd komplett zu unterbinden:
Bash

sudo mv /usr/lib/systemd/system/polkit-agent-helper@.service /usr/lib/systemd/system/polkit-agent-helper@.service.bak

3. Systemd neu laden
Bash

sudo systemctl daemon-reload

4. Letzter Check: Setuid-Bit

Stelle sicher, dass der Helper jetzt wirklich die Rechte hat, die er ohne systemd braucht:
Bash

sudo chmod 4755 /usr/lib/polkit-1/polkit-agent-helper-1

Warum das hilft

Standardmäßig versucht Polkit unter neueren Arch-Konfigurationen, für jede Anfrage einen isolierten systemd-Dienst per Socket-Aktivierung zu spawnen. Die Fehlermeldung Pidfd not supported zeigt, dass dieser Prozess beim Erstellen des Dateideskriptors abstürzt. Durch das Deaktivieren (Maskieren) des Sockets und das Setzen des setuid-Bits nutzt der grafische KDE-Agent direkt das Hilfsprogramm, was den Fehler umgeht.
