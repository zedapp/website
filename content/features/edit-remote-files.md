Edit Remote Files
=================

Zed makes editing files on any server or even local VM super easy. No port forwarding or firewall tweaking is required: as long as the server can reach the Internet, you can edit files.

Here's how to do it:

1.  Log into the server in question (e.g. via SSH)
2.  In a terminal download `zedrem`, the Zed remote editing utility (you only need to do this once):

        curl http://get.zedapp.org | bash


    This will automatically detect the operating system of your server (currently 32/64 bit and ARM Linux, FreeBSD and Mac OS X are supported) and download `zedrem` into the current directory. If you use windows, you can download [zedrem.exe from here][1].

3.  At this point you have two options, the "simple" option and the "quick" option:

    *   Simple option: run `zedrem` without any flags as follows:

            ./zedrem <dir-to-edit>


        or, leave out the `<dir-to-edit>` entirely and just run `./zedrem` to edit files in the current directory.

        You will now be given a URL to copy and paste into the Zed chrome application in the Project Picker under "Edit Remote Files". Paste the URL and press `Return`, you will now get a Zed editor window with all your files available.

    *   Quick option: get your unique zedrem key from the Zed app by (in any editor window) running the `Zedrem:Get User Key` command. Then run zedrem as follows:

            ./zedrem -key YOURUSERKEY <dir-to-edit>


        A Zed editor window should now appear immediately.

**Protip #1:** If you often run `zedrem` in the background (by adding `&` to the end). Consider enabling `huponexit` in your bash shell (e.g. in your `~/.bashrc` or `~/.bash_profile`) so that the `zedrem` process will be stopped when you exit your shell (e.g. when you disconnect your SSH connection). Put this in your bash startup file (or just enter it in your shell every time):

    shopt -s huponexit


Then, you can run `zedrem` in the background while feeling safe that all `zedrem` processes will automatically be killed when you exit:

    ./zedrem <dir-to-edit> &


**Protip #1:** Upon startup zedrem reads the `~/.zedremrc` file if exists, this file in an "ini" file with the following sections and options:

    [client]
    url = wss://remote.zedapp.org:443
    userKey = youruserkey

    # For running zedrem in server mode
    [server]
    ip = 0.0.0.0
    port = 7337
    sslCert = /path/to/file.crt
    sslKey = /path/to/file.key


This is particularly useful if you run your own zedrem server (see below) or if you edit files often on the same server (so you don't have to fill in your user key every time).

## How it works

The `zedrem` utility (written in Go, source code available from our [Github repository][2]) establishes a secure websocket connection to `wss://remote.zedapp.org:443` and registers itself. The `remote.zedapp.org` server will function as a proxy between the Zed Chrome application and your server. The Chrome app will request a file list, a file load, a file save, and these will be proxied through `remote.zedapp.org` to your server. This way you can edit files on server behind firewalls and part of VPNs -- as long as they can contact a Zed server, you can edit files there.

If you feel uncomfortable with a proxy managed by us, you can run your own. In fact the `zedrem` you downloaded can function as such a proxy server. To do so, simply run it in server mode:

    ./zedrem --server


This will run a proxy server listening on port 7337 by default (check `./zedrem --help` for command line options). Then to connect to it, pass the `-u` flag to override the `server.zedapp.org` default:

    ./zedrem -u ws://your-ip-or-hostname:7337


For this to work, the machine running `zedrem --server` must allow incoming connections on the port it's listening to.

Happy remote editing!

 [1]: http://get.zedapp.org/zedrem.exe
 [2]: https://github.com/zedapp/zedrem
