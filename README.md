# Qutebrowser Sync

Bidirectional sync for [qutebrowser](https://github.com/qutebrowser/qutebrowser) bookmarks, quickmarks, and browsing history across multiple machines.

## Features

- **Bookmarks & quickmarks sync** — bidirectional merge, deduplicates by URL/key
- **Live history sync** — SQLite merge works in real-time, no browser restart needed
- **Any storage backend** — NFS, SSHFS, Syncthing, Dropbox, Google Drive (rclone), NAS, USB drives
- **Multi-machine, multi-profile** — seamlessly sync between desktop, laptop, work, home
- **Zero dependencies** — pure Python stdlib, single file, just works

## Dependencies

Python 3.6+ (stdlib only, no pip packages required)

## Installation

```bash
curl -o ~/.local/bin/qutebrowser-sync https://raw.githubusercontent.com/wh1le/qutebrowser-sync/main/qutebrowser-sync
chmod +x ~/.local/bin/qutebrowser-sync
```

## Usage

```bash
qutebrowser-sync --remote /mnt/nas/browser-data
qutebrowser-sync --remote /mnt/syncthing --profile work
qutebrowser-sync --remote /mnt/sshfs/server --no-history
```

## Options

| Flag           | Description                                   |
| -------------- | --------------------------------------------- |
| `--remote`     | Path to mounted remote directory (required)   |
| `--profile`    | Qutebrowser profile name (default: `default`) |
| `--home`       | Override home directory                       |
| `--no-history` | Skip history sync                             |

## How it works

1. Checks if remote is mounted (looks for `qutebrowser/` dir)
2. Merges local ↔ remote bookmarks/quickmarks (union, deduplicated)
3. Merges SQLite history both directions (by url+timestamp)

## Automation

```bash
# cron (every 30 min)
*/30 * * * * /home/user/.local/bin/qutebrowser-sync --remote /mnt/nas/browser
# systemd timer, or hook into qutebrowser quit
```

## TODO

- add more flexible support for different profiles

## License

[MIT](LICENSE)
