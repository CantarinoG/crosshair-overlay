# crosshair-overlay

A tiny click-through crosshair overlay for Wayland, written in Python with GTK4 and
[gtk4-layer-shell](https://github.com/wmww/gtk4-layer-shell).

- Drawn on the layer-shell **overlay** layer, so it stays above fullscreen games
- Mouse clicks pass through it and it never takes keyboard focus
- Doesn't hook into the game, so there's nothing for anti-cheat to detect
- One command to toggle on/off, easy to bind to a key

Works on compositors that support `wlr-layer-shell` (Sway, Hyprland, river, KDE Plasma, …).
It does **not** work on GNOME, or on X11.

## Install

Debian / Ubuntu:

```sh
sudo apt install python3-gi python3-gi-cairo gir1.2-gtk-4.0 gir1.2-gtk4layershell-1.0
```

Arch: `sudo pacman -S python-gobject python-cairo gtk4 gtk4-layer-shell`

Then put the script on your `PATH`:

```sh
git clone https://github.com/CantarinoG/crosshair-overlay.git
ln -s "$PWD/crosshair-overlay/crosshair" ~/.local/bin/crosshair
```

## Usage

```sh
crosshair            # show it (Ctrl+C or SIGTERM to close)
crosshair --toggle   # show it, or close it if it's already running
crosshair --help     # all options
```

### Keybind

Sway (`~/.config/sway/config`):

```
bindsym $mod+x exec ~/.local/bin/crosshair --toggle
```

Hyprland (`~/.config/hypr/hyprland.conf`):

```
bind = SUPER, X, exec, ~/.local/bin/crosshair --toggle
```

## Options

| Option | Default | Description |
|---|---|---|
| `--style` | `cross` | `cross`, `dot`, `circle`, `cross-dot`, `t` |
| `--length` | `8` | Arm length (px) |
| `--gap` | `4` | Gap from the center to the arms (px) |
| `--thickness` | `2` | Line thickness (px) |
| `--dot` | `2` | Center dot radius (px) |
| `--radius` | `10` | Circle radius (px) |
| `--color` | `00ff00` | `RRGGBB` or `RRGGBBAA` (the last two digits set transparency) |
| `--outline` | `1` | Outline width (px), `0` turns it off |
| `--outline-color` | `000000` | Outline color |
| `--offset-x` / `--offset-y` | `0` | Move it away from the center (px) |
| `--output` | focused | Monitor name, e.g. `eDP-1`, `DP-1` |

Example:

```sh
crosshair --toggle --style cross-dot --color ff00ffcc --gap 3 --length 6
```

## Limitations

- When a game runs in a standalone gamescope session (e.g. Steam Deck gaming mode),
  the crosshair isn't shown there. Gamescope running as a nested window on your desktop works fine.

## License

MIT
