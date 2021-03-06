# QuoraDownloader
GUI tool to download Quora Answers
Quora Downloader Prototype

by dda https://github.com/dda

Made with Real Studio 2011 R4, an old version of Xojo http://www.xojo.com/

I have been using Real Basic (the language) and Real Studio (the IDE) since it was called CrossBasic (and I still had hair back then).

The cross-platform aspect is interesting (although I have no use for Windows, and little use for Linux).
But its main attraction, to me at least, is the IDE itself (probably the best I have used so far) and the ease of use when it comes to produce GUI apps.
This BASIC dialect is very easy to learn, quite a step up from the old BASIC days, and can be extended with C++ plugins, and dylibs.

This version is Mac OS X only (although I suppose it would be easy to fix it for Linux) as I am using curl in the shell to download.
There are two reasons for this.
  1/ When I used built-in HTTPSockets to download, the pages that were downloaded came back empty. With curl it works fine.
  2/ Using the shell in a synchronous manner slows things down, which in this case is better -- you need to throttle downloads.
     Of course I could throttle with asynchronous downloads too, but the shell made it easy.

There are two passes.

Pass 1:

• Get the first page -- pagination trick ?page_id=x (Thanks Nick!) and identify the total number of pages.

• Then extract the question/answer links for pass 2. They are spread over 5 workers.

Pass2:

• Create a folder fwor the answers, and a subfolder for the images

• Once we have all the links, start the workers. They go through the list of links they've been given.

• When a link is received, the page is saved. The date the question was answered/the answer updated is extracted.

• The image links are extracted and the images saved in the subfolder. JPEG and PNG images are recognized and properly named.
