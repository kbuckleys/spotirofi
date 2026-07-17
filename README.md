<b>A launcher for your tunes!</b> An advanced [rofi](https://github.com/davatorium/rofi) interface primarily designed for [spotify-player](https://github.com/aome510/spotify-player) and a part of the [ZENWORKS](https://github.com/kbuckleys/ZENWORKS) Suite.

<br>

<table>
  <tr>
      <img width="1016" height="198" alt="2026-07-17-130549_hyprshot" src="https://github.com/user-attachments/assets/66bf2901-c6df-4c43-a175-ef53110ae027" />
      <br/>
    </td>
      <img width="1023" height="328" alt="2026-07-17-130738_hyprshot" src="https://github.com/user-attachments/assets/c7e6915e-a44e-4857-b3ca-5c1b5c22b9b5" />
      <br/>
    </td>
      <img width="1019" height="281" alt="2026-07-17-130604_hyprshot" src="https://github.com/user-attachments/assets/bf1ac057-d3d6-44f1-8de0-88e7e396dfec" />
    <br/>
    </td>
      <img width="1019" height="272" alt="2026-07-17-130620_hyprshot" src="https://github.com/user-attachments/assets/d7325747-74c9-4001-a2f4-21e04328c6ad" />
    <br/>
    </td>
  </tr>

---

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
> Unfortunately, due to a lot of track ID mismatches, ```playerctl``` doesn't communicate well with spotify_player -d, which is strange because spotify-player works fine with playerctl. In short; the daemon's broken context queue makes the rofi interface play the wrong tracks and consequently; break proper continuous context-based playback. So the solution is a set of compositor keybinds that will replace your playerctl's (if you use them). If you don't use them, no need to worry about step 2 of the installation process. This is purely for using quick keybinds to play/pause, next/prev. Before you panic, rest assured that any program you have that uses playerctl will still work with these funky new binds.

# Installation
- Drop both directories in ```~/.config/rofi/```.
- Replace your playerctl keybinds with these. Other programs that use playerctl will still play along with these binds:

~~~
 lua ~/.config/rofi/scripts/spotify/spotify.lua play-pause || playerctl play-pause
 lua ~/.config/rofi/scripts/spotify/spotify.lua prev || playerctl previous
 lua ~/.config/rofi/scripts/spotify/spotify.lua next || playerctl next
~~~
