# Desktop Notes

## Selenite Lamp

```
sudo tee /etc/udev/rules.d/99-selenite-lamp.rules <<EOF
SUBSYSTEM=="tty", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", SYMLINK+="selenite-lamp", TAG+="systemd" RUN+="/bin/stty -F /dev/selenite-lamp -hupcl", ENV{SYSTEMD_DEVICE}="/dev/selenite-lamp"
EOF
sudo usermod -aG dialout $USER
systemctl --user enable selenite{,-update}.service
```

## Rustic backups

```
curl -sSL "https://github.com/rustic-rs/rustic/releases/latest/download/rustic-$(curl -sSL https://api.github.com/repos/rustic-rs/rustic/releases/latest | jq -r .tag_name)-x86_64-unknown-linux-gnu.tar.gz" | tar -xzf - -C ~/.local/bin
rclone config
systemctl --user enable --now rustic.timer
```
