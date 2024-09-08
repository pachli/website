---
layout: post
title: "One year on"
date: "2024-09-08 09:00:00 +0200"
categories: pachli
---
It's been a year since [launching Pachli on Mastodon](https://mastodon.social/@pachli/111030607167438186), so it's a good opportunity to do a quick review of what's been achieved so far, and what's still to do.

<!--more-->

## Nivenly Foundation

[Joining the Nivenly Foundation](/pachli/2024/07/02/more-on-nivenly.html) has helped set the project on a long term route to stability. There's still much to do around project policies and expanding project governance, but I'm very pleased the first milestone was achieved within the first year.

## Monthly releases

A new Pachli release happens at least once every calendar month, normally towards the end of the month. This is important for a few reasons, including:

### Incentivising contributors

If a project only releases a few times a year on an unpredictable schedule then contributors have no idea when their work will be available to the users.

If you contribute to Pachli you know your contribution to the app -- whether it's a translation, a bug fix, or a new feature -- will be in the hands of users by the end of the month.

### De-risking the release process

Infrequent releases in a software project introduce risk.

The less frequently you do something the less well-practiced it is and the greater the chance a mistake happens. It encourages only having one or two people who know how the release process works and are a critical dependency.

The Pachli release process is mostly automated, save for:

- Editing the release notes
- Writing the release blog post
- Some interactions with GitHub Actions
- Some interactions with Google Play

Those last two issues are due to API limitations in those services which still require the release engineer to click some buttons to advance the process.

### Minimising security risks in dependencies

In any large software project with dependencies one or more of those dependencies will release urgent security updates. It's a matter of if, and not when.

When this happens it's important downstream projects, like Pachli, can rapidly release a version with a fixed dependency. A Pachli release can complete within about an hour of the fix becoming available. Availability to users is then dependent on the speed with which Google Play and F-Droid can distribute the new version to users.

## Continued support for Android 6 and Android 7

Many of the Fediverse's userbase are marginalised and do not necessarily have the means to regularly upgrade their devices. Pachli continues to support devices running Android 6 while other apps move on, stranding those users on older versions unless they move to a new device.

Earlier this year planned obsolescence by Let's Encrypt meant many Android 7 devices could no longer connect to Mastodon servers using those certificates. This was [rapidly resolved](/pachli/2024/04/29/2.5.0-release.html#android-7-devices-and-lets-encrypt).

## Accessibility improvements

There have been a number of improvements to make Pachli more accessible. This includes:

- [Accessible fonts](/pachli/2023/09/29/accesible-fonts.html)
- [Showing scrollbars](/pachli/2023/10/05/1.2-release.html#show-scrollbars-in-scrollable-lists)
- [Talkback improvements](/2024/04/29/2.5.0-release.html#talkback-actions-for-notifications-and-direct-messages)
- Readability improvements for [media labels](/pachli/2024/06/27/2.6.0-release.html#improve-the-readability-of-media-labels) and [the navigation menu](/pachli/2024/06/27/2.6.0-release.html#improve-the-readability-of-the-navigation-menu-header), to name two

Many of these improvements are driven by direct requests from Pachli users. These are some of the most rewarding improvements to make, as you know they're having a direct benefit.

## New features

There have also been many new features. Some of my favourites are:

- [Removing "Load more", and always restoring the user's reading position](/pachli/2023/10/05/1.2-release.html#restore-the-users-reading-position)
- [In-app translation of posts](/pachli/2023/11/23/2.0-release.html#translation-support)
- [Better media display](/pachli/2024/02/28/2.3.0-release.html#previewing-and-playing-media)
- [Easier access to lists and list management](/pachli/2024/03/28/2.4.0-release.html#better-list-management)
- [View poll results without voting](/pachli/2024/03/28/2.4.0-release.html#view-poll-results)
- [Better timeline management](/pachli/2024/04/29/2.5.0-release.html#timeline-management)
- [Show suggested accounts](/pachli/2024/06/27/2.6.0-release.html#show-suggested-accounts)
- [Search operators](/pachli/2024/07/29/2.7.0-release.html#search-operators)
- [Warn if you post in the wrong language](/pachli/2024/07/29/2.7.0-release.html#warn-if-you-post-in-the-wrong-language)
- [Early support for non-Mastodon servers](/pachli/2024/01/29/2.2.0-release.html#detect-different-servers-adjust-visible-functionality)

## Code changes under the hood

Behind the scenes the Pachli code has undergone some sweeping changes.

The inherited code base was a mix of Java and Kotlin. It is now entirely Kotlin.

The code is also slowly being converted to modules. Partly to promote good design and untangle some of the existing dependencies, and partly to unlock significant increases in speed when building Pachli while developing. As the code is converted to modules it generally reduces the amount of code that needs to be recompiled while during the edit-compile-launch-debug cycle. I regularly see sub-two-second launch times during development, significantly faster than before this work started.

## Still to do

All of the above is great progress, and I am very pleased with how things are going.

As noted last month, [Pachli 2.9.0 will start introducing additional anti-harassment controls](/pachli/2024/08/02/harassment-controls.html). That, and expanded support for translation (in more places in the app, and privacy-preserving on-device translation) are the last large projects I want to complete in the 2.x series of releases. The 3.x series will start with additional support for fetching content from multiple servers; for example, to give a better view of a thread.

I also need to increase the number of code contributors who are not me. There is an active collection of people who regularly contribute translations (see below) and a small number of people have contributed one-off fixes for specific bugs. But I am still doing the vast majority of the development work.

That is a risk to the project. While I am not at risk from some of the issues that seem to plague open source developers around the Fediverse -- in particular, I've seen what burnout looks like when it affected former colleagues and I am careful to maintain healthy boundaries to ensure that does not happen -- something as prosaic as an accident could stall Pachli development.

So I am actively looking for additional people who want to join the project with a long term commitment. We'll see how that plays out over the next few years.

## Thank you

None of the above would have been possible without the contributions of many individuals, including:

From the [Nivenly Foundation](https://nivenly.org):

- [Quintessence Anx](https://hachyderm.io/@quintessence)
- [Dominic Harmon](https://hachyderm.io/@dma)

[Code, translations, and bug reports](https://github.com/pachli/pachli-android/graphs/contributors?to=08%2F09%2F2024&from=09%2F06%2F2023):

- [Aindriú Mac Giolla Eoin](https://github.com/aindriu80)
- [Angelo Suzuki](https://github.com/tinsukE)
- [Jener Gomes](https://github.com/JenerGomes)
- [jumase](https://github.com/jumase)
- [Kalle Kniivilä](https://github.com/kallekn)
- [Luna Jernberg](https://github.com/bittin)
- [Martijn de Boer](https://github.com/martijndeb)
- [Miles Krell](https://github.com/mileskrell)
- [Reza al Manda](https://github.com/rezaalmanda)
- [Ricky Lam](https://github.com/RickyLam11)
- [sanao](https://github.com/sanao1006)

Pachli has improved because the following people have taken the time to file bug reports:

- [Alexander Müller](https://github.com/nrgeen)
- [bakaminto](https://github.com/bakaminto)
- [Bryan Dion Greyson](https://github.com/BDGreyson)
- [caoilTe O'Connor](https://github.com/caoilte)
- [charlie2alpha](https://github.com/charlie2alpha)
- [Clément L.](https://github.com/Porkepix)
- [Daniele Conti](https://github.com/fourlastor)
- [Darryl Wright](https://github.com/punkscience)
- [Deividas Paukštė](https://github.com/KaiserCalm)
- [Eric Lathrop](https://github.com/ericlathrop)
- [Florian Berger](https://github.com/flberger)
- [foss-](https://github.com/foss-)
- [Graham](https://github.com/myfta)
- [Gregory Hammond](https://github.com/gregoryhammond)
- [Jasdemi](https://github.com/Jasdemi)
- [Korb](https://github.com/Korb)
- [lgasp](https://github.com/lgasp)
- [LucasGGamerM](https://github.com/LucasGGamerM)
- [mseifert](https://github.com/Doggy77)
- [Nitai Sasson](https://github.com/NeatNit)
- [Rainer Müller](https://github.com/raimue)
- [Sebastiano Poggi](https://github.com/rock3r)
- [vinzv](https://github.com/vinzv)

as well as many, many people who sent feedback on Mastodon.

Pachli, of course, started as a fork, and wouldn't exist without the work of the [Tusky contributors](https://github.com/tuskyapp/Tusky/graphs/contributors?to=09%2F08%2F2023).

Thank you to all of you, and apologies to anyone I missed.



