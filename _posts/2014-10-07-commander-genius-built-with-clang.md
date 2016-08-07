---
layout: post
title: "Commander Genius built with Clang"
date: 2014-10-07
---

<b>Note</b>: This is an old article I had one my old wordpress server.

There is a document around the internet (<a href="ftp://ftp.heanet.ie/disk1/sourceforge/c/cl/clonekeenplus/CGenius/CompileCGunderWindows.pdf" title="link">here for example</a>) I wrote some years ago in how to setup the source code of Commander Genius under Windows 7 the way you can compile it yourself and do changes wherever necessary.

Getting everything run on Windows is a bit more complex than with a linux distro providing some sort of software management, because the user has to download some dependencies by hand starting with a working compiler and all the required libs that suit him. As there are many options to download, I'm going to provide one that works well.

I hope with this article everything will be easier for those who want to build CG or create at no cost great and powerful programs.

Other opensource projects have the same requirements and often depend on more stuff than CG, but after going step by step with this tutorial you will have a nice opensource environment in which you can build a lot of cool programs and libs of course. 

C++11 pushs the standard over the edges and boost helps you to deploy programs with even higher quality. If you are like me, you are going to have a lot of fun with QtCreator and its ecosystem.

Of course this article might have some issues. If you encounter something or you don't get the environment run, just leave a comment or let me know by dropping an email in my box. :-)

So let's start shall we?

<h2>Prerequisites</h2>
The requirements are:
<ol>
	<li>Compatible compiler for source code (c++11)</li>
	<li>CMake</li>
	<li>SDL and SDL_image 2</li>
	<li>Ogg and Vorbis</li>
	<li>Boost</li>
</ol>

What we also want, so we can develop and might improve the code or build our own projects:

<ol>
	<li>Good IDE</li>
	<li>Good Debugger</li>
	<li>Git, hell yeah!</li>
</ol>

We are not focusing on Visual Studio because I never build it on that platform. That has several reasons, but if someone wants to try that, well, he can do that I guess. All the stuff like libs have to run with that platform which can be tedious sometimes. Languagewise it shouldn't be a problem because since M$ Visual Studio 2012 is out, there is some C++11 support pretty sure enough so you can build it.

Ahh and of course your Windows XP, Vista, 7 or higher has to be 64 Bit, since those builds will only run on that.

For a 32-Bit system you can use the 32-bit compilers instead (QtCreator ships one), but all the libs need to be compatible with that platform.

<h2>Compatible compiler (GNU C++)</h2>

There are many packages you can download but I would recommend this package <a href="http://sourceforge.net/projects/mingwbuilds/files/host-windows/releases/4.8.0/64-bit/threads-posix/seh/x64-4.8.0-release-posix-seh-rev2.7z/download" title="Mingw x64-4.8.0-release-posix-seh-rev2"></a>. It also has a debugger which does not solve all the STL goodness yet but with a strong IDE it provides some basic debugging nevertheless.

Btw. if you need a good unpacker that handles many compressed package formats try <a href="http://peazip.sourceforge.net/" title="Peazip">Peazip</a>

In the "Good Debbuger" Section of the second upcoming article I will explain how you can refine the debugger.

Just unpack the package at a place where you can access it easily. It should be a directory for developer stuff, because more files from the libraries, like boost and SDL will be put there later on. I would recommend "C:\mingw64" which we will use in the screenshots for our configurations in the IDE.

<h2>CMake</h2>
That one is easy. Get it <a href="http://www.cmake.org/download/" title="here">here</a>!

You can download the Win32 Installer and start the setup, that's all. You should remember the path where it is installed. I would think it is the best extracting the zip into C:\ming64, the way the "share", "bin" subdirectories are merged, but it's not necessary.

CMake allows to cross compile programs. It is used by CG and its strength is that you can deploy project or makefiles for different systems. The IDE of my recommendation QtCreator opens those CMakeLists.txt files and acts as frontend of cmake. So you don't have to worry about the sources that much when others want to have a project file for a different IDE.

Cmake is able to generate project files for Eclipse, CodeBlocks and M$ Visual Studio. QtCreator just bases the build-system on CMakeLists.txt.

<h2>Good IDE (QtCreator)</h2>

Also it should be clear that I use opensource software for building this interpreter and it always has been that way.

I have tried a good number of IDEs to get CG work, because first I used Eclipse CDT for a long time, which was nice but always too clonky and overbloat in my opinion. 

Later I changed to CodeLite, CodeBlocks, Anjuta, Kdevelop and also geany, but I never was happy with those. One day I tried QtCreator and instantley got hooked.

I'm going to recommend that one, but of course, any IDE in which you can define the compiler will do.

Let's go the website and download <a href="http://download.qt-project.org/official_releases/qt/5.3/5.3.2/qt-opensource-windows-x86-mingw482_opengl-5.3.2.exe" title="Qt 5.3.2 for Windows 32-bit (MinGW 4.8.2, OpenGL, 737 MB) ">here</a>

If there is a newer version, take it. As you can see, it already ships a compiler you can use right away, but it's only 32-bit. Yeah, 64-bit can runs 32-bit apps but we want to got further, let's do that...

So we have to tell QtCreator to please use the 64-bit compiler and linker.

Open up QtCreator and go to Tools->Options->Build & Run and go to the Debuggers Tab. You can clone the autodetected and edit the path of the clone so gdb for the 64-Bit compiler is set.

<a href="../../../../assets/2014/09/Bildschirmfoto14.png"><img src="../../../../assets/2014/09/Bildschirmfoto14-300x194.png" alt="gxxWin7inQTC" width="300" height="194" class="alignnone size-medium wp-image-141" /></a>

No go to the compilers tab, clone a profile here as well and set the path where you find your compiler.

<a href="../../../../assets/2014/09/Bildschirmfoto15.png"><img src="../../../../assets/2014/09/Bildschirmfoto15-300x194.png" alt="gdbWin7inQTC" width="300" height="194" class="alignnone size-medium wp-image-142" /></a>

And finally create a kit (You can clone here as well), use the desktop profile setting and choose in the dropdown menus the compiler and debugger profiles you just created in the last steps.

<a href="../../../../assets/2014/09/Bildschirmfoto16.png"><img src="../../../../assets/2014/09/Bildschirmfoto16-300x194.png" alt="kitWin7inQTC" width="300" height="194" class="alignnone size-medium wp-image-143" /></a>

Now, that you have all set up you can open CMakeLists.txt as a project file, or create your own ones with a nice wizard. Using a new cmake c++ project under File->New will create an extremely portable hello world, with CMakeLists.txt included.

If cmake was not detected, go to Tools->Options->Build & Run then go to the CMake tab and set the correct path of cmake.exe.

As you can see, staying with Windows and having a powerful build system at the same time with a fun IDE and a good compiler is possible without having to pay any money. Thanks to Richard Stallmann and all his community this and more was made possible.

Btw. did you know, that with all that you can also build Fortran programs or even mixed C/C++ Fortran programs? GNU Fortran is shipped and Cmake also supports that. Just create a new cmake c++ project, open the CMakeLists.txt, add the line "enable_language (Fortran)" before "add_exectuable(...)" and put your for-files as parameter to that "add_exectuable" command where the C++ File is already defined. Put your code in the for file and there you go! Fortran at no extra cost!!!



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
