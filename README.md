<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/cfedabca-5deb-4834-845f-44aaca207619">
  <img src="image-light.png" alt="">
</picture>

<h3><p align="center">
A launcher for your tunes!</b> An advanced <a href="https://github.com/davatorium/rofi">rofi</a> interface
<br>
Part of the <a href="https://github.com/kbuckleys/ZENWORKS">ZENWORKS</a> Suite
</p></h3>

<br>

https://github.com/user-attachments/assets/f0d46590-c18e-4a06-9ac5-4488df955887

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
- playerctl
- curl
- wl-clipboard
- notify-send
- perl
- pgrep
- A nerd font

# Installation
- Drop both directories in ```~/.config/rofi/``` and assign a keybind for ```spotirofi.lua``` in your compositor's config
- chmod +x ```spotirofi.lua``` to make it executable
- Run ```spotirofi.lua``` and enjoy

# Controls
Given the scope, you can be easily multiple levels deep as you navigate through menus, so it was important to set some keybinds in place for convenience and faster -hopefully organic- interactions.
> Keybinds can also be viewed from <b>Main > System > Keybinds</b>

<body>
  <table>
    <thead>
      <tr><th>Key</th><th>Action</th><th>Context</th></tr>
    </thead>
    <tbody>
      <tr><td><kbd>Alt+Return</kbd></td><td>Jump to main menu</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+Backspace</kbd></td><td>Back one level</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+Space</kbd></td><td>Exit to main menu</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+/</kbd></td><td>Search all</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+l</kbd></td><td>Liked tracks</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+q</kbd></td><td>Your queue</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+v</kbd></td><td>Volume</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+a</kbd></td><td>Album art of current track</td><td>Anywhere</td></tr>
      <tr><td><kbd>Alt+c</kbd></td><td>Jump to playing track / Jump to current lyric line</td><td>List / Lyrics</td></tr>
      <tr><td><kbd>Alt+s</kbd></td><td>Seek current track</td><td>List / Lyrics</td></tr>
      <tr><td><kbd>Return</kbd></td><td>Select</td><td>Anywhere</td></tr>
      <tr><td><kbd>Escape</kbd></td><td>Close</td><td>Anywhere</td></tr>
    </tbody>
  </table>
</body>
</html>


> [!NOTE]
> Made For You is a dedicated place for your own followed Spotify's curated playlists. if it's empty, it's because you didn't add any of these lists.
