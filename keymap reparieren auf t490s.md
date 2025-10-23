Kopiere die Datei:
`sudo cp /usr/share/X11/xkb/symbols/de /usr/share/X11/xkb/symbols/de_custom`


dann diese Zeilen anpassen:

```

    key <AC02>	{[          s,          S,            bar,          U1E9E ]}; // ſ ẞ
    key <AB01>	{[          y,          Y,   less,          U203A ]}; // » ›
    key <AB02>	{[          x,          X,    greater,          U2039 ]}; // « ‹

```
(bar less greater auf AltGr gesetzt)

dann
`setxkbmap de_custom`


dauerhaft in
`sudo nano /etc/X11/xorg.conf.d/00-keyboard.conf`

`        Option "XkbLayout" "de_custom"`
