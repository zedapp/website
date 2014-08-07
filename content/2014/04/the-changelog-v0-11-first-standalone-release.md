The Changelog: v0.11 -- First Standalone Release
=================
date: 2014-04-10

When I announced [that I would start working on Zed as my day job][1] I committed to one "feature" immediately: a standalone version -- a version you can use without having Chrome installed. Well, barely 2 weeks later, here it is! There may still be bugs here and there, but there's an auto-update feature, so hopefully we can quickly resolve bugs without too much work with re-downloading for you.

**Bonus feature:** Are you a Vim fan? Zed now has vim keybindings (see changelog below).

First, a little update with the funding situation. The good news is that we broke the [$100/week barrier on Gittip][2]. That's fantastic, but not nearly enough to make this project sustainable (we need roughly 10x that). So if you're a happy Zed user, [consider supporting the project financially][3].

Let me get right to the download links. If you're using the Chrome version (as now more than 15k people are!), you should be getting 0.11 within a few hours. If you want to try out the standalone version, here are the download links. Note: these may still be propagating through our CDN -- thanks [MaxCDN][4]! If the links don't work for you yet, try again in a few hours!

*   [Mac version of Zed standalone 0.11][5]
*   [Windows version of Zed standalone 0.11][6]
*   [Linux 64-bit version of Zed standalone 0.11][7]
*   [Linux 32-bit version of Zed standalone 0.11][8]

Here's the [changelog][9] for 0.11.0:

*   Standalone:
    *   First release of Zed standalone! I'm sure there will still be bugs, please report them on github when you find them.
    *   Open individual files or directories from the command line by calling "zed [dir]" or "zed [file]". On Mac, please install the CLI tools via the `Tools:Install Mac CLI` or the native Tools menu in the Mac app to use this.
*   Multiple keybindings support. That's right, we now have Vim and Emacs keybindings. Use the `Configuration:Preferences:KeyBinding:*` commands to switch between them. (by nightwing)
*   New commands:
    *   `File:Copy` (by iElectric)
*   Language modes:
    *   Python now has CTags indexing (by gholstla)
    *   Ability to switch off certain CSSLint options (by conradz)
*   Bugs fixed:
    *   Fixed a bug where when the project history is empty, no new projects are added.

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: http://zedapp.org/2014/04/zed-the-next-phase/
 [2]: https://www.gittip.com/zefhemel/
 [3]: http://zedapp.org/buy
 [4]: http://www.maxcdn.com
 [5]: http://download.zedapp.org/zed-mac-v0.11.0.tar.gz
 [6]: http://download.zedapp.org/zed-win-v0.11.0.zip
 [7]: http://download.zedapp.org/zed-linux64-v0.11.0.tar.gz
 [8]: http://download.zedapp.org/zed-linux32-v0.11.0.tar.gz
 [9]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
