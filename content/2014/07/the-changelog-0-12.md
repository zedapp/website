The Changelog: 0.12
===================
date: 2014-07-17

This is a big release, both internally (the whole code base has been refactored to use [ES6-promises][1] instead of node.js-style callbacks) and externally: there's now an optional "traditional" UI mode that shows you a persistent file tree on the left and a menu bar along the top. In addition, there's now a basic UI for managing snippets. Let's look at each of those individually.

## UI Layout Picker

The first time you run Zed 0.12 you'll be greeted with the following pop-up:

![Zed UI Layout](/img/zed-ui-layout.png)

This seems a bit contrary to the [Zed vision][2], right? Offering a "cluttered mode." The reason for offering it anyway is that:

1.  Some people just really like to have a file tree available at all times. It gives them a sense of context.
2.  Other people are completely confused by Zed's minimalist UI. They open an editor and then have no idea what to do (even though there's a little `zed::start` doc that tries to explain it) -- there's no file tree, no menu. Now what?

So, for those people -- you can now make Zed look like this:

![Zed traditional](/img/zed-traditional-2.png)

The menu bar is a curated (hardcoded) collection of commands that I think most people need or would like to know about. Ideally, you quickly learn the keyboard shortcuts (listed in the menu) and then disable the menu again, but hey... maybe it doesn't take *that* much space.

![Zed menu](/img/zed-menu.png)

## Snippets Manager

From early on people have had problems creating their own snippets and understandably so. Therefore I developed a package ([zedapp/snippets][3]) to make this easier. With a file active in a mode you want to manage snippets for run the `Snippets:List` command:

![Zed snippets](/img/zed-snippets.png)

This will list existing snippets, add new ones and allows you to edit, and remove them (if not built-in). There's also a `Snippets:Add` command to immediately add a new snippet for the current mode.

## Full changelog

*   First-run screen that asks you to pick a UI layout. This is fully configurable later on, via:
    *   New `persistentTree` preference that, when enabled, shows a file tree along the left.
    *   New `showMenus` preference that shows a menu along the top with a (curated) list of common commands (and their key bindings).
*   Snippet manager (`Snippet:List`, `Snippet:Add`) shows and adds snippets to the mode of the currently active session.
*   `File:New` command (bound to `Command-N`/`Ctrl-N`) that opens the Goto UI with the directory of the currently active file prefilled.
*   ZPM and Snippet manager use special "Zed UI" Ace mode that highlights "buttons" more like buttons, so you can tell they're clickable.
*   Language modes can now have a `completionTriggers` key with characters that should automatically trigger code completion, e.g. `.` for JavaScript or `->` for PHP. And as a result...
*   Code completion now automatically triggers after typing a `completionTriggers` sequence of characters (this can be switched on/off with the `autoTriggerCompletion` preference).
*   Big Manual overhaul
*   Modes:
    *   Scala symbol indexing
    *   PHP follow complete support
    *   Clojure follow complete support
    *   Gherkin mode (by lalomartins)
*   Themes:
    *   Base16 theme (by farnoy)

Enjoy the release!

Want to contribute to Zed's development? [Consider buying][4].

 [1]: http://www.html5rocks.com/en/tutorials/es6/promises/
 [2]: /vision
 [3]: https://github.com/zedapp/snippets
 [4]: /buy
