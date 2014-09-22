Zed Finally Hits 1.0
====================
date: 2014-09-22

After over 1.5 years of development (the last ~6 months close to full-time) here it is: Zed 1.0. Of course version numbers don't really mean much, but I thought it was good to finally hit 1.0. I've been using it for over a year full-time and I'm pretty happy with it.

This release brings some big changes as well as many minor tweaks:

* Unified UI: the separate project picker window is gone and has been integrated into editor windows (using same theming etc.). Similarly the first run, dropbox project, github picker windows have all been integrated as well.
    ![](/img/projectpicker.png)
* New preferences GUI offering a more friendly way of changing preferences, access it via `Configuration:Preferences` (`Command-,`/`Ctrl-,`). Fun fact: the preferences UI is actually [just a Zed package](https://github.com/zedapp/config-ui) that runs a web app integrated using Zed's built in web-server.
    ![](/img/preferences.png)
* Window restore on relaunch: All windows are now restored after Zed quit (`Zed:Quit`) and restart.
* Zed now also supports vim-style cursor movement. These keyboard combinations have the advantage of not having to move your hand to your cursor keys to move around. If you're familiar with vi or vim, they are generally the same keys you always use to move around together with the `Alt` key. Supported are:

  * `Alt-h`: move cursor to the left
  * `Alt-j`: move cursor down
  * `Alt-k`: move cursor up
  * `Alt-l`: move cursor to the right
  * `Alt-w`: move cursor one word to the right
  * `Alt-b`: move cursor one word to the left
  * `Alt-0`/`Alt-^`: move cursor to the start of the line
  * `Alt-$`: move cursor to the end of the line
  * `Alt-Shift-g`: move cursor to end of the file

  In addition, many of these also work together with `Shift` to use them to select text, e.g. `Alt-Shift-H` selects one character to the left.

* Native window chrome (title bar -- see screenshots above) is now used in the standalone version of Zed as well as the Chrome App version on Linux.
* The "Notes" space has been removed, due to too frequent data loss for users, we recommend to just use a local folder instead. If you were using Notes before and would like to access it still, enter "syncfs:" in the project picker search box and press Enter.

There is another big change coming to Zed, but it's not a technical one. As many of you will be aware, [on April 1st](http://zedapp.org/2014/04/zed-the-next-phase/) I made Zed my day time job. Since I've been able to iterate on Zed a lot. From the get go this was an experiment both financially, but also: would I enjoy working working on this in a 1-person team (me) -- of course there's some open source contributions, but most of the work is still done by me. While I'm not really surprised that after 6 months Zed doesn't generate enough income to pay a reasonable salary, what was I did not predict was that after working 3 years from an office far away from my co-workers I'm ready for a change. Therefore, I've decided to take a job in the city where I live (at [STX Next](http://www.stxnext.com)). For the first time in my industrial career I'll share an office with co-workers.

This also means that starting October 1st, Zed will once again become a spare time project. Naturally, I'll keep using Zed for all my programming (and since STX Next is a Python shop, I'll use it a lot for Python coding) so I'm sure improvements will keep coming, but probably at a slower pace.

Back to Zed 1.0 itself -- beside the changes above, here are some more cool ones:

* Syntax highlighting added for TeX/LaTeX, Ada, Assembly, Cobol, diff files, FORTH, .gitignore, Jade, Lisp, Objective-C, Pascal, R, Scheme, SQL (including MySQL and Postges flavours), SVG, Tcl, Typescript, Vala, and a bunch more, some of which I never heard of — if Ace supports it, now we support it too (by lalomartins)
* Standalone: Windows version now uses Zed icon on desktop.
* Default editor window size increased to 1024x768
* Linux window size restore improved.
* Fixed mouse UI UX issues (dragging and dropping of text now supported) (by nightwing)
* New commands:
    * `Navigate:Last Edit Point` (useful to go back to last location you were editing after jumping to a symbol)
    * `Window:List` (lists all open Zed windows and allows you to quickly jump between them)
* Keyboard shortcuts have been refactored here and there to better support non-Mac OSes (ChromeOS, Linux, Windows) -- check the command list when a keybinding you were accustomed to no longer works.
* Fixed Coffeescript display bug (by nightwing)
