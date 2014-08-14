The Changelog: 0.13.0
=====================
date: 2014-08-14

Big new features in this release:

1. Github support: Support for opening, editing to Github repositories without the need to clone them -- right from Zed ([screencast of this feature in action](http://screencast.com/t/Hezpqnqt1n)).
2. Embedded web server: serve (static) files right from Zed (run `Tools:Static Server:Start`).
3. Zedrem change: current Zedrem users using last version's userKeys: user keys are now no longer stored in the Configuration project, but instead in a token store. Your user key will have changed. For details, see below.

Here's the full list of changes:

* Github support: There's now a "Open Github Repository" item in the project picker. The first time you'll click it it'll ask you to create a Github token that it'll save (outside the Configuration project). After this a repository picker will appear, but you can also paste in full Github urls immediately. After picking a repo it'll ask you to pick a branch to edit.
    * Changes made to a Github project are saved locally on your machine into an IndexedDB database only. To commit the changes to Github, use the `Version Control:Commit` command (also available in the "Tools" menu if you have menus enabled).
    * You can reset any changes you made locally using the `Version Control:Reset` command.
    * You can create a branch (that'll open in a new window) using `Version Control:Create Branch`.
* Zedrem: configuration changes:
    * the "zedrem" key under preferences in the Configuration project is now _ignored_, you can remove this key safely.
    * User keys are now stored in a token store (as are the Github tokens), to retrieve your zedrem userKey run the `Zedrem:Get User Key` command.
    * If you like you can generate a new user key using `Zedrem:Generate New User Key`, a Zed restart will be required for this change to take effect.
    * The project picker now shows the status of your connection to your selected zedrem server at the bottom of the screen.
* Embedded Web server -- serve files right from Zed (works both in Chrome App and Standalone): this is available both as sandbox API (so you can implement your own servers -- see [zefhemel/zcms](https://github.com/zefhemel/zcms) for an example) and with a default static file server you can run out of the box.
    * Start static file server using the `Tools:Static Server:Start` command, this will also automatically open your browser. A port is automatically assigned.
    * Stop static file server using `Tools:Static Server:Stop`. The server will also automatically stop when you close your editor window.
* Drag and drop of binary files: this is not an advertised feature at all, but you can actually drag and drop files onto a Zed editor window and it'll "upload" them to your project. This now also works correctly with binary files, such as images.
* Currently open files (open in some split) will now appear in your Goto file list (although at the very bottom), Zed will do some session switcharoo to make this work correctly.
* Modes:
    * Improved C++ symbol indexing support (by cessen)
    * Dockerfile mode (syntax highlighting only)
    * Ruby: behavior support (auto-inserts matching braces etc.)

Also: did you know this site is now hosted on S3 and generated using the ZCMS Zed Package? See [the zedapp/website repository](https://github.com/zedapp/website) for source files.
