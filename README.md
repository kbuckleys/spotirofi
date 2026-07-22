https://github.com/user-attachments/assets/f0d46590-c18e-4a06-9ac5-4488df955887

<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

This is a near complete replacement for any Spotify client, almost everything you can do in a full-fledged client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Remove from queue (Spotify Web API limitation)
  > Local queue can be implemented, but may add complexity. Remains to be explored
- Podcast management
  > Not that spotirofi can't do it, I simply didn't implement support for it
 
The script's first run will automatically take you to Spotify's authentication page (two separate pages in fact, that's just a ```spotifyd``` quirk). At launch, it will notify you that it's building cache and will automatically run the daemons and display the main menu, at that point you can start using the rofi interface right away.

# Functionality
- Your paths are nested and retained by default, given the number of menus and submenus. This is why some custom keybinds had to be set in place, instead of reopening the main menu every time and going through multiple depth levels.
- Cache gets updated every 12 hours, a safeguard in case you made external changes to your library from, say; your phone or another Spotify client. There's also a manual option to refresh the cache, <b>but only use it when you absolutely have to.</b> Your activity on the player is dynamically and locally refreshed anyway, so you'll probably never have to use this feature.

# Dependencies
- Spotify Premium
- spotifyd
- rofi
- cjson
- lua 5.4+
- luajit
- playerctl
- curl
- xdg-open
- notify-send
- perl
- pgrep
- A nerd font

# Installation
- Drop both directories in ```~/.config/rofi/``` and assign a keybind for ```spotirofi.lua``` in your compositor's config.
- Run ```spotirofi.lua``` and enjoy.

# Controls
While this may seem silly, I have slightly different controls set in place for this setup, considering you can navigate through the interface and retain your position when you reopen rofi. So given this scope, some specific -and hopefully organic- keybinds had to be set in place.
- Alt + Backspace takes you one page up
- Alt + / takes you directly to Search > All, from any depth
- Alt + Space takes you back to main menu, from any depth
- Alt + Return takes you to the currently active (played/paused) track's action menu, from any depth
- Esc will close the rofi interface, regardless of where you are, and when you next open rofi again, it will remember your depth and resume where you left off

> [!NOTE]
> Made For You is a dedicated place for your own followed Spotify's curated playlists. if it's empty, it's because you didn't add any of these lists.
