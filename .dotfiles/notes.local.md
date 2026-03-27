# Desktop Notes

## Selenite Lamp

```
sudo tee /etc/udev/rules.d/99-selenite-lamp.rules <<EOF
SUBSYSTEM=="tty", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", SYMLINK+="selenite-lamp", TAG+="systemd" RUN+="/bin/stty -F /dev/selenite-lamp -hupcl", ENV{SYSTEMD_DEVICE}="/dev/selenite-lamp"
EOF
sudo usermod -aG dialout $USER
systemctl --user enable selenite{,-update}.service
```
