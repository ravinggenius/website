---
title: Finding, Installing And Maintaining Software
created_at: 2012-07-23 22:23:00 UTC
---

I have been extremely underwhelmed by the software install process. Mostly it seems to be a game of seek and find, but one I never wanted to play. There are no less then three "sources" I have to check to find software: App Store, Internet, Homebrew.

## App Store

Some blessed software (mostly commercial) is available in the App Store. The FOSS options in the App Store are virtually non-existent. If I cannot find what I am looking for in the App Store, I get to search the Internet. Usually I can find what I need here, but it takes so long. Sometimes (GitX) I find multiple packages, all claiming to be what I want. Hopefully what I find is a .dmg and not some .pkg or source tarball.

## Internet

Installing a .dmg (or even a .pkg) is fairly painless up front. However I have two complaints. First Apple seems to encourage app developers to show off their creativity while designing the drag-this-icon-over-to-this-other-icon step. The result is that no two .dmgs have been the same.

My second problem is with the Internet source for software is much more substantial. Every app developer has to rewrite a custom auto-update story. This sucks for app developers and users. Each developer gets to do things differently, as there is not guiding process to follow. Some don't even bother. For users it sucks because app developers may not implement any kind of automatic updates, and of the ones that do, there is no guarantee that the process will be the same. This is confusing to users and leads to more time learning pointless details.

## Homebrew

Installing software with Homebrew has its own set of challenges. It is a simple package manager, so coming from Linux, it is closest to what I am used to. Homebrew also manages dependencies and installs from source; that is good. I also appreciate that Homebrew can update everything it installed with a single command. However after perusing [Homebrew's packages](http://braumeister.org/), I feel safe to say that the selection leaves much to be desired. Another mark against Homebrew is that it seems to not be officially supported.
