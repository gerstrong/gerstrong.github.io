---
layout: post
title: "Commander Genius built with Clang"
date: 2014-09-07
---

<b>Note</b>: This is an old article I had one my old wordpress server.

Since I got some time on my hands I decided to take a look at the hype of LLVM and thought well how does it works with Commander Genius...

Now I don't want to go into details of LLVM or Clang. Tons of information about that technology can be found <a title="here" href="https://en.wikipedia.org/wiki/Clang">here</a> and anywhere else. I just want to see how well can you build Commander Genius using Clang and what do you get. Of course this was done using Linux (Mageia 4.1 64-Bit)

<h4>CMake</h4>

This one is sweet! If you don't have any obscure defines in your cmake file you can tell cmake to use it by typing:

<code>
export CC=/usr/bin/clang 
export CX=/usr/bin/clang++
cmake .
</code>

and there you go, just launch make and the build system takes it. Remember to clean up caches if you had some.

<h4>QtCreator 3.2.1</h4>

This is not that simple, but simple enough. I would launch those two exports in a terminal and then open QtCreator so its underlying build-system takes it correctly.

First of all you should enable some plugins, because by default they are deactivated. Go to Help->Plugins and enable ClangCodeModel.

<a href="../../../../assets/2014/09/QtCreatorLaunch.png"><img src="../../../../assets/2014/09/QtCreatorLaunch-300x168.png" alt="QtCreatorLaunch" width="300" height="168" class="alignnone size-medium wp-image-128" /></a>

Now you should configure the Kit so QtCreator knows what do use in order to build your app.

<a href="../../../../assets/2014/09/KitClang.png"><img src="../../../../assets/2014/09/KitClang-300x168.png" alt="KitClang" width="300" height="168" class="alignnone size-medium wp-image-127" /></a>

Define a new Kit and viola, it will build. Nothing special so far except that you can do more.

This is were Clang really shines in my opinion. First of it I feel it builds a bit faster links much faster than GCC.

Second, the warning and errors are so much better explained.

<a href="../../../../assets/2014/09/niceWarnings.png"><img src="../../../../assets/2014/09/niceWarnings-300x168.png" alt="niceWarnings" width="300" height="168" class="alignnone size-medium wp-image-129" /></a>

And last but not least the Clang Analyzer runs in the background and is able to give you some hints and warnings or even errors as you type. This is great because you don't need to compile the code first in order to see what you did wrong.

<a href="../../../../assets/2014/09/Analyzer.png"><img src="../../../../assets/2014/09/Analyzer-300x182.png" alt="Analyzer" width="300" height="182" class="alignnone size-medium wp-image-126" /></a>

The internal code analyzer used for GCC usually is also nice, but I would say this one provides more to look at.

The advantage of that really is, that the analyzer actually uses Clang itself instead of guessing what GCC would say.

<h4>Binary sizes</h4>

I also did some binary size comparisons and look at that!

With GCC 4.8 (64-Bit) I get:
<code>
[gerstrong@localhost LINUX (dbfusion)]$ ls -l
-rwxrwxr-x 1 gerstrong gerstrong 3573043 Sep 22 17:50 CGeniusExe*
</code>

And with Clang 3.3 (64-Bit):
<code>
[gerstrong@localhost LINUX (dbfusion)]$ ls -l
-rwxr-xr-x 1 gerstrong gerstrong 3312886 Sep 22 18:00 CGeniusExe*
</code>

Well, at least the binary got a bit smaller, not by much though, but everything smaller is always nice :-)

When I started CG all started pretty well. No problems, no crashes, stable as with GCC builds and also as fast, so there you go.

I don't know what to use in future, there is GCC 4.9. I read it has become better, so I would say we have a small compiler wars over here between those two at least. Good thing, as usual, is, you can decide what you want to use.

What I really like is how well it integrates into QtCreator so far and how fast it links. This is something that really impressed me.

Nevertheless it has its issues and some warnings just don't go away even when they are fixed, but still it is some good help and let's deploy your applications in less time. I'm pretty sure this will improve in later versions.

So would I recommend it? Of course I would, but I also think GCC does a fairly good job and I can't wait to see what the next versions will do.
