---
layout: post
title: "Displaying quote posts"
date: "2025-11-13 23:00:00 +0200"
categories: pachli
---
Pachli Current is rolling out with support for viewing posts containing quotes on [supported Mastodon servers](https://blog.joinmastodon.org/2025/11/mastodon-4.5/).

What you should expect:

<!--more-->

> Important: Today's features are about displaying quotes. Creating posts quoting other posts, displaying notifications about quote posts, managing your settings for allowing people to quote your posts, etc. is not ready yet. The work is ongoing and will launch soon.

## General display

Posts quoting other posts display the quoted-post below the quoting-post.

<img alt="Post with a quote" src="/assets/posts/2025-11-xx-quote-posts/post-with-quote.png" class="shadow" 
 width="486" height="522">

Quotes are separated from the rest of the content with a different background.

The content in the quoted-post is scaled down a little; smaller avatar icon and text size, to make it less prominent.

As the screenshot shows, hashtags, links, and other clickable items in the quoted-post work as normal.

- If the quoted-post has a content warning you can tap through to view the post's body.
- If a quoted post has attachments you can open them.
- If a quoted post has a poll you can vote on it.

## Content filters

If the quoting-post doesn't match one of your warning filters, but the quoted-post does, the normal warning is shown on the quoted-post.

This screenshot is the same post as the previous. The quoting-post does not match the filter, the quoted-post does.

<img alt="Post with a filtered quote" src="/assets/posts/2025-11-xx-quote-posts/post-with-filtered-quote.png" class="shadow" width="486" height="366">

You can click through to display the quoted-post in-situ.

If the quoted-post matches a filter set to "Hide" the quoted-post *is not* completely hidden. Instead, a placeholder is shown. Without this the quoting-post may be missing important context and be confusing. The name of the matching filter is deliberately not shown, nor can you click through to view the filtered quote.

<img alt="Post with a hidden quote" src="/assets/posts/2025-11-xx-quote-posts/post-with-hidden-quote.png" class="shadow" width="486" height="253">


## Accessibility

If a post contains a quote there's a new "Open quoted post" accessibility action. There is **not** accessibility support for e.g., expanding content warnings on quoted posts, or viewing the individual attachments. This would significantly increase the number of accessibility actions to choose from, and I am concerned this may be overly complicated

So the "Open quoted post" action is a compromise -- you open the quoted post first, then you use the accessibility actions on it.

I may well be wrong about this, so if you use accessibility actions I would really appreciate your feedback.

## Missing display features

I know some display features are missing, they're coming. They are (at least):

- A setting to control whether the quoted-post is shown above or below the quoting-post.
- Translating a quoting-post does not also translate the quoted-post.
- If you tap through a post to view the details it does not show the number of quotes. 

## Feedback

If possible, please provide feedback on [GitHub issue #1801](https://github.com/pachli/pachli-android/issues/1801).

{% include playlink.html link="Download Pachli Current from Google Play" app="app.pachli.current" campaign="quote-posts-1" content="textlink" %}, or the [GitHub release page](https://github.com/pachli/pachli-android/releases/tag/v3.1.0).