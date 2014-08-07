Zed Package Manager
===================
date: 2014-05-15

A while back we added a very cool feature to Zed called ZPM, which we never advertised. As you may have guessed it stands for "Zed Package Manager" and the first implementation was done by [Andrew Stephan][1].

While ZPM will likely be dramatically improved in the future, let me lay out how it works right now: how to install and manage packages and how you can create your own packages that extend the functionality of Zed.

Let's start with installing and managing.

### Installing and Managing Packages

Installing a Zed package is straight forward, all you need is a copy of Zed (duh) and the URI of the packages you want to install (more on this URI later).

To see what packages are currently installed, run the `Tools:Zpm:Installed Packages` command from an editor window, this will open up a session listing all currently installed packages as well as the ability to uninstall, update, update all and install new packages. This list uses a regular Zed file as user interface, you can operate it with the keyboard (by moving your cursor to a "button" and hitting `Enter`) or mouse (by clicking on a "button"). Note that packages that come preinstalled with Zed can not be uninstalled (they have an uninstall option, but this will have no effect).

To install a new package hit the "Install New" button. Alternatively, you can run the `Tools:Zpm:Install` command (from anywhere, doesn't need to be from the installed packages view). Then, enter the package URI. A simple package (that we'll developer later in this post) you can try is `gh:zefhemel/sample-zed-package` After installation completes you should now have a new `My Test Command` command that says "Hello world" when you run it.

Awesomeness.

Zed's package ecosystem is fully decentralized at this time. There is no central repository like Sublime and Atom have. However, [for now we can use the Zed wiki for this purpose][2].

### Under the hood

Packages are essentially not much more than a way to easily install some files into your configuration project. When you look in your Configuration project under the `/packages` directory (the tree is the best way to explore here: `Command-T`/`Ctrl-T`), you'll see that there are already a number of packages pre-installed. At the time of this writing the following modes are distributed as Zed packages:

*   [JavaScript mode][3]
*   [JSON mode][4]
*   [JSON5 mode][5]
*   [PHP mode][6]
*   [CSS mode][7]
*   [JSX mode][8]

Over time, more and more built-in modes will be migrated to Zed packages, but this is a significant undertaking, so it will take a while.

If you open up the `/default.json` file in your Configuration project, you'll see a `packages` key listed:

    packages: [
        "gh:zedapp/javascript-mode",
        "gh:zedapp/json-mode",
        "gh:zedapp/json5-mode",
        "gh:zedapp/php-mode",
        "gh:zedapp/css-mode",
        "gh:zedapp/jsx-mode"
    ]


ZPM ensures that each of the packages listed there are installed and kept up-to-date automatically. If you installed a package yourself you'll find it listed in your `/user.json` file.

So where do these packages come from? A package URI can either be a full HTTP link to a directory that contains a `package.json` file, or, preferably, a shortcut can be used. Shortcut URIs are prefixed with (currently) either `gh:` (for github) or `bb:` (for bitbucket). These expand to (in case of the `gh:zedapp/javascript-mode`) to `https://raw.githubusercontent.com/zedapp/javascript-mode/master/`. ZPM expects, by appending `package.json`, to [find a JSON file][9] similar to this:

    {
        "name": "JavaScript mode",
        "uri": "gh:zedapp/javascript-mode",
        "version": "0.2",
        "description": "JavaScript mode for Zed",
        "files": [
            "beautify-js.js",
            "beautify.js",
            "check.js",
            "index.js",
            "jshint.js"
        ]
    }


The required keys are:

*   `uri`: This URI has to *exactly* match the URI people will use to install your package (if not, you can expect weird behavior).
*   `name`: The name of the packaged used to display in the UI
*   `description`: Description used to display in the UI
*   `version`: Version number, when you increase this number people with the package installed will automatically updated (ZPM checks for updates every few hours)
*   `files`: A list of relative paths of files that the package consists of (`package.json` and `config.json` are included automatically, you don't have to add them to this list).

Every package, in addition to `package.json` should at least have a `config.json` file that contains [regular Zed config, for instance defining new commands, modes, themes][10] or whatever your package offers. [Here's the config for the JavaScript mode][11]. The rest of the files are typically JavaScript files that implement the commands listed in the config file.

### Developing your own packages

#### Preparation

The first thing you'll want to do is store your configuration project in a local directory (rather than SyncFS, which is the default in the Chrome edition of Zed). The reason is you'll want to upload or check in your package files to e.g. Github so you need direct access to the files. To do this in the Chrome version run the `Configuration:Store in Local Folder` command. If you're using the standalone version, your configuration is stored in `~/.config/zed/config` on Linux and `~/Library/Application Support/zed/config` on Mac. If you want to store your config elsewhere use the `Configuration:Set Configuration Directory` command. Personally I store my configuration somewhere in my Dropbox folder.

#### Decide where to host your package

I suggest you create a public Github or Bitbucket repository for your package. In this blog post we'll use [hosting it on a Github repository called `sample-zed-package` hosted on my `zefhemel` github account][12] as an example.

#### Create the package

The Configuration project has some developer-specific commands to get you started quickly. Run the `Tools:Zpm:Create Package` package. This will prompt you for the package URI. We'll enter `gh:zefhemel/sample-zed-package` (replace with whatever your repo is).

This will create two files in `/packages/gh/zefhemel/sample-zed-package/` named `package.json` and `config.json`. It will open `package.json` by default. Update its default values to whatever you want, e.g.

    {
        "name": "My First Zed Package",
        "uri": "gh:zefhemel/sample-zed-package",
        "version": "1.0",
        "description": "A useful new package",
        "files": []
    }


Next, let's open up the `config.json` in the same directory (tip: Open up Goto with `Command-E`/`Ctrl-E` and press the spacebar to complete the path to the current directory, then pick `config.json`).

For our purposes we'll just define a sample command:

    {
        commands: {
            "My Test Command": {
                scriptUrl: "./command.js"
            }
        }
    }


Next, let's create `/packages/gh/zefhemel/sample-zed-package/command.js` (again using the same Goto trick):

    var ui = require("zed/ui");

    module.exports = function(info) {
        return ui.prompt("Hello world!");
    };


As you can see a Zed command is implemented as a CommonJS-style JavaScript module. It exports a function taking a single argument (`info`) that, depending on your configuration contains useful information about the context in which the command was executed. Zed comes with a growing API that allow you to interact with the editor, all these APIs are available by `require`'ing modules under `zed/*`. In your configuration project look under `/api/zed` to see what's available. Admittedly, documentation is lacking on these APIs, so until that improves it is recommended to look at a lot of examples. For this, the Configuration project is your oister: all code for all installed packaegs, modes, all themes and many commands is all there to be inspected. If you have specific questions, please join the [Zed Google Group and ask!][13]

To test it out our newly created project we need to add our package to our `packages` list in `/user.json`:

    packages: [
        "gh:zefhemel/sample-zed-package"
    ]


Automaticically, your configuration will reload and your new command should be available. Run `My Test Command` to try it out. If it's not there, try reloading your configuration explicitly using `Configuration:Reload`. You will have to run this command every time you change your `config.json` file. Another command you'll need a lot is the `Sandbox:Reset` command, which will make sure your JavaScript code is reloaded the next time it's invoked.

#### Publishing your package

Before publishing our package we have to remember one important thing: to update our `package.json` to include all our extra files (files other than `package.json` and `config.json`). Luckily Zed offers a convenience command for this: Switch to your `package.json` file and run `Tools:Zpm:Update Package.json File List`. This command will automatically scan your project and update your `package.json` to include the `command.js` file.

This is where the Zed-part ends. In brief what what's left to do is to turn our package directory into a git directory, commit all files to it and push it to github.

To do so, open a terminal and `cd` to your Zed configuration directory, then `cd` into our package directory:

    $ cd packages/gh/zefhemel/sample-zed-package


Initiallize a git repository there, add all files and commit:

    $ git init
    $ git add *
    $ git commit -m "Initial checkin"


Add the github repository we created earlier as a remote and push to it. In my case:

    $ git remote add origin git@github.com:zefhemel/sample-zed-package.git
    $ git push -u origin master


Done!

#### Testing your package

Before telling all our friends, all we have to do now is test our package. For this purpose I always have a separate Zed copy lying around (either I use the standalone version for development and the Chrome version for testing or the other way around, or I use a Zed chrome install in the Canary version of Chrome). Alternatively you can switch your Zed configuration to a new, clean, directory (and switch back later). The goal is to have a Zed install without your package already installed. You can also use another computer (e.g. your Chromebook) of course.

To install your package, in your "clean" Zed run the `Tools:Zpm:Install` command and enter your package's URI. If all works out well your command should now be available. Rather than running `Tools:Zpm:Install`, you can also update your `packages` list to include your package's URI in the Configuration by hand. The effect should be the same.

Works? Congratulations, be sure to add your package to [our wiki page!][2]

#### Development and debugging tips

You should treat the Configuration project like a development environment for developing Zed packages. I usually start out with adding my new modes and commands to my `/user.json` file, and if it works I migrate them to a package.

**Logging:** Every project has a `zed::log` file that lists notices, errors and warnings from Zed and its sandbox code. If your package or script doesn't work, always check `zed::log` first for pointers to what may be wrong. For debugging purposes you can use `console.log` etc. in your JavaScript, whose output also appears in `zed::log` (prefixed with `[Sandbox]`).

**Reloading/restarting:** Since Zed strictly separates all the package and extension code from the editor itself by running it in a sandbox, it is possible to edit your packages and test the result immediately without restarting Zed or reopening your editor window. What you have to remember is that in order to reload your configuration file (`config.json`) you can just run the `Configuration:Reload` command. And if you made changes to your JavaScript files, you just run the `Sandbox:Reset` command to have Zed reload those files to see your changes in action.

**Protip:** If you do a lot of Zed package development, it may be a good idea to bind the `Configuration:Reload` and `Sandbox:Reset` commands to a key combination. I have this in my `/user.json`:

    keys: {
        "Sandbox:Reset": "Ctrl-Shift-S",
        "Configuration:Reload": "Ctrl-Alt-Shift-S"
    }


**Common problems:**

*   If your configuration keeps reloading constantly, after you add your package to the `packages` key in your `/user.json` a likely cause is that the URI listed in your `package.json` does not match the URI used in the package's path. That is, if your package URI is `gh:abc/def` your `package.json` *has to be located in* `/packages/gh/abc/def/package.json`, if it's not, looping behavior can occur.
*   If you see 404 errors in `zed::log` when installing or running your package, this is likely a problem with your `files` list in your `package.json`. If the 404s occur while installing a package, make sure that you have checked in a `package.json` where all files listed under `files` exist. If it happens while testing a package *after* installation, make sure that the file that Zed claims it cannot find was listed under the `files` key in your `package.json`.

And that's it! Let's see what you can build!

 [1]: https://github.com/TheKiteEatingTree
 [2]: https://github.com/zedapp/zed/wiki/Packages
 [3]: https://github.com/zedapp/javascript-mode
 [4]: https://github.com/zedapp/json-mode
 [5]: https://github.com/zedapp/json5-mode
 [6]: https://github.com/zedapp/php-mode
 [7]: https://github.com/zedapp/css-mode
 [8]: https://github.com/zedapp/jsx-mode
 [9]: https://raw.githubusercontent.com/zedapp/javascript-mode/master/package.json
 [10]: http://zedapp.org/2014/02/configuration/
 [11]: https://github.com/zedapp/javascript-mode/blob/master/config.json
 [12]: https://github.com/zefhemel/sample-zed-package
 [13]: https://groups.google.com/forum/#!forum/zed-user
