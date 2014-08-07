Why Zed?
========
Every "modern" code editor and IDE today (Sublime, TextMate, Atom, Eclipse, IntelliJ) works and looks more or less the same: you have a file tree on the left, tab bar at the top with open files, and if it's an IDE a bunch of additional panels, like "Outline", "Package browser" etc. To open a file you select it in the tree, make some changes and press `Command-S` or `Ctrl-S` to save.

Things haven't changed *that much*, the past years. Is this really the best we can do, or can we improve the status quo?

We believe things can be improved still. Zed is a project attempting to improving the way you work without making you feel *too* far outside of your comfort zone.

There are two ways Zed tries to do this:

1.  **Reduce cognitive load.** Programming is hard enough as it is. Worrying about juggling files, folders, local or remote, and panels and other distractions, are things we can do without.
2.  **Hackability.** The audience of a code editor is programmers. Programmers want to change things, extend things, hack on things.

## Reduce cognitive load

Here's some ways that Zed tries to reduce cognitive load while programming.

### No more open files and tabs

There are two reasons for the concept of "open files" represented as tabs in editors today:

1.  Tabs provide a quick way to navigate between a few files you're editing. This is nice in theory, but in practice the number of open files (represented as tabs) quickly become *unwieldy* and pretty soon you are unable to find the tab you're looking for. "Tab bankruptcy" is a common phenomenon where the only way out is to simply close all tabs and hope that the ones you needed resurface over time.
2.  Open files can be in a "dirty" state, i.e. they may have unsaved changes and this needs to be visible to the user. Zed argues that there is no good reason anymore for for files to be in a dirty state, ever. The days where saving to disk took a minute are over. Constantly saving files simplifies a lot of things and *good undo functionality* and version control can help in reverting a file to its previous state, even after saving or after closing and reopening a project.

**Zed** has no concept of open files (or tabs). You can navigate between files quickly and efficiently using its goto UI (`Command-E`/`Ctrl-E`), which sorts files based on date of last opening and can be used to quickly find the file you're looking for. Whether the file you're selecting is already in memory or is loaded from disk (or over the network) is completely transparent. Why would you care?

### Split views

As if managing tabs isn't difficult enough, there's also the issue of managing split views. Many editors support the most impressive window work of split editors. "Well, I have a big-ass monitor so I better use it by splitting it vertically in three, and then the middle pane in two horizontal ones, and the third into three so that I can see everything at once!"

If you ever used an editor with super flexible split view window docking, you at some point will have ended up in some insane configuration, where it became near impossible to navigate between editors without using the mouse, or without spending considerable time seeing in which pane (each with its own tab bar) you had opened that one particular file.

**Zed** has very limited split view configurations. You can have 1 editor, or 2 next to each other (and toggle their size between 50%/50% 33%/66% and 66%/33%), or 3 next to each other. There's also a 2-way split with a preview window on the right. That's it. Admittedly, initially the reason for this was simplicity of implementation, but after working this way for a year, there's really no reason to support more configurations. Limited flexibility in this sense frees your mind to think about what really matters.

![Zed splits](/img/zed-splits.gif)

### Minimal UI

Many editors today boast a "distraction free" mode. "Remove all the distracting chrome!" That's great, but when *do* you want all this distracting chrome?

Never.

It should always be you and your code, with as little chrome as possible. No panels, no tab bars, no file tree that takes up space constantly. Just as clean as functionally possible. If there's anything visible other than the code you're editing, there'd better be a damn good reason, that is either it gives you a sense of context (what file am I editing? Where am I within this file?) or it's a temporary UI element that I explicitly asked for (e.g. an open file dialog).

**Zed** has as little window chrome as reasonably possible: editors take up the full window space, minus a small indicator along the top indicating what file is open.

### Unifying file navigation and creation

[Notational Velocity][1] is a simple note taking app that unifies the concept of searching for notes and creating them. It has a three-part UI: at the top there's a "search" field, below it is the list of notes that match the search, and below that is the actual editor where you can scribble your notes. When you enter a search phrase that matches some note titles and press `Return`, it opens the note and puts the editor in focus. If you enter a search phrase that doesn't match a note and press `Return`, it creates a new note with that name and put the (empty) editor in focus.

**Zed** applies this approach to code editors. Its goto feature (`Command-E`/`Ctrl-E`) works the same way: You can use it to either navigate to an existing file, or to a non existing file, in which case it will create the file including its parent directories (if necessary). As Zed will create any directories as required, you can just treat the path as a namespace. And opening a *new* file is not at all different than opening an *existing* one.

![Navigation](/img/navigation1.gif)

### Editor state

Editor state should be preserved between editor launches. Life is hard enough as it is, if we have to keep editor windows open, because we're afraid we otherwise have to restore its state later on, that just makes life even harder.

**Zed** persists window size and location, recent commands, split view state, cursor and selections and undo history between sessions in a `.zedstate` file stored in the project directory. This gives you peace of mind: not working on a project *right now*? Just close the window. Don't worry.

### Where are my files located?

With this whole DevOps thing going on, people spend a lot of their time editing files in a virtual machine or remote server. All of a sudden, they have to use nano or vi, and completely swap out everything they know about the editor they use locally, and swap in the... interesting vi keybindings.

Even if you're a big nano or vi fan, this situation is not ideal since your preferences and customizations don't travel with you so you don't your tab size preferences and themes on those remote servers.

**Zed** has [very innovative support for editing files on any Internet-connected server][2] without the need to use WebDAV or (S)FTP. This means you can *always* use your local Zed editor with all your favorite customizations.

## Hackability

Many programmers like to be able to hack on their environment. They like to tweak things, add things, remove things. An editor can support this in two ways, and Zed supports both.

### Open source

The Zed core is completely open source (MIT licensed). You can fork the project and change whatever you want. It's all built using web technologies (HTML, CSS, JavaScript) so it's not all that complicated. Being open source is not about price, it's about flexibility. Even if you never have dive into the code, the idea that you *can* is comforting.

### Extensibility

However, if you don't have to fork your editor to make it do what you want, so much the better. That's why Zed has the ["Configuration" project][3]. This is configuration in the broadest sense of the word: in this project you can tweak preferences and keybindings, but the configuration project is also where all of Zed's language modes and themes are implemented. Indeed, features like language-specific code completers, symbol indexers, linters and all themes are implemented in the Configuration project "user-land" code. You can look at how everything is implemented and add your own custom Zed commands, language modes and themes as well.

And since the Configuration project is synced to Google Drive, all your extensions and preferences travel with you wherever you log in with your Google account.

 [1]: http://notational.net
 [2]: http://zedapp.org/features/edit-remote-files/
 [3]: http://zedapp.org/2014/02/configuration/
