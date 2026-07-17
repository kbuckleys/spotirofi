<b>A launcher for your tunes!</b> An advanced [rofi](https://github.com/davatorium/rofi) interface primarily designed for [spotify-player](https://github.com/aome510/spotify-player) and a part of the [ZENWORKS](https://github.com/kbuckleys/ZENWORKS) Suite.

---

<table>
  <tr>
    <td align="center">
      <img width="1030" height="211" alt="2026-07-17-073212_hyprshot" src="https://github.com/user-attachments/assets/25545ad7-e825-4b47-8e10-08859e1b40e0" />
      <br/>
      <b>Main Menu</b>
    </td>
    <td align="center">
      </table> <img width="1031" height="337" alt="2026-07-17-073255_hyprshot" src="https://github.com/user-attachments/assets/a9dd4ba4-081c-4ada-bcb2-85eebbaf07e5" />
      <br/>
      <b>Liked Tracks</b>
    </td>
  </tr>

<br>

This is a near complete replacement to spotify-player's UI, almost everything you can do in the main client can be done from within this interface. It's meant to be a quick and convenient way to manage your listening on the fly, much like a program launcher, except for your music. There's much you can do in this interface, so I'd rather list the things you CANNOT do:

- Precise seeking.
- View lyrics (might be doable, remains to be looked into)
- There's an API cap on some results (20), so at one point you'll have to use the main client.

The script assumes you already have spotify-player installed and authenticated. At launch, it will automatically run the daemon ```spotify_player -d``` and you can start using the rofi interface right away. You're still able to run spotify-player normally, even with the daemon running, in case you want more advanced functionalities.

# To-do
- Improve initial load times for menus at first run.
- Search is practically useless for some reason. Needs looking into.
