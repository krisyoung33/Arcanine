# Arcanine

A dual-pane file manager for Linux, built as a fork of [Nemo](https://github.com/linuxmint/nemo)
(the Linux Mint file manager). Designed for working with local folders and
rclone / FUSE mounts such as Google Drive.

![Arcanine icon](icons/arcanine-128.png)

> Arcanine is an independent fork. It is not affiliated with or endorsed by Linux Mint.

## What's different from stock Nemo

- **Stacked dual panes:** two file panes, one above the other (instead of side by side).
- **Preview panel:** a permanent column on the right. Click a single item to see:
  - images, scaled to fit
  - PDFs, rendered with Evince (scrollable, zoomable, selectable text)
  - plain text files (first part of the file, selectable)
  - a file-type icon for everything else
- **Downloads drop pane:** a small pane at the bottom of the left sidebar, locked to
  `~/Downloads`, so files can be dragged out into either main pane.
- **Default columns:** list view shows only `Name` and `Date Modified`.
- **Shortcuts:**

  | Key   | Action                          |
  |-------|---------------------------------|
  | F2    | Rename                          |
  | F7    | New folder                      |
  | Alt+M | Move to the inactive pane       |
  | Alt+C | Copy to the inactive pane       |

- **Icon fallback:** icon names with the `xsi-` prefix were changed to standard names,
  so toolbar and sidebar icons show on Debian 13, whose `xapp` package does not ship them.

## Status

First edition. Known rough edges:

- Sidebar width (target 180 px) and the 50/50 split between the file panes and the
  preview panel may need tuning on different screen sizes.
- Depends on `libevview3` (Evince). Debian is moving to Papers, so this dependency may
  need replacing in future.
- Tested only on Debian 13 (Trixie) with GNOME.

## Build and install (Debian 13)

```bash
sudo apt install git meson ninja-build build-essential libevince-dev
sudo apt build-dep nemo        # needs deb-src lines enabled in your apt sources

git clone https://github.com/krisyoung33/Arcanine.git
cd Arcanine
meson setup build --prefix=/usr/local
ninja -C build
sudo ninja -C build install
sudo glib-compile-schemas /usr/local/share/glib-2.0/schemas
```

Quit any running Nemo first (`nemo -q`), then launch `/usr/local/bin/nemo`.
It uses the same D-Bus name as stock Nemo, so only one can run at a time.

### Run from the build folder without installing

```bash
cd build
XDG_DATA_DIRS=/usr/share:/usr/local/share GSETTINGS_SCHEMA_DIR=custom-schemas ./src/nemo
```

## Icon

Icons are in `icons/` (SVG plus PNGs at 48, 64, 128, 256 and 512 px). Cyan `#8cd0d3`
filing cabinet on a transparent background.

## Licence

Arcanine inherits Nemo's licence, the GNU General Public License v2 or later. See the
`COPYING` files in this repository. Original Nemo copyright belongs to its authors
(Red Hat, Eazel and the Linux Mint team).
