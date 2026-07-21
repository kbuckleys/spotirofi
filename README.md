<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

<table>
  <tr>
    <td><img width="1005" height="323" alt="2026-07-21-123850_region" src="https://github.com/user-attachments/assets/29384991-c927-4678-a743-ade3923b3587" /></td>
    <td>Main Menu</td>
  </tr>
  <tr>
    <td><img width="1014" height="430" alt="2026-07-21-122437_region" src="https://github.com/user-attachments/assets/1cefec2b-b696-47c7-9141-6c13e1b21348" /></td>
    <td>Track's Action Menu</td>
  </tr>
  <tr>
    <td><img width="1009" height="271" alt="2026-07-21-132451_region" src="https://github.com/user-attachments/assets/5be676f6-3fe7-492b-95f9-9a57fc6f00f1" /></td>
    <td>Liked Tracks</td>
  </tr>
  <tr>
    <td><img width="1019" height="270" alt="2026-07-19-151355_region" src="https://github.com/user-attachments/assets/2916717e-7598-43b8-8a09-836bdbce32e1" /></td>
    <td>Lyrics view</td>
  </tr>
</table>

<br>

This is a near complete replacement for any Spotify client, almost everything you can do in a full-fledged client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Remove from queue (Spotify Web API limitation)
> Local queue can be implemented, but may add complexity. Remains to be explored
- Podcast management
> Not that spotirofi can't do it, I simply didn't implement support for it
 
The script's first run will automatically take you to Spotify's authentication page (two separate pages in fact, that's just a spotifyd quirk), assuming you already have ```spotifyd``` installed. At launch, it will notify you that it's building cache and will automatically run the daemons and display the main menu, at that point you can start using the rofi interface right away.

# Functionality
- Your paths are nested and retained by default, given the number of menus and submenus. This is why some custom keybinds had to be set in place, instead of reopening the main menu every time and going through multiple depth levels.
- Cache gets updated every 12 hours. a safeguard in case you made external changes to your library from, say; your phone or another Spotify client. There's also a manual option to refresh the cache, <b>but only use it when you absolutely have to.</b> Your activity on the player is dynamically and locally refreshed anyway, so you'll probably never have to use this feature.

# Dependencies
- Spotify Premium
- spotifyd
- rofi
- cjson
- lua 5.4+
- curl
- xdg-open
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
