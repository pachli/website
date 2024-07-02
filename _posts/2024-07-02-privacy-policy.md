---
layout: post
title: "Privacy policy update for Pachli from Google Play"
date: "2024-07-02 18:00:00 +0200"
categories: pachli
---
A new feature launching in Pachli Current now requires a small update to the Pachli privacy policy.

Read on for details.

<!--more-->

Mastodon expects you to accurately set the language of your post before posting.

There are real-world accessibility problems if you set it incorrectly, including:

(a) Mastodon's translation feature may not work correctly

(b) when people follow you they can opt-in to only receive posts you send in a particular language. If you mis-label the language of your posts you may be inadvertently spamming your followers.

A new feature in Pachli helps to fix this. Before sending a post Pachli will check the language the post is written in. If the language doesn't appear to match the language you've chosen you'll be warned about this, and have the option to change the language, or continue with the post as is.

![Interstitial language warning dialog](/assets/posts/2024-07-xx-privacy-policy/language-warning.png)

This feature is rolling out in [Pachli Current](https://play.google.com/store/apps/details?id=app.pachli.current) now.

If you have installed Pachli from [F-Droid](https://f-droid.org/en/packages/app.pachli/) or the [GitHub Release](https://github.com/pachli/pachli-android/releases) and are on a device running Android 10 or above (released 2019) this uses built-in Android libraries to detect the language.

If you have installed Pachli from [F-Droid](https://f-droid.org/en/packages/app.pachli/) or the [GitHub Release](https://github.com/pachli/pachli-android/releases) on a device older than Android 10 the the feature is not available.

If you have installed Pachli from Google Play this feature uses Google's [ML Kit Language Identification library](https://developers.google.com/ml-kit/language/identification) to identify the language. This works on all devices Pachli runs on, from Android 6 and above.

In all cases **none of the text you enter is ever sent to Google**.

If you have installed Pachli from Google Play, [ML Kit may send and receive some data from Google's servers](https://developers.google.com/ml-kit/terms). To quote from that page (emphasis added):

> When you use ML Kit APIs, processing of the input data (e.g. images, video, text) fully happens on-device, and **ML Kit does not send that data to Google servers**. As a result, you can use our APIs for processing data that should not leave the device.
>
> The ML Kit APIs may contact Google servers from time to time **in order to receive things like bug fixes, updated models and hardware accelerator compatibility information**. The ML Kit APIs also **send metrics about the performance and utilization of the APIs in your app to Google**. Google uses this metrics data to measure performance, debug, maintain and improve the APIs, and detect misuse or abuse, as further described in our [Privacy Policy](https://policies.google.com/privacy).

Accordingly, the [Privacy Policy](/privacy/) has been updated to note that, if you install Pachli from Google Play, some ML Kit statistics are sent to Google, and ML Kit may download updated language identification models to your device.

## Possible questions

### Which version of Pachli will this apply from?

Pachli Current as of today, July 2nd 2024.

Pachli 2.7.0, which is not released, but should be released some time in the last week of July.

### Why use ML Kit at all?

ML Kit allows the feature to be implemented (for some users) on the earliest devices Pachli supports.

This is not a theoretical problem. The [Let's Encrypt certificate issue](/pachli/2024/04/29/2.5.0-release.html#android-7-devices-and-lets-encrypt) I had to work-around in Pachli 2.5.0 was raised by real users having a real problem on older devices.

### Are there open source alternatives to ML Kit?

Not that work. The most promising is [Lingua](https://github.com/pemistahl/lingua) but it is not designed for this use case; simply loading all the language models so it can implement detection and suggest an alternative crashed Pachli on my Pixel 4a after to trying to use all available memory.

### How do I opt out?

Install Pachli from [F-Droid](https://f-droid.org/en/packages/app.pachli/) or the [GitHub Release](https://github.com/pachli/pachli-android/releases) page.

ML Kit is not something that can be disabled at run-time, so there is no mechanism to provide a "Disable ML Kit" or similar option in the preferences.

### How do I see my device's Android version?

Open Pachli's "About" screen. In the "Your device" section your device's Android version is shown.

### Does Pachli send any data to Google or other companies?

No. Pachli only communicates with the server(s) associated with your account(s).