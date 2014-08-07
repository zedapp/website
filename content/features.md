Features
========
1.  **Chrome Application:** Installing via the Chrome Web Store brings a few useful features:
    1.  Cross platform: Zed runs on any platforms that desktop Chrome runs on (including Chromebooks).
    2.  Installation is easy with just a few clicks.
    3.  Upgrades are automatic.
    4.  Settings are automatically synchronized between all computers logged into with the same Google account.
    5.  Special "Notes" space is stored in Google Drive and synchronized between computers automatically as well.
2.  **[Edit files remotely with your local preferences][1]:** Need to edit files on a remote server, or even in a local VM, and don't like copying your editor's settings files everywhere you go? Zed makes this easy, just install the `zed` binary with a single command(/download), run it to get a URL you can copy & paste into the Zed Chrome app, to edit files immediately. This works even if your server is part of a VPN or doesn't have a public IP.
3.  **Edit files locally:** By selecting "Open Local Folder"
4.  **Edit files directly on Dropbox:** By selecting "Open Dropbox Folder"
5.  **State preservation**: Zed preserves your editor state completely: the state of your splits, recency of open files, cursor and scroll positions, even part of the undo history for open files.
6.  **Auto save**: Zed always automatically saves your files. Save buttons are so '00s.
7.  **Chromeless:** Zed fits Chrome perfectly, by not having any. The UI is completely clutter free.
8.  **Keyboard oriented:** Zed can operated entirely with the keyboard.
9.  **Programming language support:**
    *   Linters/checkers for various languages (reports errors in the gutter as you edit code)
    *   Code completion (`Tab`):
        *   Words that appear in the current file (any file type)
        *   Based on ctags (Zed has its own ctags indexers for various languages)
        *   Snippets
10. **Efficient project navigation** at various levels of granularity:
    *   Files, quickly jump to the file you want (`Command-E`)
    *   Symbols, Zed indexes all symbols defined in your project and lets you quickly jump to the one you're interested in (`Command-R`, `Command-J`)
11. **Command-based:** Similar Emacs, every key you press in Zed runs a command. Keybinding to command mappings are configurable in the "Settings" projects. Commands can also executed by name via `Command-.` (for a filter list view of all comands) or `Command-Shift-.` (for a tree view of all commands).
12. **(Vertical) split views**: either 1, 2 or 3 vertical splits. (`Command-1`, `Command-2`, `Command-3`, and `Command-0` to switch between splits). Or use `Command-P` to get a preview split for various languages.

(All keyboard shortcuts mentioned here refer to the default keybindings. For Windows and Linux replace `Command` with `Ctrl`.)

 [1]: /features/edit-remote-files/
