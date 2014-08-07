The Changelog: 0.11.5
=====================
date: 2014-07-09

This release incorporates some of the findings in [How Zed is Actually Used][1] (specifically better support for popular Zed languages such as Python, Ruby and PHP). It also includes two new packages as part of the distribution: [follow-complete and bracket-check][2]. In addition, various bugs have been fixed and features tweaked.

Let's recap what follow-complete does:

> Follow complete is based on a few observations:
>
> 1.  A lot of languages use a `a.b` and `a.b()` (and similar: `a->b` and `a->b()`, `a::b`) notations for package namespacing, property access and method calling, e.g. JavaScript, Go, C++, PHP, Ruby, CoffeeScript, C#, Java, Dart, Groovy, Lua, Rust, Python, Scala etc.
> 2.  Programmers tend to name variables of certain types the same all over the code base: e.g. `arr` for arrays, `el` for HTML DOM elements.
> 3.  Many languages use the `a.b` pattern for namespacing, for instance in Python after you `import os` you call methods on it via `os.some_method()`. Even without explicit imports, `document.createElement()` is an example of this in JavaScript.
>
> If this is the case, wouldn't indexing any sequence of `x.y`, `x.y(...)`, `x(...).y` and `x(...).y(...)` found in a code base, result in some useful completions when requesting code completion after typing `x.`? In that case, code completions could include `y` and `y()`.
>
> This is exactly what follow complete does. It uses Zed's new database APIs to index sequences of identifiers with `.`s in between and uses that for completion. As it turns out, if your code base is big enough, this gets surprisingly useful.
>
> Again, here's a Go example. Go happens to use `.` as a package separator. Without any Go-specific knowledge, let alone knowledge of Go's APIs, Zed can now give the following completion for the `datastore` package (which is an Google App Engine specific package that is used fairly heavily in this particular project):
>
> <img src="http://zedapp.org/wp-content/uploads/2014/05/Screenshot-2014-05-22-15.19.13.png" alt="Screenshot 2014-05-22 15.19.13" width="491" height="171" class="aligncenter size-full wp-image-324" />
>
> As you can see, although Zed "knows" that these are all methods, it doesn't show method argument names, simply because it doesn't know them. Potentially these method names could be matched with the symbol list, perhaps to also give argument names. Nevertheless, even without that getting some completion for APIs that are used in your project is quite useful.

Follow complete is currently enabled for: JavaScript, Python, Ruby, Go, Java, C#, Groovy, Lua, Nix, Rust and Scala.

Now let's recap what bracket check does:

> There are many more language for which parser written in JavaScript are *not* yet available. And writing a high-quality parser for most languages is *a lot of work*.
>
> So would it be possible to build some syntax tooling that helps *at least a little* in detecting common mistakes writing code?
>
> This is what bracket check does: it checks nesting of brackets: e.g. `[{(`. Is this a full-blown syntax check? No (although... almost for Lisps), but it *helps*.
>
> For each language, you only have to configure two things: the bracket pairs to match and the parts to skip over (such as string literals, comments) etc. Here is it in action:
>
> <img src="http://zedapp.org/wp-content/uploads/2014/05/Screenshot-2014-05-22-15.27.24.png" alt="Screenshot 2014-05-22 15.27.24" width="473" height="116" class="aligncenter size-full wp-image-326" />

Here's the full [changelog][3] for 0.11.5:

*   Modes:
    *   Ruby: symbol indexing
    *   Python: improved symbol indexing
    *   C: symbol indexing
    *   PHP: improved symbol indexing
    *   Java: symbol indexing
    *   C#: symbol indexing
    *   GLSL syntax highlighting
    *   Stylus syntax highlighting
*   Two new packages made part of the default distribution:
    *   follow-complete: offers quasi-intelligent completions for `x.y` property accesses/method calls for many languages (currently enabled for JavaScript, Python, Ruby, Go, Java, C#, Groovy, Lua, Nix, Rust and Scala)
    *   bracket-check: checks matching brackes (currently enabled for Clojure, Go, Dart, Python, Ruby, Java, and C#)
*   Local (Chrome) directories with more than 100 files/directories did not show up completely before, this is now fixed (by farnoy)
*   Projects are automatically indexed (for symbols and code completion) the first time they are opened, you can do this manually with `Tools:Index Project`.
*   Search project now only searches known file types and does so more sequentially, which should prevent crashes
*   Key bindings:
    *   Default keybinding for `Find:Next` on Linux/Windows/ChromeOS is now `Ctrl-G`, and `Find:Previous` is now `Ctrl-Shift-G`.
    *   `Nativate:Reload Filelist` is now bound to `Command-Shift-L` on Mac and `Ctrl-Shift-L` on Windows/Linux/ChromeOS as well as `F5` on both.
*   Dotfiles (files starting with `.`) now appear in the file list, except those defined in `gotoExcludes` (by default `.git`)
*   Goto matching algorithm tweaked, now also does fuzzy matching again (although with a lower score).
*   File renaming fixes (by TheKiteEatingTree)

As always, if you have Zed installed, Zed should be upgraded automatically. If not, you can [download Zed from its download page][4].

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: http://zedapp.org/2014/06/zed-usage/
 [2]: http://zedapp.org/2014/05/language-agnostic-tooling/
 [3]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
 [4]: /download
