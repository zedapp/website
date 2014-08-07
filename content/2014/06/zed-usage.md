How is Zed Actually Used?
=============
date: 2014-06-27

A few releases back, Zed added opt-in analytics. Upon first launch, Zed asks the user whether he's ok sending some anonymous usage data to further improve Zed. It has been about two months since this release, so it's time to share some results.

Of course, there's no way of telling how many people have *not* opted into the analytics, so total numbers don't say much. However, presumably percentages give some indication how Zed is used.

## Zed Chrome vs. Standalone

As of version [0\.11][1] Zed comes in two editions:

1.  Zed Chrome, the Chrome App installable (and discoverable) via the Chrome Web Store, available for all platforms that Google Chrome runs on.
2.  Zed Standalone, based on node-webkit, available for Mac, Linux and Windows.

At various points in time, [features have been discussed][2] that would need to introduce APIs (such as running CLI commands from sandbox code) that would only be implementable in the *standalone* version of Zed. Therefore, it's interesting to see how many users would be impacted if we'd start adding features that only work in the standalone version.

Based on data from the past two months, it turns out **79%** of Zed usage comes from the Chrome App. Note that this is not just counting launches but all events -- meaning that "real" usage counts more towards this percentage than a single launch.

The question is: Why is the Chrome App so much popular? I can think of a few reasons:

1.  The Chrome App is promoted in the [Chrome Web Store][3] which brings in a lot of new users that otherwise would probably never had heard of Zed.
2.  The Chrome App has been around longer and people haven't switched.
3.  The Standalone version seems to have some unexplainable [power consumption issues][4], at least on Mac.
4.  The standalone version does not have automatic configuration syncing, nor the syncing Notes project, nor Dropbox support.
5.  The standalone version does not run on Chrome OS.

A few of these can be further investigated. For instance, option 4 includes Dropbox support and the Notes project. Are those heavily used features? We have some data on that. Here are the used "file system types" ranked by usage:

![Zed FS types](/img/zed-fs-types.png)

Translation of the names used:

*   `local` is Chrome's Local Folder file system implementation.
*   `config` is Chrome's syncing Configuration file system.
*   `node` is the Standalone version's node.js-based local file system.
*   `manual` is the Manual project,
*   `syncfs` is the syncing Notes project (Chrome only).
*   `http`/`https` is remote editing of directories using `zedrem`.
*   `nwconfig` is the Standalone version of the Configuration project.
*   `dropbox` is the Dropbox file system (Chrome only).
*   `textarea` is the new "Edit in Zed" feature (Chrome only).

From this we can see that editing of local folders (`local` + `node`) accounts for 57% of all projects being opened. Chrome-specific features (Notes and Dropbox support) add up to about 10%, which isn't huge but still significant. Whether or not people choose the Chrome version for this reason -- they at least use it.

## Language Modes

Zed has syntax highlighting support for many different languages. In addition, for some languages it has language-specific features, such as integrated syntax checking, linting and code beautification. However, does that impact usage? What languages do people use Zed for where language-support can be further improved?

Here are the top 10 most popular language mode by usage:

![Zed popular languages](/img/zed-popular-languages.png)

Zed's most advanced language mode is JavaScript, and indeed, that's topping the chart. More surprising are "text" and "markdown". Markdown mode has syntax highlighting and preview support, but could be further improved. Also when you open a new project with Zed a `zed::start` document shows that uses `markdown` mode, so that may skew the results. Interesting items on this list are PHP, Python, C, and Ruby. PHP has a syntax checker, but Python, C and Ruby don't have very good language features yet. Definitely something to work on in further releases.

## Goto vs the File Tree

Zed has championed its Goto functionality. It grows out of the belief that the "type a few characters in a search field" way of navigating files is better than using a file tree. Nevertheless, Zed still features a file tree, although it's not always visible. So, what are users actually using?

Based on data collected, it appears that in Zed **87%** of the time Goto is used to navigate between files. Note that this doesn't prove that Zed made the right call, just that users use Zed the way it was intended.

## Popular Commands

Zed is command based, commands can be bound to keys, but also be executed by name. Naturally, most commands are executed through a key binding (e.g. you use the `Up` key rather than executing the `Cursor:Up` command manually), but commands can be executed by name too. It's interesting to see what commands are commonly executed by name -- because they're worth assigning a keyboard shortcut to.

Here's the top 10:

![Popular commands](/img/zed-popular-commands.png)

Three of these `File:Rename`, `File:Delete` and `Navigate:Reload Filelist` are file-management related commands. I use these three myself too, although I bound the latter to a key in my own configuration. `Navigate:Reload Filelist` is an annoying one. It's a command that ideally you'd never have to execute manually, Zed should just detect changes itself. Sadly, in practice this is hard to do without rescanning your whole file tree (potentially huge) every minute or so (and is every minute even enough?) as there's no way to "watch" a directory tree at an OS level (at least not in most file systems Zed supports, such as the HTML5 based local file system used in Chrome).

## Operating Systems and Geography

What operating system do most Zed users use? Here's the list:

1.  Windows: 42%
2.  Mac: 16%
3.  Linux 64-bit: 16%
4.  Chrome OS: 15%
5.  Other: 11%

Time to pay attention to all those Windows users, for sure. Also, there's a significant number of ChromeOS users, which I find intriguing. It'd be interesting to further investigate how ChromeOS users use Zed, because most likely they don't use the ability to edit local folders -- because there are none (other than the Downloads folder).

And just for fun -- here's the geographic distribution of Zed users:

![Zed user map](/img/zed-map.png)

![Zed user countries](/img/zed-countries.png)

This begs the question: People of Greenland -- y u no use Zed?

## Actionable items

So, what do we do with this information? Here's a few action items, at least for me:

1.  Test every release on Windows, since this is how the largest percentage of users will experience Zed.
2.  Explore what new features can be added to the following language modes:
    *   markdown/text
    *   PHP
    *   Python
    *   Ruby
    *   C
3.  See what keyboard shortcuts can be assigned to reloading the file list and renaming a file.
4.  Write up a blog post about effective ways of using Zed on ChromeOS.

 [1]: http://zedapp.org/2014/04/the-changelog-v0-11-first-standalone-release/
 [2]: https://github.com/zedapp/zed/issues?state=open
 [3]: https://chrome.google.com/webstore/category/apps
 [4]: https://github.com/zedapp/zed/issues/311
