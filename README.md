<b>A launcher for your tunes!</b> An advanced [rofi](https://github.com/davatorium/rofi) interface primarily designed for [spotify-player](https://github.com/aome510/spotify-player) and a part of the [ZENWORKS](https://github.com/kbuckleys/ZENWORKS) Suite.

<br>

<table>
  <tr>
      <img width="1030" height="211" alt="2026-07-17-073212_hyprshot" src="https://github.com/user-attachments/assets/25545ad7-e825-4b47-8e10-08859e1b40e0" />
      <br/>
    </td>
      </table> <img width="1031" height="337" alt="2026-07-17-073255_hyprshot" src="https://github.com/user-attachments/assets/a9dd4ba4-081c-4ada-bcb2-85eebbaf07e5" />
      <br/>
    </td>
  </tr>

---

This is a near complete replacement to spotify-player's UI, almost everything you can do in the main client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's much you can do in this interface, so I'd rather list the things you CANNOT do:

- Precise seeking.
- View lyrics (might be doable, remains to be looked into)
- Result pagination is hard capped, so at one point you'll have to use the main client.

The script assumes you already have spotify-player installed and authenticated. At launch, it will automatically run the daemon ```spotify_player -d``` and you can start using the rofi interface right away. You're still able to run spotify-player normally, even with the daemon running, in case you want more advanced functionalities.

# To-do
- Improve initial load times for menus at first run.
- Search filtering is practically useless for some reason. Needs looking into.

# But why only for spotify-player?
While I could transition to Spotify's Web API for broader compatibility, there are plenty of drawbacks that come along with it:
- Latency — Every search, library load, detail fetch becomes an HTTP round trip instead of a local process call. Browsing an artist, album, tracks means 3 sequential API calls with network overhead.
- Rate limiting — Spotify API limits to ~180 requests per minute per app. Heavy browsing (opening multiple artists, albums) could hit this.
- Token depends on spotify_player — Alternatively, implementing full OAuth2 (register a Spotify app, browser-based auth flow, handle redirects) is possible but more complex.
- No local cache fallback — Currently the script reads spotify_player's local cache files as a fallback. Pure API means if the API is down or rate-limited, nothing happens.
- Pagination everywhere — Liked tracks, playlists, search results, followed artists are all paginated (max 50 per page). More code to handle that.

Long story short, spotify-player does most of the heavy lifting and the rofi interface is a mere portal to its cache.
