# user-systemd-template

The template to put a systemd service under user control

## systemd as user

Run the systemd as user.

Enable particular user to use systemd services `sudo loginctl enable-linger $USER`.

User units are stored in `~/.config/systemd/user` (or alternatives see below).

file: __backend.service__

```
[Unit]
Description=API backend service

[Service]
ExecStart=%h/mkt/backend.sh
WorkingDirectory=%h/mkt

[Install]
WantedBy=default.target
```

```bash
# quick start

mkdir -p ~/.config/systemd/user

sudo loginctl enable-linger $USER

mcedit ~/.config/systemd/user/backend.service

# systemctl --user ...

systemctl --user daemon-reload

systemctl --user start backend.service

systemctl --user enable backend.service

systemctl --user status backend.service
```