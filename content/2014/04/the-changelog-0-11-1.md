The Changelog: 0.11.1
=====================
date: 2014-04-23

This is the first update to be pushed for both the Chrome and Standalone version, so we'll be finding out if auto-update works in the standalone version!

Before we get to the changes in this release, a little update on the funding situation. Last time we crossed the $100/week mark on [Gittip][1] and there is has been some growth, but not that much -- we're currently at $108/week, which is still way off from making this project sustainable. So, if you're a Zed user, [consider buying][2]!

Both the Chrome and Standalone version should be upgraded automatically. If you somehow can't wait for the standalone version to self-update, feel free to download it again from the [download page][3].

This release saw even more growth in community contributions. I'm very excited about this -- Zed is really becoming a team effort.

Here's the [changelog][4] for 0.11.1:

*   New auto save (which should be friendlier for people using build systems with file watchers). The new version *always* saves when switching between splits and files and when the editor loses focus. What's new is the ability to switch off timed saves (set to `saveTimeout` to 0 to disable).
*   Commands to move splits around: (`Split:Move To *`)
*   New splits now receive focus automatically
*   Version number now appears in project picker
*   Fixes to file tree (by eltuerto)
*   Sandbox messages now appear in zed::log for standalone version
*   Configuration now uses [JSON5][5] format (which supports comments etc.)
*   Fix to trim remote URLs when pasting (by surma)
*   ZPM auto update fixes
*   Scroll past end preference (`scrollPastEnd`) (by TheKiteEatingTree)
*   Modes:
    *   PHP mode now includes a parser and reports parse errors
    *   Livescript mode (by maninalift)
    *   Groovy mode (by calebmpeterson)
    *   JSX mode
    *   Improved Markdown preview styling (by ghotsla)

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: https://www.gittip.com/zefhemel/
 [2]: /buy
 [3]: /download
 [4]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
 [5]: http://json5.org/
