# dotfiles

My Hyprland/Arch desktop setup. Clone this on a fresh install to get the same look and feel back.

## Prerequisites

Packages this config depends on:

- `hyprland`
- `waybar`
- `hyprpaper`
- `dunst`
- `nwg-look` (GTK theme switcher GUI)
- `catppuccin-gtk-theme-mocha` (AUR) — GTK theme, applied via `nwg-look`
- [SilentSDDM](https://github.com/uiriansan/SilentSDDM) (AUR: `sddm-theme-silent-git` or similar) — login screen theme

## Setup on a new machine

1. Clone this repo:
   ```
   git clone git@github.com:<your-username>/dotfiles.git ~/code/dotFiles
   ```

2. Symlink the configs into place:
   ```
   ln -sf ~/code/dotFiles/config/hypr ~/.config/hypr
   ln -sf ~/code/dotFiles/config/waybar ~/.config/waybar
   ln -sf ~/code/dotFiles/config/dunst ~/.config/dunst
   ```

3. Copy the wallpapers:
   ```
   mkdir -p ~/wallpapers
   cp ~/code/dotFiles/wallpapers/*.png ~/wallpapers/
   ```

4. Install the SDDM login theme, then apply the saved config and background:
   ```
   sudo cp ~/code/dotFiles/sddm/default.conf /usr/share/sddm/themes/silent/configs/default.conf
   sudo cp ~/code/dotFiles/wallpapers/cats.png /usr/share/sddm/themes/silent/backgrounds/
   ```

5. Set the GTK theme with `nwg-look` (select `catppuccin-mocha-green-standard` under GTK theme).

6. Reload everything:
   ```
   hyprctl reload
   killall hyprpaper && hyprpaper &
   pkill waybar && hyprctl dispatch exec waybar
   ```

## Notes / cheatsheet

### Hyprland — borders & gaps
`config/hypr/hyprland.conf`
```
general {
    gaps_in = 2
    gaps_out = 2
    border_size = 0

    col.active_border = 0xFF6A8C50
    col.inactive_border = 0xFF1B2A1E
}
```

### Waybar — top bar
`config/waybar/style.css`, `config/waybar/config`

Reload after edits:
```
pkill waybar && hyprctl dispatch exec waybar
# or, keeping the console open:
pkill waybar
waybar &
```

### GTK theme (apps)
```
nwg-look
```

### Background (desktop wallpaper)
`config/hypr/hyprpaper.conf`

Reload after edits:
```
killall hyprpaper && hyprpaper &
```

### Lock screen (SDDM)
Theme config: `sddm/default.conf` → `/usr/share/sddm/themes/silent/configs/default.conf`

To change the background image:
```
sudo cp ~/wallpapers/<name> /usr/share/sddm/themes/silent/backgrounds/
sudo sed -i '58s/".*"/"newimage.png"/' /usr/share/sddm/themes/silent/configs/default.conf
```

### Notifications
`config/dunst/dunstrc`

## Wallpapers

- `wallpapers/garden.png` — current desktop background
- `wallpapers/cats.png` — current lock screen background
