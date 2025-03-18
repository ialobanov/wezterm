# WezTerm Configuration

## Windows

```powershell
winget install --id wez.wezterm -e --source winget
```

```ps1
vim .wezterm.lua
```

```lua
-- Core setting
local wezterm = require 'wezterm'
local mux = wezterm.mux
local config = {}

-- Set PowerShell as the default shell
config.default_prog = { 'pwsh', '-NoLogo' }

-- Maximaze on start up
wezterm.on('gui-startup', function()
  local tab, pane, window = mux.spawn_window {}
  window:gui_window():maximize()
end)

-- Set window paddings
config.window_padding = {
  left = 20,
  right = 22,
  top = 16,
  bottom = 6,
}

-- Hide OS panel and disable confirmation for close terminal
config.window_decorations = "INTEGRATED_BUTTONS|RESIZE"
config.window_close_confirmation = 'NeverPrompt'

-- For right paste in different terminals
config.canonicalize_pasted_newlines = "CarriageReturnAndLineFeed"

-- Font settings
config.font = wezterm.font 'JetBrainsMono Nerd Font Mono'
config.font_size = 22.0

-- WezTerm color theme
config.color_scheme = 'rebecca'
config.color_schemes = {
  ['rebecca'] = {
    ansi = {
     "#12131e",
     "#dd7755",
     "#04dbb5",
     "#FFC300",
     "#7aa5ff",
     "#bf9cf9",
     "#56d3c2",
     "#e4e3e9",
     },
     background = "#292a44",
     brights = {
      "#666699",
      "#ff92cd",
      "#01eac0",
      "#FFC300",
      "#69c0fa",
      "#c17ff8",
      "#8bfde1",
      "#f4f2f9",
     },
     cursor_bg = "#D155B1",
     cursor_border = "#D155B1",
     cursor_fg = "#292a44",
     foreground = "#e8e6ed",
     indexed = {},
     selection_bg = "#663399",
     selection_fg = "#f4f2f9",
     scrollbar_thumb = 'FFC300',
    },
}

-- Disable audio notifications
config.audible_bell = 'Disabled'

-- Keymaps
-- Select text with the left mouse button and paste with a right-click
config.mouse_bindings = {
  {
    event = { Up = { streak = 1, button = 'Left' } },
    mods = 'NONE',
    action = wezterm.action.CompleteSelection 'Clipboard',
  },
  {
    event = { Up = { streak = 1, button = 'Right' } },
    mods = 'NONE',
    action = wezterm.action.PasteFrom 'Clipboard',
  },
  {
    event = { Up = { streak = 1, button = 'Right' } },
    mods = 'NONE',
    action = wezterm.action.PasteFrom 'PrimarySelection',
  },
  -- Open links with CTRL + Left button click
  {
    event = { Up = { streak = 1, button = 'Left' } },
    mods = 'CTRL',
    action = wezterm.action.OpenLinkAtMouseCursor,
  },
}
-- Closes tabs without confirm and add keymap
config.keys = {
  {
    key = 'w',
    mods = 'CTRL',
    action = wezterm.action.CloseCurrentTab { confirm = false },
  },
  {
    key = 't',
    mods = 'CTRL',
    action = wezterm.action.SpawnTab 'DefaultDomain',
  },
  {
    key = 'q',
    mods = 'CTRL',
    action = wezterm.action.QuitApplication,
  },
}

config.wsl_domains = {
  {
    name = 'WSL:Ubuntu-24.04.1',
    distribution = 'Ubuntu-24.04.1',
    username = 'techadmin',
  },
}

-- Font settings for tabs
config.window_frame = {
  font = require('wezterm').font 'Bahnschrift',
  font_size = 14,
}

return config

```
