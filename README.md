LiveReload: xrefresh for Safari & Chrome
========================================

LiveReload is a Safari/Chrome extension + a command-line tool that:

1. Applies CSS and JavaScript file changes without reloading a page.
2. Automatically reloads a page when any other file changes (html, image, server-side script, etc).

Watch an [awesome screencast by Gregg Pollack](http://blog.envylabs.com/2010/07/livereload-screencast/) at envylabs.com.

**Warning: Windows is not supported yet.** We now have Windows installation instructions, but the directory watching does not work. Will be fixed later this week with transition to another monitoring API.

**What do our users say?**

“I think LiveReload is going to change the way I work...” [@mheerema](http://twitter.com/mheerema/status/18363670011)

“spent a day using livereload. really impressed, very nice to watch pages update as I add / change code.” [@pollingj](http://twitter.com/pollingj/status/18366550224)

“Gem of the month (quarter?): LiveReload” [@grimen](http://twitter.com/grimen/status/18369684099)


What's new?
-----------

Want to know about latest developments and smart tricks? Follow [@livereload](http://twitter.com/livereload) on Twitter!

1.2.2: add .erb to the list of monitored extensions (this is a gem-only update, run `gem update livereload` to install).

1.2.1: added workaround for Chrome bug (unable to open WebSocket to localhost), fixed problem with command-line tool trying to use kqueue on Linux.

1.2: added Chrome extension, added icon artwork, added a check that the command-line tool version is compatible with the extension version, fixed a bug with multiple stylesheet updates happening too fast.

1.1: enabled autoupdating for the Safari extension.

1.0: original release -- Safari extension and a command-line tool in a Ruby gem.


Installing in Safari
--------------------

1. You need Ruby installed. Mac OS X users already have it, Windows users get it from [ruby-lang.org](http://www.ruby-lang.org/en/downloads/).

2. Install the command-line tool. On OS X and Linux:

        sudo gem update --system
        sudo gem install livereload

    on Windows:

        gem update --system
        gem install eventmachine --platform=win32
        gem install livereload

    (warning: Windows is not supported yet, see the warning in the beginning)

3. If you haven't already, [you need to enable Safari extensions](http://safariextensions.tumblr.com/post/680219521/post-how-to-enable-extensions-06-09-10).

4. Download [LiveReload 1.2 extension](http://github.com/downloads/mockko/livereload/LiveReload-1.2.safariextz). Double-click it and confirm installation:

![](http://github.com/mockko/livereload/raw/master/docs/images/safari-install-prompt.png)


Installing in Chrome
--------------------

1. You need Ruby installed. Mac OS X users already have it, Windows users get it from [ruby-lang.org](http://www.ruby-lang.org/en/downloads/).

2. Install the command-line tool. On OS X and Linux:

        sudo gem update --system
        sudo gem install livereload

    on Windows:

        gem update --system
        gem install eventmachine --platform=win32
        gem install livereload

    (warning: Windows is not supported yet, see the warning in the beginning)

3. Visit the [LiveReload page](https://chrome.google.com/extensions/detail/jnihajbhpnppcggbcgedagnkighmdlei) on Chrome Extension Gallery and click Install. Confirm the installation:

![](http://github.com/mockko/livereload/raw/master/docs/images/chrome-install-prompt.png)

Done. Now you have an additional button on your toolbar:

![](http://github.com/mockko/livereload/raw/master/docs/images/chrome-button.png)


Usage
-----

Run the server in the directory you want to watch:

    % livereload
    
You should see something like this:

![](http://github.com/mockko/livereload/raw/master/docs/images/livereload-server-running.png)

Now, if you are using Safari, right-click the page you want to be livereload'ed and choose “Enable LiveReload”:

![](http://github.com/mockko/livereload/raw/master/docs/images/safari-context-menu.png)

If you are using Chrome, just click the toolbar button (it will turn green to indicate that LiveReload is active).

Looking to also process CoffeeScript, SASS, LessCSS or HAML? Here's a [Rakefile that does that live too](http://gist.github.com/472349).


Known Issues (please read!)
---------------------------

The command-line tool uses a lame per-file watching API from EventMachine and runs out of open file limit on large projects. In Chrome, this looks like a broken connection immediately after you connect. In Safari, this looks like a crash (since Safari crashes if websocket is disconnected during handshake).

Until this is fixed, you may want to increase your `ulimit -n`:

    ulimit -n 4096
    livereload

Does not work on Windows (yet!)


Limitations
-----------

Note that you can only have one page monitored, so if you enable LiveReload on another page, the first one will stop reloading.

LiveReload does not work with local files in Chrome (since accessing file:// URLs from an extension requires an approval from the Google Chrome team) and in Safari (since we haven't bothered fixing it yet).


License
-------

This software is distributed under the MIT license.


Thanks
------

LiveReload has been greatly inspired by (and actually borrows a few lines of code from) [XRefresh](http://xrefresh.binaryage.com/), a similar tool for Firefox.
