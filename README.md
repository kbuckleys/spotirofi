https://github.com/user-attachments/assets/f0d46590-c18e-4a06-9ac5-4488df955887

<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

This is a near complete replacement for any Spotify client, almost everything you can do in a full-fledged client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Remove from queue (Spotify Web API limitation)
  > Local queue can be implemented as an alternative. In which case it will provide full control over its functions. However...
  > - It adds complexity and relative blaot for what it's supposed to do.
  > - Local implementation inherently means zero sync with other Spotify clients/connect devices if you use any.
- Podcast management
  > Not that spotirofi can't do it, I simply didn't implement support for it, for two primary reasons;
  > - Spotify's API doesn't expose some of the key features that help make listening to podcasts accessible, like chapter management.
  > - This may sound subjective, but it's a relatively niche medium to cover.
 
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
Given the scope, you can be easily multiple levels deep as you navigate through menus, so it was important to set some keybinds in place for convenience and faster -hopefully organic- interactions.
> Keybinds can also be viewed from <b>Main > System > Keybinds</b>
- Alt + Backspace takes you one level back
- Alt + L jumps to your liked tracklist
- Alt + Q jumps to your queue list
- Alt + / jumps to Search > All
- Alt + Space jumps to main menu
- Alt + S jumps to active track's seek menu
- Alt + C highlights the currently active track in a list.
- Alt + V jumps to the player's volume control panel (not system volume)
- Alt + Return jumps to the currently active (playing/paused) track's action menu
- Esc will close the rofi interface, regardless of where you are, and when you next open rofi again, it will remember your depth and resume where you left off

> [!NOTE]
> Made For You is a dedicated place for your own followed Spotify's curated playlists. if it's empty, it's because you didn't add any of these lists.
