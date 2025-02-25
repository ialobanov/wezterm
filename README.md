# WezTerm Configuration for Windows setup

```ps1
vim .wezterm.lua
```

```lua
-- Core setting
local wezterm = require 'wezterm'
local mux = wezterm.mux
local config = {}

-- Colors & perfomance
config.term = "xterm-256color"
config.front_end = "WebGpu"
config.webgpu_power_preference = "HighPerformance"

-- Maximaze on start up
wezterm.on("gui-startup", function()
  local tab, pane, window = mux.spawn_window{}
  window:gui_window():maximize()
end)

-- PowerShell by default shell
config.default_prog = { 'pwsh' }

-- Font settings
config.font = wezterm.font 'JetBrains Mono' 
config.font_size = 20.0

-- WezTerm theme
config.color_scheme = 'rebecca'

-- Disable audio
config.audible_bell = 'Disabled'

-- Copy by Mouse Left button selection text and paste by Right button click 
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
    -- Open links CTRL + Left button click
    {
      event = { Up = { streak = 1, button = 'Left' } },
      mods = 'CTRL',
      action = wezterm.action.OpenLinkAtMouseCursor,
    },
}

config.wsl_domains = {
  {
    name = 'WSL:Ubuntu-24.04.1',
    distribution = 'Ubuntu-24.04.1',
    username = "techadmin",
  },
}

-- Cursor color
config.colors = {
  cursor_bg = '#0CFF93',
  cursor_fg = 'black',
  cursor_border = '#0CFF93',
}

-- Font settings for tabs
config.window_frame = {
  font = require('wezterm').font 'Bahnschrift',
  font_size = 12,
}

return config
```
