The Changelog: 0.11.4
============
date: 2014-06-16

This release has some solid improvements for its Goto feature (whose matching algorithm was improved and now also searches symbols by default) and project-wide search (with case insensitive and regex support and support for only searching files matching a file pattern) as well as some other, more minor changes that should smoothen the experience.

Here's the full [changelog][1] for 0.11.4:

*   Goto improvements:
    *   Goto (Ctrl-E/Command-E) now also includes matches from the symbol index (without having to use the `:@` or `@` prefix)
    *   New fuzzy matching algorithm:
        *   Now also searches file directory names by default.
        *   Character sequences now have to match exactly, spaces can be used as wildcards. E.g. "bcd" matches "abcde" but not "abccde", however "bc d" will match "abccde".
        *   Scoring is now based on how close the pattern match is to the end of the path, the closer to the end, the higher the score. This favors file name matches over directory name matches, which is usually what you want.
*   Project search improvements:
    *   Now integrated into goto (Ctrl-Shift-F/Command-Shift-F)
    *   New query syntax: `searchphrase [-flags] [filepath pattern]` for example: `hello` or `hello *.js` or `hello -i` (case insensitive search) `he*llo -ie /docs/*.md` (case insensitive regex search). Supported flags: `-i` (case insensitive matching) and `-e` (regex match).
*   Batched undo: you no longer have to run undo for every character, certain operations (including typing and deleting) are now batched up.
*   Better behavior when "closing" a split (going from 2 to 1 splits): the split left will now contain the file in the active split.
*   Bug fix: Fix window positioning after restore
*   Bug fix: Better recovery from broken configuration
*   Bug fix: No longer show stacked "file changed" dialogs for each change
*   Sandbox API:
    *   `zed/http` API now also has POST, PUT, DELETE etc. support and returns not just content, but also headers (by akoenig)
    *   `zed/preview` API now supports opening the preview split (by akoenig)
*   Mode:
    *   Clojure/ClojureScript mode: symbol indexing and better indenting

As always, if you have Zed installed, Zed should be upgraded automatically. If not, you can [download Zed from its download page][2].

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
 [2]: /download
