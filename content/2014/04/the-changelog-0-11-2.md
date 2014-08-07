The Changelog: 0.11.2
=====================
date: 2014-04-29

Before we get to the changes in this release, a little update on the funding situation. We're currently at $115/week, which is still way off from making this project sustainable. So, if you're a Zed user, [consider buying][1]!

Both the Chrome and Standalone version should be upgraded automatically to 0.11.2. If you somehow can't wait for the standalone version to self-update, feel free to download it again from the [download page][2].

![][3]

This release brings one major feature for Chrome Zed users: [Edit in Zed][4]. Edit in Zed is a new Chrome Extension that works in cooperation with the Zed Chrome App, so be sure you have both installed when testing it. What it does is add a little icon on any `textarea` on any website that shows up when you hover your mouse over it. When you click the icon, Zed will open allowing you to edit the content of the text area, constantly writing back the content. By default Zed launches in text mode, but you can, of course, easily switch to Markdown mode, use preview etc. This feature is fantastic when writing a lot of content on a web page (in a CMS, for instance). Try it out! [Here's a little screencast that demoes the feature][5].

Here's the full [changelog][6] for 0.11.2:

*   New "Edit in Zed" Chrome Extension for Zed Chrome version: adds a little on-hover Zed icon to textareas on any website in Chrome, when you click it, you can edit the contents of this text area using Zed. [Download the extension from the Chrome Store][4].
*   Usage data collection: upon first launch you will be asked to agree to collect anonymous usage data. This helps us to see what features (e.g. language modes) people are using and what to improve.
*   ZPM fix github package support (by conradz)
*   Fix: code beautification (formatting) for selection works now
*   Scroll past end of editor preference (by TheKiteEatingTree)
*   Modes:
    *   JSX (react.js) mode now has JSHint support
    *   Ruby mode now also works on Vagrantfile
*   Various minor bug fixes (by robru and others)

Thanks to all who contributed!

<script data-gittip-username="zefhemel" data-gittip-widget="button" src="//gttp.co/v1.js"></script>

 [1]: /buy
 [2]: /download
 [3]: http://lh5.googleusercontent.com/GTD14j7CnJ8Oc7EUErrNWEtPpgqDI45egaWD-dDxv_TEr-ANH5QoqK-eC1GQ32PkyVH0Rm09LQ=s640-h400-e365-rw
 [4]: https://chrome.google.com/webstore/detail/edit-in-zed/dpkaficlkfnjemlheobmkabnnoafeepg
 [5]: http://screencast.com/t/tjJXX1rYO
 [6]: https://github.com/zedapp/zed/blob/master/app/manual/changelog.md
