<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface designed for <a href="https://github.com/aome510/spotify-player">spotify-player</a> and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

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
  <tr>
    <td><img width="1023" height="140" alt="2026-07-19-151408_region" src="https://github.com/user-attachments/assets/4bd2c733-e697-4a7a-a2fd-9a4563fccd54" /></td>
    <td>Precise Voume Control</td>
  </tr>
</table>

<br>

This is a near complete replacement for spotify-player's UI, almost everything you can do in the main client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Precise seeking.
- Removing a track from queue list.
- Result pagination is hard capped, so at one point you'll have to use the main client.

The script's first run will automatically take you to Spotify's authentication page, assuming you already have spotify-player installed. At launch, it will automatically run the daemon ```spotify_player -d``` and you can start using the rofi interface right away. You're still able to run spotify-player normally, even with the daemon running, in case you want more advanced functionalities.

Another important notice, the first time you navigate the interface, it might be a bit slow as it generates the cache files, which are located in ```~/.cache/spotify_rofi```. However, future runs will be fluid and snappy.

# But why only for spotify-player?
Long story short, spotify-player does most of the heavy lifting and the rofi interface is a mere portal to its CLI and cache. While I could transition to Spotify's Web API for broader compatibility, there are plenty of drawbacks that come along with it:
- Latency — Every search, library load, detail fetch becomes an HTTP round trip instead of a local process call. Browsing an artist, album, tracks means 3 sequential API calls with network overhead.
- Rate limiting — Spotify API limits to ~180 requests per minute per app. Heavy browsing (opening multiple artists, albums) could hit this.
- Token depends on spotify_player — Alternatively, implementing full OAuth2 (register a Spotify app, browser-based auth flow, handle redirects) is possible but more complex.
- No local cache fallback — Currently the script reads spotify_player's local cache files as a fallback. Pure API means if the API is down or rate-limited, nothing happens.
- Pagination everywhere — Liked tracks, playlists, search results, followed artists are all paginated (max 50 per page). More code to handle that.

# Dependencies
- rofi
- spotify-player
- cjson
- lua 5.3+
- curl
- xdg-open
- pgrep
- A nerd font

> [!NOTE]
> <b>You only need to read this if you have playerctl keybinds set up</b>
>
> Unfortunately, due to ```playerctl``` not communicating as well as it should with spotify_player -d --which is strange because spotify-player works fine with playerctl-- there's a lot of track ID mismatches. In short; the daemon's broken context queue makes the rofi interface play the wrong tracks and consequently; break proper continuous context-based playback. So the solution is a set of compositor keybinds that will replace your playerctl's (if you use them). If you don't use them, no need to worry about step 2 of the installation process. This is purely for using quick keybinds to play/pause, next/prev. Before you panic, rest assured that any program you have that uses playerctl will still work with these funky new binds.

# Installation
- Drop both directories in ```~/.config/rofi/``` and assign a keybind for ```spotify.lua``` in your compositor's config.
- Replace your playerctl keybinds' targets with these. Other programs that use playerctl will still play along with these binds:

~~~
 lua ~/.config/rofi/scripts/spotify/spotify.lua play-pause || playerctl play-pause
 lua ~/.config/rofi/scripts/spotify/spotify.lua prev || playerctl previous
 lua ~/.config/rofi/scripts/spotify/spotify.lua next || playerctl next
~~~

# Controls
While this may seem silly, I have slightly different controls set in place for this setup, given you can navigate through the interface and retain your position when you reopen rofi. So given its scope, this had to be done.
- Alt + Backspace takes you one page up.
- Alt + / takes you directly to Search > All, from any depth.
- Alt + Space takes you back to main menu, from any depth.
- Alt + Return takes you to the currently active (played/paused) track's action menu, from any depth.
- Esc will close the rofi interface, regardless of where you are, and when you next open rofi again, it will remember your depth and resume where you left off.
