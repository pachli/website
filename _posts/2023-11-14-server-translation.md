---
layout: post
title: "Supporting server translation"
date: "2023-11-14 12:00:00 +0200"
categories: pachli
---

> Edit: This feature is now also available in Pachli 2.0.0.

[Pachli Current](/download) (on [Google Play](https://play.google.com/store/apps/details?id=app.pachli.current)) now supports server-side translation of posts.

This means the translation does not happen on your device. Instead (and if your Mastodon provider is configured to support it) Pachli asks your Mastodon provider to translate the post, and they, in turn, typically contact a third-party translation service (often DeepL.com) to do the actual translation. Then a copy of the translation is sent back to Pachli.

This comes with a few caveats and additional details.

<!--more-->

---

## Which versions of Pachli support translation?

At the time of writing, Pachli Current.

Translation support is the feature gating the release of Pachli 2.0, so once this has had some real-world testing from users of Pachli Current this will also be in Pachli 2.0.

## How do I translate a post or undo a translation?

Tap the "..." menu at the bottom right of the post, and choose "Translate" or "Undo translate" as appropriate.

![Screenshot showing the "Translate" menu for a post](/assets/posts/2023-11-xx-server-translation/translate-menu.png)

A "Translating..." message will appear under the post while translation is happening.

![Screenshot showing Pachli Current translating a post](/assets/posts/2023-11-xx-server-translation/translating.png)

 When translation is complete the content of the post is updated and information about the translation provider is shown below the post.

![Screenshot showing a translated post in Pachli Current](/assets/posts/2023-11-xx-server-translation/translated.png)

If the translation process fails then an error message is shown, and you may be able to retry.

## Why is this behind a menu?

I considered making this part of the "action" buttons at the bottom of a post (reply, boost, favourite, bookmark) and decided against it.

Not all servers support translation and not all posts can be translated (see [Why is the "Translate" option not in the post's menu?](#why-is-the-translate-option-not-in-the-posts-menu)).

So the buttons might shift position as the "Translate" button was present on some posts but not others. This is bad for users' muscle memory as it makes it easier to tap the wrong button.

Sometimes that's OK but sometimes it's not; for example, mistakenly bookmarking a post is OK, but favouriting or boosting a post causes your account do something that's publicly visible, and Pachli errs on the side of caution for actions that are public.

Always showing the a translate button but disabling it some of the time was rejected; it prevents the muscle-memory problem but it reduces the space available for the other "action" buttons which are already quite narrow. Making them narrower risks introducing an accessibility problem.

I also expect this feature will -- for the majority of users -- be used far less frequently than the other action buttons, so putting it behind a menu that requires an additional press to activate seems like a reasonable compromise.

## What parts of a post are translated?

Translation can change all of the following in a post:

- The content warning (if present)
- The text of the post
- The options in a poll (if present)
- The descriptions on any media attachments (if present)

If a post has been edited only the most recent version of the post can be translated.

## How do I stop posts being sent to third parties like DeepL?

At the moment you can't, it is managed by server administators.

A future version of Pachli will include an option to perform translation entirely on your device.

## Why is the "Translate" option not in the post's menu?

Any of the following reasons.

1. You are looking at the post on anything **except** your home timeline. In Pachli 2.0 translation is only available for posts on the home timeline. This will be fixed in a future release and translation will be available on all timelines.
2. Your Mastodon server is too old. Translation became available in Mastodon 4.0.
3. Your Mastodon server is version 4.0 or later, but your server administrators have not enabled the translation functionality.
4. The post was marked private (can be seen by followers and mentioned users) or direct (can only be seen by mentioned users); Mastodon does not support translating private or direct posts

## The translation is wrong

As the translation is carried out by a third party service there is nothing Pachli can do about this.

## Translating a post showed an error message

The translation service may fail. If this happens a message will pop up at the bottom of the screen with details about the failure.

There is nothing Pachli can do about this, but your server administrators may be interested in the details of the failure.

## Translating a post didn't change the text of the post

The translation service might send back an untranslated copy of the post. This could be because:

1. The post's author did not set the language of their post correctly. Suppose your account is configured to use English, you're reading a post written in German, but the post's author said the post was written in English. Pachli still sends the post for translation, but your Mastodon server will refuse to translate it. This is tracked as Mastodon bug [#1330](https://github.com/mastodon/documentation/issues/1330).
2. The service can not translate the language the post was written in. Different services will support different languages. For example, [DeepL API: get-languages](https://www.deepl.com/docs-api/general/get-languages/) shows the list of languages DeepL supports.
3. The service had some other problem translating the post, but did not report the error back.

In these cases there is nothing Pachli can do about this, but your server administrators may be interested in receiving a problem report.

{% include playlink.html link="Download Pachli Current from Google Play" app="app.pachli.current" campaign="blog" content="textlink" %}.