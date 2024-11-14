---
id: kitty
aliases: []
tags:
  - linux
  - macOS
  - terminal
---

# Kitty

Terminal emulator multiplatform.

## Installation

> Reference: [Binary Install](https://sw.kovidgoyal.net/kitty/binary/#binary-install)

### macOS

```bash
brew install --cask kitty
```

### Linux

```bash
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

> [!WARNING]
> By default, kitty won't appear in the applications list. To fix this, run the following command:
>
> ```bash
> # Create symbolic links to add kitty and kitten to PATH (assuming ~/.local/bin is in
> # your system-wide PATH)
> ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/
> # Place the kitty.desktop file somewhere it can be found by the OS
> cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
> # If you want to open text files and images in kitty via your file manager also add the kitty-open.desktop file
> cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
> # Update the paths to the kitty and its icon in the kitty desktop file(s)
> sed -i "s|Icon=kitty|Icon=$(readlink -f ~)/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty*.desktop
> sed -i "s|Exec=kitty|Exec=$(readlink -f ~)/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
> # Make xdg-terminal-exec (and hence desktop environments that support it use kitty)
> echo 'kitty.desktop' > ~/.config/xdg-terminals.list
> ```

## Configuration

The configuration directory is located at `~/.config/kitty`.

```bash
├── kitty.conf # config file
└── tab_bar.py # tab bar theme
```

### `kitty.conf`:

```bash
# ⚙️  Non-default settings:
# =============================================================================
# 👀 UI: {{{

# Font
font_family                 Maple Mono NF
bold_font                   auto
italic_font                 auto
bold_italic_font            auto
font_size                   13.0
font_features               MapleMonoNF-Regular +cv01 +cv02 +cv03 +cv04 +ss01 +ss02 +ss03 +ss04 +ss05

# Cursor
box_drawing_scale           0.00125, 1.25, 1.875, 2.5
cursor_beam_thickness       1.875
cursor_underline_thickness  2.5
mouse_hide_wait             1.0

# Window
hide_window_decorations     titlebar-only # macOS
# hide_window_decorations     yes # Ubuntu

# Tab
tab_bar_style               powerline
tab_powerline_style         slanted
tab_bar_edge                top
tab_bar_align               left
tab_bar_margin_width        0.0
tab_bar_margin_height       0.0 0.0
tab_bar_min_tabs            1
tab_title_template          {title}{' :{}:'.format(num_windows) if num_windows > 1 else ''}
# tab_title_template          "{f'{title[:30]}…' if title.rindex(title[-1]) + 1 > 30 else (title.center(6) if (title.rindex(title[-1]) + 1) % 2 == 0 else title.center(5))}{' :{}:'.format(num_windows) if num_windows > 1 else ''}"
bell_on_tab                 false
tab_separator               ""
tab_activity_symbol         none
active_tab_font_style       normal
allow_remote_control        yes

# fix nerd font mappings
# symbol_map                  U+23FB-U+23FE,U+2665,U+26A1,U+2B58,U+E000-U+E00A,U+E0A0-U+E0A3,U+E0B0-U+E0 Symbols Nerd Font

# URL
undercurl_style             thick-sparse

# https://sw.kovidgoyal.net/kitty/overview/#layouts
enabled_layouts             fat:bias=75,tall:bias=60,fat:bias=25
window_border_width         1px
window_margin_width         4
single_window_margin_width  0
placement_strategy          center

# }}}

# =============================================================================
# 🎨 UX: {{{

macos_quit_when_last_window_closed    yes
macos_menubar_title_max_length        50
macos_option_as_alt                   left

# }}}
# ============================================================================

# 🎨 Color scheme: {{{

# basics
foreground                  #CDD6F4
background                  #1E1E2E
selection_foreground        #1E1E2E
selection_background        #F5E0DC

# cursor
cursor                      #F5E0DC
cursor_text_color           #1E1E2E

# URL underline when hovering with mouse
url_color                   #F5E0DC

# kitty window border
active_border_color         #B4BEFE
inactive_border_color       #6C7086
bell_border_color           #F9E2AF

# OS window titlebar
wayland_titlebar_color      system
macos_titlebar_color        system

# tab bar
active_tab_foreground       #11111B
active_tab_background       #CBA6F7
inactive_tab_foreground     #CDD6F4
inactive_tab_background     #181825
tab_bar_background          #11111B

# Colors for marks (marked text in the terminal)
mark1_foreground            #1E1E2E
mark1_background            #B4BEFE
mark2_foreground            #1E1E2E
mark2_background            #CBA6F7
mark3_foreground            #1E1E2E
mark3_background            #74C7EC

# The 16 terminal colors

# black
color0                      #45475A
color8                      #585B70

# red
color1                      #F38BA8
color9                      #F38BA8

# green
color2                      #A6E3A1
color10                     #A6E3A1

# yellow
color3                      #F9E2AF
color11                     #F9E2AF

# blue
color4                      #89B4FA
color12                     #89B4FA

# magenta
color5                      #F5C2E7
color13                     #F5C2E7

# cyan
color6                      #94E2D5
color14                     #94E2D5

# white
color7                      #BAC2DE
color15                     #A6ADC8

#: }}}
# =============================================================================

# ⌨️  Keymaps:
# =============================================================================
# 📑 Tabs: {{{

map kitty_mod+1             goto_tab 1
map kitty_mod+2             goto_tab 2
map kitty_mod+3             goto_tab 3

#: }}}
# =============================================================================
```

### `tab_bar.py`:

```python
# pyright: reportMissingImports=false
from datetime import datetime

from kitty.boss import get_boss
from kitty.fast_data_types import Screen, add_timer, get_options
from kitty.tab_bar import (
    DrawData,
    ExtraData,
    Formatter,
    TabBarData,
    as_rgb,
    draw_attributed_string,
    draw_title,
)
from kitty.utils import color_as_int

opts = get_options()
icon_fg = as_rgb(color_as_int(opts.color183))
icon_bg = as_rgb(color_as_int(opts.color0))
bat_text_color = as_rgb(color_as_int(opts.color15))
clock_color = as_rgb(color_as_int(opts.color15))
date_color = as_rgb(color_as_int(opts.color8))
SEPARATOR_SYMBOL, SOFT_SEPARATOR_SYMBOL = ("", "")
RIGHT_MARGIN = 1
REFRESH_TIME = 1
ICON = "  "  #  󰈸    󰅟
UNPLUGGED_ICONS = {
    10: "",
    20: "",
    30: "",
    40: "",
    50: "",
    60: "",
    70: "",
    80: "",
    90: "",
    100: "",
}
PLUGGED_ICONS = {
    1: "",
}
UNPLUGGED_COLORS = {
    15: as_rgb(color_as_int(opts.color1)),
    16: as_rgb(color_as_int(opts.color15)),
}
PLUGGED_COLORS = {
    15: as_rgb(color_as_int(opts.color1)),
    16: as_rgb(color_as_int(opts.color6)),
    99: as_rgb(color_as_int(opts.color6)),
    100: as_rgb(color_as_int(opts.color2)),
}


def _draw_icon(screen: Screen, index: int) -> int:
    if index != 1:
        return 0
    fg, bg = screen.cursor.fg, screen.cursor.bg
    screen.cursor.fg = icon_fg
    screen.cursor.bg = icon_bg
    screen.draw(ICON)
    screen.cursor.fg, screen.cursor.bg = fg, bg
    screen.cursor.x = len(ICON)
    return screen.cursor.x


def _draw_left_status(
    draw_data: DrawData,
    screen: Screen,
    tab: TabBarData,
    before: int,
    max_title_length: int,
    index: int,
    is_last: bool,
    extra_data: ExtraData,
) -> int:
    if screen.cursor.x >= screen.columns - right_status_length:
        return screen.cursor.x
    tab_bg = screen.cursor.bg
    tab_fg = screen.cursor.fg
    default_bg = as_rgb(int(draw_data.default_bg))
    if extra_data.next_tab:
        next_tab_bg = as_rgb(draw_data.tab_bg(extra_data.next_tab))
        needs_soft_separator = next_tab_bg == tab_bg
    else:
        next_tab_bg = default_bg
        needs_soft_separator = False
    if screen.cursor.x <= len(ICON):
        screen.cursor.x = len(ICON)
    screen.draw(" ")
    screen.cursor.bg = tab_bg
    draw_title(draw_data, screen, tab, index)
    if not needs_soft_separator:
        screen.draw(" ")
        screen.cursor.fg = tab_bg
        screen.cursor.bg = next_tab_bg
        screen.draw(SEPARATOR_SYMBOL)
    else:
        prev_fg = screen.cursor.fg
        if tab_bg == tab_fg:
            screen.cursor.fg = default_bg
        elif tab_bg != default_bg:
            c1 = draw_data.inactive_bg.contrast(draw_data.default_bg)
            c2 = draw_data.inactive_bg.contrast(draw_data.inactive_fg)
            if c1 < c2:
                screen.cursor.fg = default_bg
        screen.draw(" " + SOFT_SEPARATOR_SYMBOL)
        screen.cursor.fg = prev_fg
    end = screen.cursor.x
    return end


def _draw_right_status(screen: Screen, is_last: bool, cells: list) -> int:
    if not is_last:
        return 0
    draw_attributed_string(Formatter.reset, screen)
    screen.cursor.x = screen.columns - right_status_length
    screen.cursor.fg = 0
    for color, status in cells:
        screen.cursor.fg = color
        screen.draw(status)
    screen.cursor.bg = 0
    return screen.cursor.x


def _redraw_tab_bar(_):
    tm = get_boss().active_tab_manager
    if tm is not None:
        tm.mark_tab_bar_dirty()


def get_battery_cells() -> list:
    try:
        with open("/sys/class/power_supply/BAT0/status", "r") as f:
            status = f.read()
        with open("/sys/class/power_supply/BAT0/capacity", "r") as f:
            percent = int(f.read())
        if status == "Discharging\n":
            # TODO: declare the lambda once and don't repeat the code
            icon_color = UNPLUGGED_COLORS[
                min(UNPLUGGED_COLORS.keys(), key=lambda x: abs(x - percent))
            ]
            icon = UNPLUGGED_ICONS[
                min(UNPLUGGED_ICONS.keys(), key=lambda x: abs(x - percent))
            ]
        elif status == "Not charging\n":
            icon_color = UNPLUGGED_COLORS[
                min(UNPLUGGED_COLORS.keys(), key=lambda x: abs(x - percent))
            ]
            icon = PLUGGED_ICONS[
                min(PLUGGED_ICONS.keys(), key=lambda x: abs(x - percent))
            ]
        else:
            icon_color = PLUGGED_COLORS[
                min(PLUGGED_COLORS.keys(), key=lambda x: abs(x - percent))
            ]
            icon = PLUGGED_ICONS[
                min(PLUGGED_ICONS.keys(), key=lambda x: abs(x - percent))
            ]
        percent_cell = (bat_text_color, str(percent) + "% ")
        icon_cell = (icon_color, icon)
        return [percent_cell, icon_cell]
    except FileNotFoundError:
        return []


timer_id = None
right_status_length = -1


def draw_tab(
    draw_data: DrawData,
    screen: Screen,
    tab: TabBarData,
    before: int,
    max_title_length: int,
    index: int,
    is_last: bool,
    extra_data: ExtraData,
) -> int:
    global timer_id
    global right_status_length
    if timer_id is None:
        timer_id = add_timer(_redraw_tab_bar, REFRESH_TIME, True)
    clock = datetime.now().strftime(" %H:%M")
    date = datetime.now().strftime(" %d.%m.%Y")
    cells = get_battery_cells()
    cells.append((clock_color, clock))
    cells.append((date_color, date))
    right_status_length = RIGHT_MARGIN
    for cell in cells:
        right_status_length += len(str(cell[1]))

    _draw_icon(screen, index)
    _draw_left_status(
        draw_data,
        screen,
        tab,
        before,
        max_title_length,
        index,
        is_last,
        extra_data,
    )
    _draw_right_status(
        screen,
        is_last,
        cells,
    )
    return screen.cursor.x
```
