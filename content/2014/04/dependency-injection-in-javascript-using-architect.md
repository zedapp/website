Dependency Injection in JavaScript Using Architect
==============
date: 2014-04-11

[Architect][1] is an open source dependency-injection framework for both server and client-side JavaScript code. Wikipedia defines [dependency injection][2] as follows:

> Dependency injection is a software design pattern that implements inversion of control and allows a program design to follow the dependency inversion principle.

Very impressive. The way I think of it -- at least in Architect's implementation -- is simply as *dynamic imports*. Whereas usually you import (or `require`) a *specific* module by listing its path, dependency injection allows you to postpone the decision which module to load until run time.

Why is this useful? Here's a few reasons:

1.  Testing: it becomes easy to test modules if you can easily switch out imported modules with mock implementations.
2.  The module to pick may depend on the context in which the application is run (e.g. arguments passed upon launch, or the runtime environment).

The second is the reason I recently refactored Zed to use Architect as part of the effort to offer both a [Chrome App and a node-webkit based version][3].

What does such a refactor entail? Essentially it means turning require.js modules into Architect plugins.

### File systems

Here's roughly what Zed's require.js modules looked like *before*:

    define(function(require, exports, module) {
        var fs = require("./fs/local");
        module.exports = {
            method1: function() {
                fs.readFile("/.zedstate", function(err, content) {
                    // Do something useful
                });
            }
        };
    });


If you know a little bit about Zed's feature set you can spot the problem with this pseudo module: Zed supports *many* types of file systems and this ties our module to one in particular. Currently Zed supports:

*   A [RESTful HTTP file system][4] (used for editing remote files)
*   A [local file system][5] (using Chrome's APIs) for editing local folders
*   A [dropbox file system][6] for editing files on Dropbox
*   A [file system that syncs to Google Drive][7] (using Chrome's SyncFS APIs) used for the Notes and Configuration projects.
*   A [read-only static file system][8] that reads files from the application bundle (used for the manual project)
*   A [node.js-based file system][9] for accessing local folders (for node-webkit)
*   A [union file system][10] that combines any of the above (used for the Configuration project)

Clearly, a `require` call to any particular file system module makes our module immediately dependent on a particular file system implementation. Even wrapping the `require` in an if-statement wouldn't scale, since there are quite a few options.

Alright, so now let's have a look at the Architect version, which is only slightly more verbose:

    define(function(require, exports, module) {
        plugin.consumes = ["fs"];
        plugin.provides = ["mymodule"];
        return plugin;

        function plugin(options, imports, register) {
            var fs = imports.fs;
            var api = {
                method1: function() {
                    fs.readFile("/.zedstate", function(err, content) {
                        // Do something useful
                    });
                }
            };
            register(null, { mymodule: api });
        }
    });


Rather than exporting the API immediately, the module now exports a single function `plugin` that takes three arguments:

*   `options`: containing any options for the plugin.
*   `imports`: containing a key with the API of each consumed service
*   `register`: the function to be called to register the services provided by the plugin.

In addition, two properties are tacked onto the `plugin` function object:

*   `consumes`: an array all services that this plugin relies on. Note these are symbolic names, not module paths.
*   `provides`: an array of all services that this plugin implements and exposes.

Note that all the `require`s are gone and have been replaced by "consumed services." The `plugin.consumes =` line says "this plugin [module] requires a service named 'fs' to function." Any other plugin that `provides` the "fs" service can now be *injected* here, as long as the interfaces match. As you can [see in Zed's codebase][5] all file system plug-ins expose *exactly* the same methods and all `provide` the `fs` service.

So, how does an `fs` service get injected? That's Architects job, the plugin doesn't have to worry about it. In practice, the way this works is that the project to be opened is encoded in the URL passed to the `editor.html` page that hosts the editor. Based on the request parameters [a piece of code figures out][11] which plugin providing the `fs` service is to be loaded. More on composing plugins into applications later on.

### Runtime-specific APIs

Switching out file system modules is just *one* useful application of Architect in the implementation of Zed. Another one is abstracting from APIs specific to the runtime environment.

As I mentioned, the challenge was to get Zed to run *both* as a Chrome App as a node-webkit app. Each of these provide certain APIs (e.g. to get access to the local file system, window management, etc.) that are different between the runtimes. The way this is solved in Zed is by wrapping these APIs in Architect plug-ins that have two implementations: one for Chrome and one for node-webkit.

A clean example of this are the `window` plugins for [Chrome][12] and for [node-webkit][13] (note the consistent use the `.chrome.js` and `.nw.js` filename patterns to make clear that these plugins are runtime specific). Both these plug-ins implement the same methods:

*   `close()` to close the current window
*   `create(...)` to create a new window
*   `fullScreen()` to toggle full-screening the window
*   `maximize()` to toggle maximizing a window

etc.

Any plugin that consumes the `window` service provided by this plug-in will now call into the runtime-specific implementation. Examples of this include the [title bar][14] and [project picker][15].

Pretty cool right?

### Putting it together

So, how do we compose multiple plug-ins into an application? For this we use a plugin list. In its most basic form:

    var plugins = ["./mymodule", "./fs/local"];

    architect.resolveConfig(plugins, ".", function(err, config) {
        architect.createApp(config, function(err, app) {
           // At this point we have an instantiated application
           var mymodule = app.getService("mymodule");
           mymodule.method1();
        });
    });


In essence you specify a list of plug-ins to load and then create an application out of them, which will link them all up. Now, replacing `./fs/local` with `./fs/sync` would switch `mymodule` to another file system implementation, without having to change the file at all.

However, in practice, almost all file system plug-ins require extra arguments. These can be passed by not using the plain-string notation, but the object notation, e.g.:

    var plugins = [
        "./mymodule",
        { packagePath: "./fs/local", dir: "/etc" }
    ];


The `packagePath` contains the require.js module that contains the plug-in (as before), and any other provided options are passed into the plug-in via the `options` argument to the `plugin` function.

And that's pretty much everything there's to it! For some examples of real world architect plugin lists and instantiations, have a look at [boot.js][16] (for the editor windows) and [open.boot.js][17] (for the project picker). Both of these build up a list of plugins that are laregely shared, but add some plugins based on the runtime environment (based on the `isNodeWebkit` variable).

### Caveats

Something to be aware of using Architect:

Plugins cannot have circular dependencies, i.e. plugin 1 cannot depend on a service provided by plugin 2 if plugin 2 depends one one provided by plugin 1, even if this happens indirectly. If you do this you get obscure errors. The way I've been working around this is by assigning the resulting architect application to a global, and then calling `getService("servicename")` on that global.

For instance, I instantiate the application this way:

    architect.resolveConfig(plugins, ".", function(err, config) {
        architect.createApp(config, function(err, app) {
            window.zed = app;
        });
    });


Then, elsewhere in some plugin that doesn't have an explicit dependency on service `A` (listed under `consumes`) I call `zed.getService("A")` to get a reference to it anyway. Clearly, this is a bit ugly, but you need it sometimes.

Second: *always call `register()`* as soon as posisble. If you don't call register() at all, your application will never load -- every plugin has to call it. Also, if you wait with calling `register` too long, everything else is waiting for it, resulting in a poor user experience.

If you keep these two things in mind, you should be golden.

### Do I Need Architect?

So, does every application need [Architect][1]? Probaby not. However, for applications of a certain size, and applications that need to be loaded in different configurations, it can be very useful. So evaluate its value for your application specifically.

Architect was developed largely by [Tim Caswell][18], back when we both worked at [Cloud9][19]. Cloud9 these days uses it both for their node.js back-end and their client-side too. Another former Cloud9 colleague gave [some talks about Architect that also give a good introduction][20].

### About Zed and this Blog Post

[Last week I announced][21] I would make working on Zed my day-time job. Zed was open source before, and I kept it that way. In addition to the openness in *code* I also want to be open in design decisions and other lessons learned during this endeavor. This post is one example of that: it shows how Zed gets value out of Architect, but it's potentially useful for any JavaScript developer. Do you want to support me in working in this open way? [Consider contributing on Gittip][22].

**Unrelated post script:** This post was written and edited on a Chromebook running Zed in Vim mode, using the Notes project that's automatically synced with my other computers. *And it was a great experience.*

 [1]: https://github.com/c9/architect
 [2]: http://en.wikipedia.org/wiki/Dependency_injection
 [3]: /download
 [4]: https://github.com/zedapp/zed/blob/master/app/js/fs/web.js
 [5]: https://github.com/zedapp/zed/blob/master/app/js/fs/local.js
 [6]: https://github.com/zedapp/zed/blob/master/app/js/fs/dropbox.js
 [7]: https://github.com/zedapp/zed/blob/master/app/js/fs/sync.js
 [8]: https://github.com/zedapp/zed/blob/master/app/js/fs/static.js
 [9]: https://github.com/zedapp/zed/blob/master/app/js/fs/node.js
 [10]: https://github.com/zedapp/zed/blob/master/app/js/fs/union.js
 [11]: https://github.com/zedapp/zed/blob/master/app/js/fs_picker.js
 [12]: https://github.com/zedapp/zed/blob/master/app/js/window.chrome.js
 [13]: https://github.com/zedapp/zed/blob/master/app/js/window.nw.js
 [14]: https://github.com/zedapp/zed/blob/master/app/js/title_bar.js#L50
 [15]: https://github.com/zedapp/zed/blob/master/app/js/open.js#L49
 [16]: https://github.com/zedapp/zed/blob/master/app/js/boot.js
 [17]: https://github.com/zedapp/zed/blob/master/app/js/open.boot.js
 [18]: http://creationix.com/
 [19]: http://c9.io
 [20]: https://www.youtube.com/watch?v=QzSoHMnvSB0
 [21]: http://zedapp.org/2014/04/zed-the-next-phase/
 [22]: https://www.gittip.com/zefhemel/
