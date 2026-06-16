# AIMP Floating Lyrics Plugin - Localization

> Also see [Post on AIMP Forum](https://aimp.ru/forum/index.php?topic=77574.0).

> What's this?  
> The repo provides AIMP-Floating-Lyrics-Plugin translations.  
> As I'm from China, I only know about Chinese and English. If you are interested, you can help translate this plugin to other languages.

### About Plugin

Here I present my hand-made plugin: AIMP Floating Lyrics Player and Editor Plugin, as a software developer, this is my hobby project. If you have found any issue, it would be a great help to tell me :)!
It has these features:

1. It plays synchronized lyrics file(currently only supports ".lrc" file format with UTF-8 or ASCII encoding) for your song, it reads from your local lrc file alongside with your song file, or if your song file has synchronized lyrics embedded(like ID3v2 tag supported by AIMP), it will also play it;
2. For playing lyrics, you can style text color, text size, text shadow and more, I have written a preference window to configure these(and more configurations will be brought in the future updates);
3. For playing lyrics, currently I designed 2 playing styles, one is to fade in fade out lyrics text, another style is to scroll lyrics horizontally;
4. You can make or edit your own ".lrc" file, just right click the playing lyrics window, choose "Make / Edit Lyrics". Or in AIMP playlist, right click playlist item(aka, songs in your library), choose "Send to - Lyrics Editor".
5. About the lyrics editor, when it opens, it will fill basic information automatically if it finds that, otherwise, you need to input information yourself.
6. Some hint to use the lyrics editor: Currently I exposed 3 hotkeys to inert/replace/delete timestamp on active line, they are bound with F7/F8/F9 keys globally by default. You can always change these hotkeys in AIMP's "Hotkeys" configuration, but remember, local hotkeys won't work, because the lyrics editor is not recognized by AIMP as local window. The inserted or replaced timestamp is always the timestamp that AIMP is current playing at, so ideally you just play the song once and inserted timestamps all by yourself. There are also some handy buttons there, you can hover on them to see brief descriptions.

\*Tip: you can set lyrics playing window's background color to a totally transparent value, which looks fancy, but it will make context menu harder to open, if you really can't fetch context menu at that time, go to AIMP's "preferences - Floating Lyrics", you can open plugin's preference window there.

### How to Install & Use

To install and use this plugin,

1. Download and install ".NET 8.0 Desktop Runtime":
    - for AIMP x64: https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-8.0.26-windows-x64-installer
    - for AIMP x86: https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-8.0.26-windows-x86-installer

2. ~~Download and install "Visual C++ Redistributable 2012" from https://www.microsoft.com/en-us/download/details.aspx?id=30679, make sure to pick x86 or x64, which depends on AIMP x86 or x64 your are using. (a known issue listed below also mentions this runtime package, if you are not sure, I recommend you just download and install it);~~

You no longer need to install VC++ 2012 since v1.2.4, plugin has already included necessary files.

3. Unzip "aimp_floating_lyrics_x[86\_or\_64]\_ver\_[VERSION].zip" and drop extracted "aimp_floating_lyrics" folder to "[your-AIMP-x86-or-x64-installation-folder]/Plugins";
4. Finally, open AIMP and check "Floating Lyrics" menu item in AIMP's main menu to show lyrics player window and let's roll!

### Troubleshooting

~~1. If AIMP complains about an external exception when opening preference window, that's because my plugin is importing "msvcr110.dll" to make sure .net UI is compatible with AIMP's Delphi UI,~~  
~~when that happens, make sure to download and install "Visual C++ Redistributable 2012" here: https://www.microsoft.com/en-us/download/details.aspx?id=30679, plugin should work properly then.~~

You no longer need to install VC++ 2012 since v1.2.4, plugin has already included necessary files.

2. In some cases, AIMP might disable the plugin so you won't be able to use the plugin in AIMP, you can follow these steps to fix:

> i. Make sure to close AIMP instance before proceed;  
> ii. Open "AIMP.ini" file within "[your-AIMP-installation-directory]/Profile" directory, search and delete these lines (it may differ from your file, but should look similar):
>
> ```ini
> [Plugins]
> aimp_floating_lyrics.dll=0
>
> [Plugins.CachedInfo]
> aimp_floating_lyrics.dll=0|||||1552900961
> ```
>
> iii. If this still does not work, you can try to delete whole `[aimp_floating_lyrics_plugin]` section in "AIMP.ini" file, this will reset all configurations of my plugin.

Try launching AIMP after that, plugin should work now.

### Plugin Screenshots

![Floating lyrics Window](/screenshots/floating_window.jpg)
![Floating lyrics Window Context Menu](/screenshots/context-menu.jpg)
![Lyrics Editor](/screenshots/lyrics_editor.jpg)
![Preference Window](/screenshots/preference_window.jpg)
![Configuration Panel in AIMP](/screenshots/configuration_panel_in_AIMP.jpg)

### Change Logs

#### 1.2.5.fix1 (2026.06.16)

- Fix Two-Line play style will not clean up stage if switching to a song without lyrics (bug reported by **Soolo**)
- Fix an issue that Two-Line play style may not play first lyrics line if its starting time is too small
- Make lyrics scroll window fades in/fades out if window is about to change visibility

#### 1.2.5 (2026.06.14)

- Implement Two-Line play style, which plays lyrics in two-line
- Optimize One-Line play style: when playback pauses/resumes, animations will also pause/resume
- Optimize animations when user starts/restarts/seeks/stops playback
- Add `Fade Duration` preferences for both One-Line and Two-Line play styles (note that they did not share same preferences)
- Optimize overall stability

#### 1.2.4 (2026.06.14)

- Optimize plugin's low native C++ layer to have better memory management
- Drop the necessity of installing VC++ 2012 runtime
- Optimize "edge feather width" preference implementation to prevent lyrics from being blocked by it
- Support playing non-synchronized lyrics in `.txt`/`.lrc` files or embedded tag (suggested by **Artem**)
- Fix .NET string formatting behaves inconsistently across different systems with different regional formats (bug reported by **Soolo**)

#### 1.2.3 (2026.06.04)

- Fix(#6): At the edge of playing lyrics, shadow effect may be blocked by an invisible area, this happens because lyrics playing area is not set to full width of owner window
- Fix inconsistent .NET `System.Convert` behavior among Windows OS with different regional format (Thanks for **Soolo** reporting the issue!)
- Fix some memory leak issues as **Artem** points out (Thank you AIMP creator!), and with the help of CRT Library, some native C++ code is refactored in this update to get away such issue as much as possible

#### 1.2.2 (2026.05.31)

- optimize(#6 related): Add lyrics window edge feather effect and a corresponding preference to set feather width
- Add a hotkey that allows to toggle lyrics window click-through behavior
- Make preference window layout responsive, alongside some minor adjustments
- Fix an issue happens when user toggles/restarts playing song, window would blink once when "Hide if No Lyrics" preference is enabled
- Other minor fixes and optimizations

#### 1.2.1.1 (2026.05.26)

- Fix an issue when "Hide if No Lyrics" preference is enabled, there is a chance lyrics window not showing even if playing song has lyrics
- Optimize option dialog implementation to embrace AIMP's Automatically Localization feature
- Add some localization entries

#### 1.2.1 (2026.05.20)

- Add a preference, when enabled, floating lyrics window will not appear on taskbar
- Add a preference, when enabled, floating lyrics window will be hidden when no lyrics are found
- Add text stroke preference, which means outlined/hollow text is supported now
- Font family picker now respects AIMP's language: font family name now displays as AIMP language if possible
- Preference window's size is remembered now in case some user's screen is too small
- Other minor bug fixes and optimizations, and modified some localization entries

#### 1.2.0 (2026.05.10)

- Migrate plugin's floating lyrics window implementation to Edge Webview2 to achieve better animation performance.
- Add letter spacing preference as web platform supports them out of the box.
- Add an experimental preference that allows you to animate letter spacing under "Fade In Out Play Style", which looks fancy.
- Other minor bug fixes and optimizations, and modified some localization entries.

#### 1.0.3 (2026.04.21)

- Support multi-language lrc file as 17hapi on AIMP forum suggests
- Change default font family to make UI look better
- Optimize lang files entries, enhance Chinese translations

#### 1.0.2 (2026.04.19)

- Re-write preference window user interface to make it have a modern look
- Add an option to enable/disable click-through lyrics playing window(note that when background is set to a transparent color, the click-through feature is always enabled)
- Fix an issue causing context menu's text and icon blurry
- Other minor stability optimizations and adjustments

#### 1.0.1 (2026.04.15)

- Now supports both AIMP 5 x86 and x64! Make sure to download corresponding zip file and install corresponding runtime packages (see "How to Install & Use" section below)
- Fix an issue causing lyrics editor to crash when user clears "offset" input
- Add option panel in AIMP's preference window, provides functionality to open plugin's preference window or reset lyrics playing window's position there
- Optimize code originally porting from .NET Framework to ensure better compatibility with .NET 8.0
- Update project dependencies: WPF.UI from 4.0.3 to 4.2.0; my dotnet-lrc-parser 0.3.0 to 0.3.1(minor changes concerning .NET 8.0)
- Other stability optimizations and adjustments

#### 1.0.0 (2026.04.12)

Original Release
