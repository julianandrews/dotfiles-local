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
curl -sSL "https://github.com/rustic-rs/rustic/releases/latest/download/rustic-$(curl -sSL https://api.github.com/repos/rustic-rs/rustic/releases/latest | jq -r .tag_name)-x86_64-unknown-linux-gnu.tar.gz" | tar -xzf - -C ~/.local/bin rustic

# Log into backblaze and get application keys ready for both the main backup and passwords buckets
# Configure rclone (~/.config/rclone/rclone.conf) with both keys
pass show madagascar/rustic/password | systemd-creds encrypt --user --name=rustic-password - ~/.config/credstore.encrypted/rustic-password.cred
systemctl --user enable --now rustic-main.timer
systemctl --user enable --now rustic-main-prune.timer
systemctl --user enable --now rustic-gargantua-two.timer
systemctl --user enable --now rustic-gargantua-two-prune.timer
systemctl --user enable --now rustic-passwords-two.timer
systemctl --user enable --now rustic-passwords-two-prune.timer
```
