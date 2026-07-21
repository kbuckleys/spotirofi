<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

<table>
  <tr>
    <td><img width="1010" height="218" alt="2026-07-19-151243_region" src="https://github.com/user-attachments/assets/456ff58a-3119-4bb1-85a6-c590771a4c08" /></td>
    <td>Main Menu</td>
  </tr>
  <tr>
    <td><img width="1011" height="273" alt="2026-07-19-151252_region" src="https://github.com/user-attachments/assets/ad67201e-1f38-498b-934c-e3b5f80cf5c3" /></td>
    <td>Track's Action Menu</td>
  </tr>
  <tr>
    <td><img width="1017" height="328" alt="2026-07-19-151309_region" src="https://github.com/user-attachments/assets/09b963f9-cd33-467d-9cd0-22c7a13b1c0d" /></td>
    <td>Liked Tracks</td>
  </tr>
  <tr>
    <td><img width="1019" height="270" alt="2026-07-19-151355_region" src="https://github.com/user-attachments/assets/2916717e-7598-43b8-8a09-836bdbce32e1" /></td>
    <td>Lyrics view</td>
  </tr>
</table>

<br>

This is a near complete replacement for any Spotify client, almost everything you can do in a full-fledged client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Precise seeking.
- Remove from queue. (Spotify's Web API limitation)
 
The script's first run will automatically take you to Spotify's authentication page (two separate pages in fact, that's just a spotifyd quirk), assuming you already have ```spotifyd``` installed. At launch, it will automatically run the daemon and you can start using the rofi interface right away.

Another important notice, the first time you navigate the interface post-authentication; it may be a bit slow as it generates the cache files, which are located in ```~/.cache/spotirofi```. However, future runs will be fluid and snappy.

# Functionality
- Your paths are nested and retained by default, given the number of menus and submenus. This is why some custom keybinds had to be set in place, instead of reopening the main menu every time and going through multiple depth levels.
- First run will be slow as the script generates a fresh cache for faster and near instant interactions.
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
- Alt + Backspace takes you one page up.
- Alt + / takes you directly to Search > All, from any depth.
- Alt + Space takes you back to main menu, from any depth.
- Alt + Return takes you to the currently active (played/paused) track's action menu, from any depth.
- Esc will close the rofi interface, regardless of where you are, and when you next open rofi again, it will remember your depth and resume where you left off.
