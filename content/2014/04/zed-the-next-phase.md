Zed: The Next Phase
===================
date: 2014-04-01

When I started the Zed project about a year ago I intended to build an editor just for me: something minimal, simple and stable. Writing something for myself seemed a natural thing to do after spending about a year and a half having a job [building an IDE][1]: once you've built your own tools, there's no going back. Also, having built this sort of thing before (although not from "scratch"), it was fairly quick to get something working.

Over the past year, Zed has been the ultimate piece of dogfood-ware for me -- my own personal playground that allowed me to iterate on lingering ideas I had on improving code editing. Since people asked why I created *yet another* editor, over time I distilled some [principles behind the design of Zed][2].

<img src="/img/zed-screen-new.png" alt="Screenshot" width="1040" height="737" class="aligncenter" />

The past half a year I've been using Zed full-time and I've been *very* happy with it. And I'm not the only one. The Google Chrome Web Store (Zed currently runs as a Chrome app) [tells me][3] there are well over 4000 "weekly users", and the reviews are generally very positive. Now I take the 4k number with a grain of salt, but clearly, this is no longer a 1-person audience editor. The number of community contributions has also increased lately and there appears to be a growing number of users that don't just like Zed as a cool "look what web tech can do" demo, but really *love* Zed as an editor, and see it as a modern-day Emacs or Vim: minimalist, powerful and extensible.

However, with a full-time day job at work, and full-time night job as a parent, there isn't always much time to spend on Zed. At least not as much as I'd like. And I have *so many* cool ideas I still want to implement.

It's time to fix that.

### I'm making Zed my day job

So, I'm going to try something radical. As of today, I'm making Zed my day-time job.

I've launched a company to further develop Zed, with the goal to, over time, earn enough money on it to support me and my family, and to continue developing Zed into something great.

While an obvious option to make Zed profitable would be to make it proprietary and sell licenses, I won't be doing that. I think there's a lot of value for users in the fact that their editor is open source, in terms of hackability and longevity. Also, since I'm a company of one -- for the foreseeable future -- I think the best way to compete is if when the community helps out with enhancement and bug fixes, as it does already. So, *Zed will remain open source.*

### Sustainable Open Source

I'm going to try making a living working on open source. I have not fully decided how I'll attempt this, so [all ideas are welcome][4]. However, my current plan is the simplest and most transparent thing possible: ask users to pay. If you use Zed and get value out of it, support me financially to support further development. Just as you would for regular commercial software, pay for Zed as well.

While possibly naive, this seems like the cleanest way to sustainability of this type of project. I don't want to do [open core][5], or do weird in-editor ads (which people would be able to easily remove anyway). Consulting around Zed also doesn't seem to make much sense. Again, tips or suggestions, are welcome, so [get in touch][4].

### Why would you pay for an *editor*?

So why would you pay for an editor when you can get Vim, Emacs, Notepad++ and Gedit for free?

As I see it, the cost of software has very little to do with purchase price. If a piece of software *just* makes you 1% more productive compared to *not* using the software, and you earn, say, $40/hour and use it 40 hours a week (developers tend to use their editors close to full-time), very quickly this software is worth $70/month. Or rather, *not* using that piece of software costs you $70/month. Zed will be *significantly* cheaper than that, price wise.

Are you as productive using your "free" software as you are/will be with Zed? My challenge is to make the answer to that question a resounding "no."

As a bonus, in contrast to proprietary editors like Sublime and most Jetbrains IDEs, Zed is 100% open source, so you can read the source code, enhance it, fix it, break it and learn from it. Even if I or my company will go away, Zed won't, if somebody cares enough about it to develop it further. So it's a more lasting investment than paying for a commercial alternative.

Of course, this being open source, there's no way to enforce anybody to pay a dime. So what if people don't? That will mean that when my savings run out I will have to go back to a regular day time job. As a result, Zed development will slow down again. This tool that your rely on won't improve at the same pace anymore. Me unhappy, you unhappy. If instead lots of people contribute, possibly I can hire a second person, third, fourth. Who knows. Result: Zed will get even awesomer.

It's all in your hands.

Can't some random person fork the project and attempt same thing? Yep. Worse, they can fork the project, and create a proprietary version and start selling it. I'm just assuming people are decent and respect my and the community's work. That's what this whole open source thing is all about, or so I understand.

### So, what cool features will we get?

I have *loads* of things I want to do, but the only one I want to commit to right now is a stand-alone version of Zed. Zed currently is only available as a [Chrome packaged app][6]. So you need to use Chrome to run it. This is fine, but not everybody likes it. It also limits OS integration somewhat.

The stand-alone version will be built on top of [node-webkit][7] and be available for Mac, Windows and Linux. Once the initial work there is done, both version should continue working from the same code base, so I should be able to support two versions (Chrome App and standalone) without much effort.

There are many more things I will finally have time for, but I'll talk about those over time. Those [familiar with my background][8] can probably guess what direction I could take.

### Sign me up!

I'm still working out ways for users to support this project, but one that's available for those who want to support the project right away is [my Gittip account][9]. I'm going on a stretch here and am willing to accept Gittips from people who do not currently use Zed, but are excited about the dream and want to find out where this is going. I know, I'm a very generous that way. Also, if you or your company are interested in supporting this effort and don't want to use Gittip, [get in touch][4]. And if you haven't already, give Zed a try and [report any bugs you may find][10].

I'm *very* excited, and frankly, a bit scared to take this step. But I've also been looking forward to it for a long time.

Let's make Zed even more awesome!

Watch this blog, my [twitter account][11], or [Zed's twitter account][12] and subscribe to the [Google Group][13] for regular updates!

Discussion on [Hacker News][14] and [Reddit][15].

 [1]: http://c9.io
 [2]: /vision
 [3]: https://chrome.google.com/webstore/detail/zed-code-editor/pfmjnmeipppmcebplngmhfkleiinphhp/reviews
 [4]: mailto:zef@zef.me
 [5]: http://en.wikipedia.org/wiki/Open_core
 [6]: https://chrome.google.com/webstore/detail/zed-code-editor/pfmjnmeipppmcebplngmhfkleiinphhp
 [7]: https://github.com/rogerwang/node-webkit
 [8]: http://zef.me/about
 [9]: https://www.gittip.com/zefhemel/
 [10]: https://github.com/zedapp/zed/issues?milestone=1&state=open
 [11]: http://twitter.com/zef
 [12]: http://twitter.com/ZedEditor
 [13]: https://groups.google.com/forum/#!forum/zed-user
 [14]: https://news.ycombinator.com/item?id=7515147
 [15]: http://www.reddit.com/r/programming/comments/220czd/zed_new_open_source_code_editor_the_creator_quits/
