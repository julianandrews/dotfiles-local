# Dotfiles-local

## Page Status

Edit `/etc/page-status/config.toml`:

```
[pages]

  [pages.jellyfin]
  url = "https://jellyfin.seemyvest.net/web/"
  method = "Head"
  poll-interval = 10

  [pages.apt]
  url = "https://apt.seemyvest.net"
  method = "Head"
  poll-interval = 10
```

```
sudo systemctl restart page-status.service
```
