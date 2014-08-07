The Changelog: v0.10.2
======================
date: 2014-04-08

Woah, the past week has been a huge week. On Tuesday [I announced that I would make working on Zed my day job][1] which resulted in a *lot* of attention. The number of active users exploded, as did participation on [Github][2] and the [Google Group][3]. A couple of new people contributed code to the project too, which is fantastic. I couldn't be happier!

I'm also happy to see that many of you already made the effort to contribute to the sustainability of the project by [donating weekly on Gittip][4]. We haven't nearly reached financial sustainability of the project, but it's encouraging!

I just pushed Zed version 0.10.2 to the [Chrome Store][5], which is a minor release in terms of features, but a big one in the amount of work that was done to work towards the promised standalone version. I suspect that this will be the last release before a version that will come in both a Chrome App and Standalone edition -- hopefully by the end of this week or early next week. Stay tuned!

Here's the [changelog][6] for 0.10.2:

*   Refactoring of Zed core codebase to use Architect plug-ins, making it easier to create the Zed standalone (without Chrome dependency) version.
*   New commands:
    *   `Help:Commands` (bound to F1 by default) gives you a context-sensitive list of all available Zed commands in your current mode, documentation for each command (if available) and current keybinding (by robru)
    *   `Tools:Document Statistics` gives some useful stats about your current document (word count, line count, character count etc.) (by robru)
*   Sandbox updates:
    *   Added sandbox commands to call goto and invoke arbitrary other commands (by robru)
    *   Added a "click" handler for the sandbox.
*   Language modes:
    *   Separate SCSS mode (by wpapper)
    *   Scala mode (by netzwerg)
    *   Mode is now set for files without a file extension based on Unix shebang line, e.g. #!/bin/bash uses bash mode (by robru)
*   Made configuration loading more robust, even if user.json contains JSON parse errors.
*   Minor fixes of the whitespace trimmer (by robru)
*   Indent on paste fixes (by TheKiteEatingTree)
*   Some minor updates to the manual (particularly the config.md documentation)

Thanks to all who contributed!

 [1]: http://zedapp.org/2014/04/zed-the-next-phase/
 [2]: https://github.com/zedapp/zed
 [3]: https://groups.google.com/forum/#!forum/zed-user
 [4]: https://www.gittip.com/zefhemel/
 [5]: https://chrome.google.com/webstore/detail/zed-code-editor/pfmjnmeipppmcebplngmhfkleiinphhp
 [6]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
