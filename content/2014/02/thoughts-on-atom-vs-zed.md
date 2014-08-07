Thoughts on Atom vs Zed
=======================
date: 2014-02-27

So, [Atom happened][1], github's web tech-based code editor. I have an Atom invite and I played around with it a bit today and it's an interesting project -- and with the weight of Github behind it, definitely not something to ignore.

Of course, as the author of Zed I have to ask: how does Atom compare to Zed, and is there any reason for Zed to exist anymore? In this post I'll try to compare and contrast the two a little bit based on what I've learned so far. Of course, all of this is somewhat biased, but I try to abstain from criticism at the level of "WHY COFFEESCRIPT!? COFFEESCRIPT SUCKS!!1"

### Web technology

Both Zed and Atom observed that web technology is a great way to build a hackable editor, and that a web tech stack doesn't need to live in a web page. In Zed's case it's a [Chrome app][2] (and available for Mac/Windows/Linux/ChromeOS) -- although *spoiler alert* I have a branch with a [node-webkit][3] prototype for Zed too --- in Atom's case it's a native app based on a forked version of node-webkit, currently only on Mac, but I'm sure with at least a Windows version is not far off. Zed is built using HTML, pure CSS and JavaScript. Atom is built using HTML, [Less][4] and [CoffeeScript][5].

Atom is, due to its strong ties to node.js APIs, less portable than Zed. Zed currently runs as a Chrome app, and in prototype-form as a node-webkit "native" app. But it's easy to also make it work as a regular web app, if need be, or as a Firefox App if that ever becomes a thing. That said, of course, getting access to node.js directly allows the editor to do anything node.js can do (= basically anything) and Chrome or web apps can't.

### UI/UX

Zed has the explicit goal of [doing things differently][6] regarding the concept of open files and tabs (or lack thereof), minimalism in UI, unifying file opening and creation, and remote file editing. Atom basically looks like sublime: file tree on the left, tab bar along the top, and borrows features like goto and the command panel from Sublime and Textmate too (Zed does too, but has tweaked the way goto works). Atom is more "traditional" UX-wise, which is a perfectly legitimate choice.

### Feature set

I'm not going to do a feature-by-feature comparison. Let's say that Zed and Atom are relatively close in terms of feature set. Atom is probably stronger in terms of find and replace support (regex support, find and replace in project). Zed is stronger in language support (extensible code completion, inline markers for linters, symbol indexing, code formatters etc.) and remote file editing. The reason for Zed's language support focus is obvious, [considering where I came from][7] and you can expect more features in this area in the future.

Since both are extensible editors, my response to any missing feature in Zed can be "well, just fork the project and add it, or create an extension" and Github will say "well, just write an extension."

### Extensibility

From the beginning the ability to extend Zed (beyond forking the code) has been high priority for Zed, however being a Chrome app limits its flexibility a bit. If you want to use Chrome APIs like getting access to the local file system, you need to [run in a "safe" mode][8] that does not allow a lot of things like eval'ing arbitrary (user) code. Therefore, in Zed, all extension code lives in a sandbox in a separate process. Zed exposes [APIs][9] to the sandbox to do certain things like using basic UI elements, getting access to files etc. Zed extension points are designed in advance and not accidental. Zed provides specific extension points to extend its built-in code completion, symbol indexing, linting etc. support. There are (currently) no APIs to make arbitrary changes to the DOM, listen to arbitrary events etc. Zed may eventually get these features, but they have to added explicitly.

However, putting extension code in a sandbox has two advantages:

1.  Extensions can interfere with the main process in limited ways, it's difficult to make the main editor crash as a result of poor extension code, and because the sandbox lives in a separate process, performing CPU intensive tasks also does not slow down the editor.

2.  It is easy to reload extension code without having to reload the whole editor (by simply killing the sandbox and restarting it). As a result, extensions can be developed without having to relaunch Zed, but just by resetting the sandbox.

Atom extensions as far as I can see, get full access to about everything: the DOM and all CoffeeScript/JS APIs. This provides a lot of flexibility, and as a result a more significant part of Atom is built as extensions compared to Zed. For instance, [auto completion][10] is not a built-in Atom feature, but built as an extension. The question is how extensions will interact, for instance if I want to add a JavaScript-specific auto completer. I suppose the autocomplete Atom extension would need to provide an API somehow (couldn't find how, or if this is supported). In Zed, code completion is a core feature and provides handlers to plug in to, to do this -- which how the [word][11], [ctag symbol][12] and [snippet completers][13] are implemented.

However, since all code in Atom is loaded into the same JavaScript VM, reloading involves reopening windows to see the results during extension development -- at least, as far as I can see. And poor extension code, can completely screw up the editor.

Atom has `apm`, a package manager (from the looks of it, based on [npm][14]) to easily install, upgrade, remove and publish extensions. Very cool stuff. Zed has no such feature yet, [although it's coming][15].

### Licensing and cost

How Atom will be distributed once it leaves beta is not 100% clear. Most likely it will be free, but not open source with some sort payment model attached. Github is trying to find a balance between the ability to earn money on the product, while still [open sourcing][16] as much as possible. Zed is [100% open source, MIT licensed][17].

 [1]: http://atom.io
 [2]: https://chrome.google.com/webstore/detail/zed-code-editor/pfmjnmeipppmcebplngmhfkleiinphhp
 [3]: https://github.com/rogerwang/node-webkit
 [4]: http://lesscss.org
 [5]: http://coffeescript.org/
 [6]: http://zedapp.org/vision/
 [7]: http://zef.me/3881/post-phd-plans-cloud-9-ide
 [8]: http://developer.chrome.com/apps/contentSecurityPolicy
 [9]: https://github.com/zedapp/zed/tree/master/app/config/api/zed
 [10]: https://github.com/atom/autocomplete
 [11]: https://github.com/zedapp/zed/blob/master/app/config/default/command/text_completer.js
 [12]: https://github.com/zedapp/zed/blob/master/app/config/default/command/ctags_completer.js
 [13]: https://github.com/zedapp/zed/blob/master/app/config/default/command/snippet_completer.js
 [14]: http://npmjs.org
 [15]: https://github.com/zedapp/zed/pull/90
 [16]: https://github.com/atom
 [17]: https://github.com/zedapp/zed
