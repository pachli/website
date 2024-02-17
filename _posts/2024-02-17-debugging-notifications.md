---
layout: post
title: "Debugging notifications"
date: "2024-02-17 09:00:00 +0200"
categories: pachli
---
Pachli started as a fork of Tusky so has inherited some of Tusky's bugs, which are now being fixed.

One of those is users reporting they never receive Android notifications for Mastodon events; when someone follows you, or replies to one of your posts, or a poll you've voted on closes, etc.

The Mastodon notifications still appear in the app, but never as Android notifications.

This has been difficult to fix because it's not reproducible by the developers. When my account (or the [@pachli@mastodon.social](https://mastodon.social/@pachli) account) receives a Mastodon notification it appears as an Android notification on my phone within seconds, exactly as it's supposed to.

To better understand what's going on the version of Pachli Current rolling out now -- and the next version of Pachli -- includes comprehensive information about how Pachli is getting your Mastodon notifications, what you might need to do to improve the situation on your device, and a mechanism to report logs to the developers to help with bug hunting.

<!--more-->

# Mastodon notifications and Android notifications

The term "notification" is overloaded, so the rest of this post differentiates between Mastodon notifications and Android notifications.

A Mastodon notification is the message from your server that someone has done something you want to be notified about; boosted a post, replied, etc.

An Android notification is how the Mastodon notification is displayed with the rest of your device notifications; in a pull-down shade where you can dismiss it, tap on it to open Pachli, press buttons to immediately reply, and so on.

So Pachli has to **receive** Mastodon notifications in order to **create and show** Android notifications.

Through the rest of this post "Mastodon" is shorthand for "Mastodon, and any other server software that implements notifications the same way".

# Seeing how Mastodon notifications are delivered

If you are experiencing delayed Mastodon notifications on your device open the "About" screen from the left side navigation menu and open the new "Notifications" tab.

This has a child "Details" tab, split in to a number of sections.

# Section "Android notifications are enabled?"

This section covers whether Pachli should be fetching Mastodon notifications at all, and if so, how Pachli determines new Mastodon notifications are available.

Pachli checks to see if you have enabled at least one type of Android notification across all of the accounts you have signed in to Pachli. If you have not enabled those Android notifications then Pachli will never fetch Mastodon notifications.

You should see a list of your signed accounts with either a "✔" or a "✖" next to each one.

A "✔" means this account has at least one Android notification type enabled.

A "✖" means this account has no Android notifications types enabled.

At least one of your signed in accounts must have Android notifications enabled, so you must see at least one "✔". If you do not then notifications are disabled.

If there is a "✖" next to an account and you think the account should be receiving Android notifications then open "Account preferences > Notifications" for the account in Pachli. You should see you a list of the different Android notification channels Pachli uses; there's one for boosts, one for favourites, one for follow requests, etc. Enable at least one of them.

If there are no Android notification channels then that's a bug. See later for how to report it.

If Android notifications *are* enabled then below the list of accounts is an explanation of how Pachli becomes aware of new Mastodon notifications.

If Android notifications are not enabled then the rest of the information on this screen is hidden.

> **Push and pull notification mechanisms**
>
> Either your Mastodon server pushes Mastodon notifications to Pachli when they happen or Pachli has to periodically check and see if new Mastodon notifications are available (we say Pachli "pulls" the Mastodon notifications from your server).
>
> Using the push method should use less energy, and should deliver Mastodon notifications much more quickly, so is the recommended approach.
>
> However, for the push method to work you must install another open source application that acts as a bridge between your server and applications like Pachli that want to receive Mastodon notifications.
>
> If this application is not installed then Pachli will fall back to pulling Mastodon notifications from your server; approximately every 15 minutes it will contact your server and see if there are new Mastodon notifications, and if there are Pachli creates the Android notifications.

---

# Section "Push notifications with UnifiedPush"

This section describes how Mastodon push notifications are configured.

This section is shown even if you have not enabled Mastodon push notifications so you can see which steps need to be completed.

You can skip to ["Pull notifications with periodic workers"](#section-pull-notifications-with-periodic-workers) if you don't want to use pull notifications for some reason.

## "UnifiedPush is available?"

For Mastodon push notifications to work you must install the open source *ntfy* application.

- [Get ntfy from Google Play](https://play.google.com/store/apps/details?id=io.heckel.ntfy)
- [Get ntfy from F-Droid](https://f-droid.org/en/packages/io.heckel.ntfy/)

If it is installed then this section will be checked. If it is not then first install *ntfy*, then come back to Pachli and refresh this screen.

If you have installed *ntfy* and this section is **not** checked then please [report a bug](#using-this-information-and-reporting-problems).

## "All accounts have 'push' OAuth scope?"

Your Mastodon account allows applications like Pachli to act on your behalf. When Pachli registers with your server it requests a set of permissions it needs; permissions like sending posts, adding to bookmarks, uploading media, and so on.

We call those permissions "scopes".

To receive Mastodon push notifications from your server Pachli needs the `push` scope. It should have been requested when you first signed in to your account with Pachli, and your server should have approved the request.

You should see a list of your signed in accounts with either a "✔" or a "✖" next to each one.

A "✔" means this account has the `push` scope and Pachli can receive Mastodon push notifications for this account.

A "✖" means this account does not have the `push` scope.

> **Important**: All accounts must have the `push` scope
>
> If one or more accounts do not have the `push` scope then Mastodon push notifications are disabled for all accounts and Mastodon notifications will be pulled.

To try and fix an account without the `push` scope you can log out of the account in Pachli and then log back in. Pachli will re-request the `push` scope when you log in.

> **Warning**: Data deletion
>
> This will delete your local data for the account, including your Pachli account settings and any drafts for the account, so only do this if you are comfortable deleting the data.

If this does not fix the problem this may be an issue with your server or with Pachli. Please [report a bug](#using-this-information-and-reporting-problems).

## "All accounts have a UnifiedPush URL?"

When your Mastodon server wants to send Pachli a Mastodon push notification it sends the information to a special URL. The *ntfy* application manages this, and the URL is stored in your Pachli account.

You should see a list of your signed in accounts with either a "✔" or a "✖" next to each one.

A "✔" means the server for this account knows the URL to send Mastodon notifications to

A "✖" means there was an error when sending the server information about the URL, and no Mastodon notifications will be received for this account.

To try and fix an account without the URL you can log out of the account in Pachli and then log back in. Pachli will re-send the URL to your server when you log in.

> **Important**: Data deletion
>
> This will delete your local data for the account, including your Pachli account settings and any drafts for the account, so only do this if you are comfortable deleting the data.

If this does not fix the problem this may be an issue with your server or with Pachli. Please [report a bug](#using-this-information-and-reporting-problems).

## "All accounts are subscribed?"

You should see a list of your signed in accounts with either a "✔" or a "✖" next to each one.

A "✔" means this account is correctly set up for Mastodon push notifications

A "✖" means this account is not set up for Mastodon push notifications, and should show an error explaining why

## "NTFY is exempt from battery optimization"

Although your accounts may be configured correctly there is only more problem, Android power management. To preserve battery life Android may limit how often *ntfy* can run and receive Mastodon notifications.

To prevent this you must exempt *ntfy* from Android's power optimizations.

To do this open *ntfy*. You should see a message at the top of the *ntfy* screen telling you battery optimization should be disabled with a "Fix now" option; use that to find the entry for *ntfy* in your device's power management settings and ensure it is allowed "Unrestricted" use.

If you do not do this then *ntfy* may be slow to receive the Mastodon notifications from your Mastodon server and pass them on to Pachli.

---

# Section "Pull notifications with periodic workers"

This section is only displayed if Mastodon notifications are being periodically pulled, instead of pushed via *ntfy*.

Android limits applications to doing this at most once every 15 minutes, and depending on your battery optimisation settings it may be much less frequent.

## "Pachli is exempt from battery optimization?"

Android can restrict applications like Pachli from working in the background. To quote the developer documentation:

> If a user leaves a device unplugged and stationary for a period of time, with the screen off, the device enters Doze mode. In Doze mode, the system attempts to conserve battery by restricting apps' access to network and CPU-intensive
services. It also prevents apps from accessing the network and defers their jobs, syncs, and standard alarms.
> \- [https://developer.android.com/training/monitoring-device-state/doze-standby](https://developer.android.com/training/monitoring-device-state/doze-standby)

If this happens then Android may limit or stop Pachli's periodic checks for new Mastodon notifications.

To change this you can exempt Pachli from these optimisations.

How to exempt Pachli from these optimisations will vary from device to device and manufacturer to manufacturer. On my Pixel 4 running Android 14 this is:

1. Open the device's system settings
2. Open "Apps"
3. Find and open "Pachli" or "Pachli Current" in the list
4. Open "App battery usage"
5. Change from "Optimised" to "Unrestricted"

If you do this -- or the equivalent on your device -- you should see a check next to the "Pachli is exempt from battery optimization" message.

## Worker list

To pull Mastodon notifications Pachli configures a "periodic worker". This should run approximately once every 15 minutes.

This section should show you exactly one entry for a worker. There will be a long string of text as the worker's ID, followed by `ENQUEUED`, indicating it is waiting to run, and the time when it is next scheduled to run.

This scheduled time is the *earliest* time Android will run the worker. If the worker cannot be run then -- e.g., because the device is not connected to a network -- Android will delay starting the worker.

If you leave this screen open -- and the device is connected to the network -- you should see the `ENQUEUED` briefly change to `RUNNING` shortly after the scheduled start time when Pachli checks for new Mastodon notifications, then switch back to `ENQUEUED` with an updated scheduled start time.

---

# Section "Last /api/v1/notifications request"

This section is displayed whether Pachli is using push or pull for Mastodon notifications.

You should see a list of your signed in accounts with either a "✔" or a "✖" next to each one.

A "✔" means the most recent attempt to fetch Mastodon notifications for this account succeeded.

A "✖" means the most recent attempt to fetch Mastodon notifications for this account failed. There should be an explanation for the failure after the account details.

Below each account is the time of the last attempt.

For Mastodon push notifications this should be very close to the time of your last real Mastodon notification.

For Mastodon pull notifications this should be within the last ~ 15 minutes, assuming Pachli is exempt from battery optimisation and was connected to the network. If Pachli is not exempt from battery optimisation or did not have network connectivity this may have been hours ago.

---

# Section "Power management restrictions"

To better understand how Android might be restricting Pachli's ability to work in the background, including fetching Mastodon notifications, the "Power management restrictions" section shows details of when Android changed Pachli's background restrictions.

This is a list of changes, most recent first, covering the last three days.

If you see:

- "Exempted" -- Pachli is exempt from all restrictions because you set it to be exempt from battery optimisation. Push notifications should be almost immediate, pull notifications should be every ~ 15 minutes as long as the device has a network connection
- "Active" -- like "Exempted", but because you actively using Pachli, or were using it very recently
- "Working set" -- Pachli has not been used for a while, and Pachli can do at most 10 minutes of background work every two hours. This should be sufficient to fetch notifications

Anything else indicates Pachli may be being prevented from performing background work, including fetching and displaying notifications.

---

# The "Log" tab

The log tab contains additional logs for developers trying to debug the problem, but may also help you determine what is wrong if you have a technical background. Every ~ 12 hours the logs are pruned to remove any entries more than two days old.

The "Filter" button is used to filter the shown logs by their priority. By default all logs are shown, but you can choose to, for example, only show warnings, errors, or assertion failures.

Use the "Sort newest first" checkbox to switch the log display from oldest log entries first (the default) to newest first.

The "Download" button will save a copy of the logs, and the information from the "Details" tab to your device. From there you can send it to the developers or attach it to a bug report. See the next section for more information.

# Using this information and reporting problems

If you are experiencing delays seeing Mastodon notifications in Pachli you should:

1. Verify the "Details" tab shows [Android notifications are enabled for at least one account](#section-android-notifications-are-enabled). If no accounts have notifications enabled you will need to fix that first.

2. Then decide if you want to use push or pull notifications. We strongly recommend push notifications for the best experience.

   a. To use push notifications install *ntfy* and verify [push notifications are configured correctly](#section-push-notifications-with-unifiedpush).

   b. To use pull notifications ensure Pachli is [exempt from battery optimisation](#section-power-management-restrictions).

If you have done this and notifications are still delayed, or any of the sections shows an error you do not understand you can report an issue and we can investigate.

The most effective way to report an issue is via GitHub. You can [search the list of existing issues](https://github.com/pachli/pachli-android/issues) to see if anyone else has reported the same issue, or has suggested a workaround. If you cannot find a related issue then you can [report a new issue](https://github.com/pachli/pachli-android/issues/new?assignees=&labels=&projects=&template=bug_report.md&title=).

If you cannot use GitHub you can also e-mail [team@pachli.app](mailto:team@pachli.app).

Whichever method you use please download a copy of the notification details and logs, and either attach it to the GitHub issue or to the e-mail. Without this information it is very unlikely we will be able to help.

To download the information tap the "Download" button on the "Log" tab. You will be prompted for a location to save the file (the default is the "Downloads" folder on your device).

This file will contain a text copy of the information on the "Details" and "Log" tabs, and you should attach it to the bug report or the e-mail.

> **Important**: Consider the contents of the log before sharing
>
> The downloaded file contains some data from all the accounts you have signed in to Pachli. This means:
>
> - If you have multiple accounts that are not normally publicly linked or known to be owned by you this link will be disclosed.
> - By sending the logs via e-mail the developers will know an e-mail address associated with the accounts
> - By attaching the logs to a GitHub issue anyone viewing the issue can associate your GitHub account with your Mastodon accounts
>
> You are encouraged to review this file before sending it to ensure it does not contain information you want to keep private.