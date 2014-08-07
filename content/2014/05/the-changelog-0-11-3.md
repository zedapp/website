The Changelog: 0.11.3
=====================
date: 2014-05-14

This release contains some big infrastructural changes (primarily the switch from the `/tags` ctags file to using [IndexedDB][1] (a fast LevelDB-powered in-browser database) that will enable some cool language-intelligence features that will most likely be released as separate Zed packages in the near future. In addition, icons are now used in the symbol list and auto complete to signify whether they're functions, types, snippets etc. Some indexers (e.g. the ones for JavaScript and Go) now also includes arguments to functions in the symbol list.

![New symbols](/img/new-symbols.png)

Here's the full [changelog][3] for 0.11.3:

*   [ZeDB][4]: a simple abstraction layer on top of IndexedDB. Packages and other sandbox code can create their own data stores and indexes (via the `databases` key in configuration) and read, write and query that data quickly. This system is current primarily used for symbol indexing and code completion (see below).
*   Complete rework of generic project indexing system, now storing symbol information in IndexedDB for faster retrieval (than the `/tags` file in ctags format that it used to use).
*   Support for full function signatures and icons in symbol list (`Command-R`/`Ctrl-R`) and code completion for certain languages (JavaScript, Go, others still have to be updated)
*   General-purpose regex-based symbol indexer allows to add basic symbol indexing to modes without writing any JavaScript (see Go and JavaScript mode for examples).
*   Additional multi-cursor commands (`Cursor:Multiple:Add Above Skip Current` and `Cursor:Multiple:Add Below Skip Current` by thebishopgame)
*   Standalone:
    *   No longer crashes when an exception occurs
    *   Do not save window position for minimized windows (by nightwing)
*   Modes:
    *   New matlab mode (by timothyrenner)
    *   Markdown: disable strip whitespace (by robru)
    *   Handlebars mode (by chenxsan)

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
 [2]: http://zedapp.org/wp-content/uploads/2014/05/new-symbols.png
 [3]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
 [4]: https://github.com/zedapp/zedb
