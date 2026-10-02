# Optional focused-window glow

Hyprland can draw a soft outer halo with its window shadow. Ember Foundry uses a warm amber color for focused windows and a faint neutral shadow for inactive windows. Omarchy disables shadows by default.

Append this snippet to `~/.config/hypr/looknfeel.lua`:

```lua
-- A subtle amber halo only while Ember Foundry is active.
local ember_theme_file = io.open((os.getenv("HOME") or "") .. "/.local/state/omarchy/current/theme.name", "r")
local ember_theme_name = ember_theme_file and ember_theme_file:read("*l")
if ember_theme_file then ember_theme_file:close() end

if ember_theme_name == "ember-foundry" then
  hl.config({
    decoration = {
      shadow = {
        enabled = true,
        range = 16,
        render_power = 3,
        color = "rgba(e5ad6060)",
        color_inactive = "rgba(00000022)",
      },
    },
  })
end
```

Run `hyprctl reload` and `hyprctl configerrors` to apply and validate the change. The halo appears when Ember Foundry is active and switches off when you change to another theme. `omarchy theme set ember-foundry` applies the theme and reloads Hyprland.

Omarchy's Git theme installer omits executable Lua files from repositories, so this user-config step is necessary for a theme installed from GitHub. See [Hyprland's shadow settings](https://wiki.hypr.land/Configuring/Basics/Variables/#shadow) for `range`, `render_power`, and color details.
