ProtonMail offers bridge for desktop client, but they're currently only available for paid users, we can however use a free alternative called [hydroxide](https://github.com/emersion/hydroxide) that does the same, but  requires some manual input in cli and doesnt have a systemd service or docker
## TODO 
create a docker image for hydroxide


##Service
```ini
[Unit]
Description=Third party ProtonMail IMAP Bridge
After=network.target

[Service]
Type=exec
User=hydroxide
Group=hydroxide
Restart=on-failure
ExecStart=/usr/bin/hydroxide -smtp-host (ip) -imap-host (10.9.4.1) -disable-carddav serve

ProtectHome=true
ProtectSystem=full
PrivateDevices=true
NoNewPrivileges=true
PrivateTmp=true
InaccessibleDirectories=/root /sys /srv -/opt /media -/lost+found
ReadWriteDirectories=/var/lib/hydroxide
WorkingDirectory=/var/lib/hydroxide

[Install]
WantedBy=multi-user.target
```
or 
```ini
[Unit]
Description=Hydroxide (Protonmail proxy) service

[Service]
ExecStart=/usr/bin/local/hydroxide serve
Type=simple
Restart=always
RestartSec=30

[Install]
WantedBy=default.target
```
