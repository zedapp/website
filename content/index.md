Welcome to Zed
==============

### What does it look like?

<img src="/img/zed-screen-new.png" alt="zed-screen-new" width="1221" height="992" class="aligncenter size-full" />

### What is it?

Zed is a fully offline-capable, open source, keyboard-focused, text and code editor for power users. You can use Zed to edit *local files* as well as *remote files* on any server. Zed has all features you'd expect from a capable code editor:

*   Syntax highlighting for many programming languages (e.g. C, Clojure, CoffeeScript, C#, CSS, Dart, Erlang, Go, Haml, Haskell, HTML, ini files, Java, JavaScript, JSON, LogiQL, Lua, Markdown, Nix, PHP, Plist, Protobufs, Python, Ruby, Shell, XML)
*   Code completion: symbols, snippets and property/method completion.
*   Built-in linting for some languages with inline markers (JavaScript, CoffeeScript, JSON, Lua, CSS)
*   Multiple cursors
*   Split-view editing
*   Themes: light and dark themes out of the box and you can easily develop your own using CSS.

<iframe width="560" height="315" src="//www.youtube.com/embed/Rb8oQ5XHoLA" frameborder="0" allowfullscreen></iframe>

Zed is distributed in two editions: [a *Chrome App* and a standalone app][1].

### Why *another* editor?

Zed was not designed to be an *X* clone (although it borrows ideas from many). It has opinionated ideas on how to make *you* more productive editing code. Specifically:

1.  Zed tries to reduce [cognitive load][2] while editing code by *simplifying* as much as possible:
    *   Zed has *no* tabs and no concept of open files. You navigate between files either using the goto UI (`Command-E`/`Ctrl-E`) or file tree (`Command-T`/`Ctrl-T`). Switching between recent file is easy because recently opened files appear at the top.
    *   Zed has as little window chrome as reasonably possible: editors take up the full window space, minus a small bar along the top indicating what file is open.
    *   Zed *unifies* file navigation and file creation in its goto UI: you can either navigate to an existing file, or to a non existing file, in which case it will create the file including its parent directories (if necessary). As Zed will create any directories as required, you can just treat the path as a namespace.
    *   Zed has [first-class support for editing files on any Internet-connected server][3], so you no longer have to switch to nano or vi when editing files remotely, and swap in all the associated keybindings into your brain.
    *   Zed persists edit state between sessions: window size and location, recent commands, split view state, cursor and selections and even undo history are persisted between sessions in a `.zedstate` file stored in the project directory. This gives you peace of mind: not working on a project *right now*? Just close the window. Don't worry.
2.  Zed is built 100% using web technologies (HTML, JavaScript and pure CSS). Because it is [open source][4] (MIT licensed), you can inspect the DOM and change the code. Alternatively, you can write [extensions][5] (create new language modes, custom commands, key bindings, themes etc.) from within the editor without having to touch the Zed codebase at all.
3.  **Chrome App version bonus:** the Chrome App version of Zed has some extra useful features:
    *   Cross platform: Zed runs on any platforms that desktop Chrome runs on (including Chromebooks)
    *   Installation is easy with just a few clicks
    *   Settings are automatically synchronized between all computers logged into with the same Google account.
    *   Special "Notes" space is stored in Google Drive and synchronized between computers automatically as well.

[Click here to learn more about why we created Zed][6].

 [1]: /download
 [2]: http://en.wikipedia.org/wiki/Cognitive_load
 [3]: /features/edit-remote-files/
 [4]: https://github.com/zedapp/zed
 [5]: http://zedapp.org/2014/05/zed-package-manager/
 [6]: /vision
