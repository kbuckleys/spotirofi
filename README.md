<b>A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface designed for <a href="https://github.com/aome510/spotify-player">spotify-player</a> and a part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite.

<table>
  <tr>
    <td><img width="1015" height="222" alt="2026-07-19-134954_region" src="https://github.com/user-attachments/assets/9c2d5d1f-6031-4e74-b450-1d95b8e74049" /></td>
    <td>Main Menu</td>
  </tr>
  <tr>
    <td><img width="1018" height="276" alt="2026-07-19-135014_region" src="https://github.com/user-attachments/assets/7f1128dc-07e5-49f1-a203-b2364c451250" /></td>
    <td>Track's Action Menu</td>
  </tr>
  <tr>
    <td><img width="1016" height="328" alt="2026-07-19-135049_region" src="https://github.com/user-attachments/assets/c99b94b0-2a18-42c7-aaaf-ce235001b149" /></td>
    <td>Liked Tracks</td>
  </tr>
  <tr>
    <td><img width="1013" height="270" alt="2026-07-19-135138_region" src="https://github.com/user-attachments/assets/a33a03bb-9058-4cff-96b2-ad2df0a97859" /></td>
    <td>Lyrics view</td>
  </tr>
  <tr>
    <td><img width="1014" height="143" alt="2026-07-19-135403_region" src="https://github.com/user-attachments/assets/91c70be0-8a4b-4746-a048-eda7a708e782" /></td>
    <td>Precise Voume Control</td>
  </tr>
</table>

<br>

This is a near complete replacement for spotify-player's UI, almost everything you can do in the main client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's a lot you can do in this interface -and I mean A LOT- you can even show lyrics! So I'd rather list the things you CANNOT do:

- Precise seeking.
- Result pagination is hard capped, so at one point you'll have to use the main client.

The script assumes you already have spotify-player installed and authenticated. At launch, it will automatically run the daemon ```spotify_player -d``` and you can start using the rofi interface right away. You're still able to run spotify-player normally, even with the daemon running, in case you want more advanced functionalities.

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
