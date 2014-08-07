The Changelog: 0.12.1
=====================
date: 2014-08-01

This release has a [much improved flow for editing files remotely using zedrem][1]. Rather than having to copy and paste URLs every time, you can now pass in a user-specific key to the zedrem command and windows will automatically open up when you use zedrem. See the [Edit Remote Files page][2] for updated instructions. Note: if you already downloaded the zedrem binary onto a server before, be sure to redownload it to get these new features.

*   Zedrem: The `zedrem` binary now takes an optional `-key` flag where the user key can be passed in. This key is automatically generated (see below) and can be requested using the `Configuration:Zedrem:Get User Key` command. When passed in, edit windows will automatically appear when you run zedrem.
*   Zedrem: the `~/.zedremrc` file (that is: the .zedremrc file in your $HOME directory) has been extended to have a `userKey` entry in the `[client]` section, this is useful if often editing files on the same server and not wanting to pass in the user key every time.
*   To support the above there is now a `zedrem` preference in the Configuration (under preference). By default a server is configured there (remote.zedapp.org over SSL) and a `userKey` generated. The project picker will establish a persistent websocket connection with this server to enable the behavior described above.
*   Zedrem: ownership of files is now preserved.
*   Modes:
    *   Improved C++ symbol indexing (by cessen)
*   Key bindings:
    *   Mac: Alt-Delete now added as alternative to Alt-D (by 11684)
*   Zed now works on the Chrome Beta channel again (Chrome 37)
*   Symbols are now listed in order that they appear in files, rather than based on length.
*   Mutliple cursor bug fixes: moving and copying lines up and down now works with multiple cursors, as does whitespace trimming.
*   Standalone: no more crashes with the splash screen.

 [1]: http://screencast.com/t/Lrk2BIUnD
 [2]: http://zedapp.org/features/edit-remote-files/
