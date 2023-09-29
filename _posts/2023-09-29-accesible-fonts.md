---
layout: post
title: "Accessible fonts"
date: "2023-09-29 12:00:00 +0200"
categories: pachli
gallery:
  images:
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_system_default.png
      title: System default
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_atkinson_hyperlegible.png
      title: Atkinson Hyperlegible
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_comic_neue.png
      title: Comic Neue
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_estedad.png
      title: Estedad
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_lexend.png
      title: Lexend
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_luciole.png
      title: Luciole
    - src: /assets/posts/2023-09-xx-accessible-fonts/pangram_opendyslexic.png
      title: OpenDyslexic
---
To improve accessibility Pachli allows the user to change the font used in the UI.

The feature originated from work I was doing on the Tusky client. I had seen occasional user requests asking for different fonts, either to improve overall legibility, or specifically to assist people with dyslexia.

I put together a proof-of-concept using [Atkinson Hyperlegible](https://brailleinstitute.org/freefont) from the Braille Institute and [OpenDyslexic](https://opendyslexic.org/) as they are both freely available and claim to be helpful.

This allowed me to experiment with the UX and identify any issues that might make adopting this difficult.

This is not an accessibility issue I currently have to contend with, so I approached the user community for feedback and recommendations for additional fonts, asking:

<!--more-->

> If you have #dyslexia, do alternative fonts in apps help with the reading experience?
>
> If yes, are Atkinson Hyperlegible or OpenDyslexic useful fonts to use with #Tusky? Are there others (that are freely redistributable).
>
> The attached screenshots show what this would look like.
>
> Please boost for reach.
>
> \- [https://mastodon.social/@Tusky/110741534444074976](https://mastodon.social/@Tusky/110741534444074976)

Reading the thread a few things quickly became apparent.

- There was definitely demand for this feature
- Research on the effectiveness of some fonts was, at best, inconclusive
- Nevertheless, individual reports showed while a given font might not be effective across a broad population, some people would still benefit from its inclusion
- There were a number of other fonts people were quick to recommend

There were also a number of requests to allow the user to choose any font from a font provider like [Google Fonts](https://fonts.google.com/). I choose not to in this first version of the feature as I already had a working prototype with embedded fonts, and extending it would introduce three additional issues:

1. Google Fonts has ~ 1,500 fonts. The UX to select from those is very different from the UX to select between a small number of options
2. Using Google Fonts needs the user to have a device with Google Play Services
3. Some of the user recommended fonts are not available on Google Fonts, so support for embedded fonts would still be necessary

Based on user recommendations the initial set of fonts, and the descriptions from their websites, are:

**[Atkinson Hyperlegible](https://brailleinstitute.org/freefont)**, "*named after Braille Institute founder, J. Robert Atkinson.  What makes it different from traditional typography design is that it focuses on letterform distinction to increase character recognition, ultimately improving readability.*"

**[Comic Neue](https://comicneue.com/)** "*aspires to be the casual script choice for everyone including the typographically savvy. The squashed, wonky, and weird glyphs of Comic Sans have been beaten into shape while maintaining the honesty that made Comic Sans so popular.*"

**[Estedad](https://github.com/aminabedi68/Estedad)** "*("Talent" in Persian) is an Arabic-Latin Sans-Serif typeface in 9 standard weights. Estedad has wide codepoint range support for most Arabic and Latin languages. The design is simple, smooth, compact, legible, low contrast, lowest optical size (a bit higher in bold and above weights) and optimized for web-like environments.*"

**[Lexend](https://www.lexend.com/)** "*is a variable typeface designed by Bonnie Shaver-Troup and Thomas Jockin in 2018. Applying the Shaver-Troup Individually Optimal Text Formation Factors, studies have found readers instantaneously improve their reading fluency.*"

**[Luciole](http://www.luciole-vision.com/luciole-en.html)** "*(French for “firefly”) is a new typeface developed explicitly for visually impaired people. The result of a two-year collaboration between the Centre Technique Régional pour la Déficience Visuelle (the Regional Technical Center for Visual Impairment) and the type-design studio [typographies.fr](typographies.fr), this project received a grant from the Swiss Ceres Foundation and support from the DIPHE laboratory at the Université Lumière Lyon 2.*"

**[OpenDyslexic](https://opendyslexic.org/)** "*is a new open sourced font created to increase readability for readers with dyslexia.*"

When used (at the "small" font size) these look like this:

{% include image-gallery.html folder="/assets/posts/2023-09-xx-accessible-fonts" %}

To choose a different font open Pachli "Preferences" and select one from the "Font family" option.

All of this work was originally done for Tusky in [pull request #3288](https://github.com/tuskyapp/Tusky/pull/3288) starting in February 2023.

There was insufficient interest from the other Tusky contributors to merge the work, but given the significant amount of user support in the thread it was an obvious candidate to include in Pachli 1.0.
