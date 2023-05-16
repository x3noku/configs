# Kitty Config

### Create `kitty.conf` file
```shell
touch ~/.config/kitty/kitty.conf
```

### Update `kitty.conf` file
```yaml
include other.conf
# Include *.conf files from all subdirs of kitty.d inside the kitty config dir
globinclude kitty.d/**/*.conf
# Include the *contents* of all env vars starting with KITTY_CONF_
envinclude KITTY_CONF_*

cursor_shape block
shell_integration no-cursor
cursor_blink_interval 0

font_family JetBrainsMonoNerdFontCompleteM-Regular
font_size 11.5
bold_font auto
italic_font auto
bold_italic_font auto

tab_bar_style separator
active_tab_foreground   #ccc
active_tab_background   #555
inactive_tab_foreground #ccc
inactive_tab_background #232627
tab_separator " | "
tab_title_template "{bell_symbol}{activity_symbol}{tab.active_wd.split('/')[-1]}:{tab.active_exe}"

background_opacity 0.9
background #232627

map ctrl+shift+t new_tab_with_cwd
map ctrl+shift+h previous_tab
map ctrl+shift+l next_tab
map ctrl+shift+[ move_tab_backward
map ctrl+shift+] move_tab_forward
map ctrl+b close_tab

map ctrl+j scroll_line_down
map ctrl+k scroll_line_up
map ctrl+d scroll_page_down
map ctrl+u scroll_page_up
map ctrl+g scroll_home
map ctrl+shift+g scroll_end
```
