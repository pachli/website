---
layout: post
title: "Notification filters"
date: "2024-11-25 09:00:00 +0200"
categories: pachli
---
The first iteration of the account filtering work mentioned in [Anti-harassment controls](/pachli/2024/08/02/harassment-controls.html) is now in [Pachli Current](/download/#pachli-current).

<!--more-->

You can now choose how notifications from certain accounts are displayed, in "Account preferences > Notification filters".

<img alt="" src="/assets/posts/2024-11-xx-notification-filters/pref-notification-filters.png" class="shadow">

This will open a dialog with options for the three account categories, and a drop-down menu allowing you to choose from show, warn, or hide. The default behaviour is "show".

<img alt="" src="/assets/posts/2024-11-xx-notification-filters/dialog-notification-filters.png" class="shadow">

In this screenshot the option for accounts you don't follow is set to "Warn", and the menu for accounts created in the last 30 days is showing.

The criteria are:

- Accounts you do not follow
- Accounts created in the last 30 days
- Accounts limited by your server's moderators

For each of those categories you can choose to:

- Show the notification as normal
- Replace the notification with a warning, which you must click through
	- This applies within Pachli. There's no way to "click through to disclose" an Android notification, so this is treated as "Hide" when displaying Android notifications.
- Hide the notification completely

> **Note**: Notifications about:
>
> - Accounts you have opted in to be notified about (by tapping the "bell" icon on the account's profile page)
> - A poll you voted on
> - A change to a post you have boosted
> - Moderation reports
> - Moderator activity severing one or more of your following/follower relationships
> - (if you're an admin) New sign up report
>
> are never filtered. These are notifications about posts or accounts you have already interacted with. If you subsequently decide to ignore the account you can mute or block it.

The Notifications tab / screen shows notifications marked with a warning similarly to how posts matching a content filter are shown.

This screenshot shows three different types of notification, all filtered with a warning.

<img alt="" src="/assets/posts/2024-11-xx-notification-filters/filtered-notifications.png" class="shadow">

The notification header shows the underlying cause of the notification. The account's name is not shown as it might be a vector for abuse. The domain is shown as I think it's likely it is useful information when deciding whether or not to click through to show the notification.

Next is the reason the notification is filtered. If multiple reasons apply (e.g., you don't follow the account, and the account is less than 30 days old) only the first one that applies is shown.

Then there are two buttons; "Edit filter" opens the same options dialog from "Account preferences". "Show anyway" shows the notification.

## How does this interact with Mastodon's new notification filters?

Mastodon 4.3 released [new notification filtering options](https://blog.joinmastodon.org/2024/10/mastodon-4.3/#notifications).

This feature in Pachli is separate, as there are a number of problems with Mastodon's approach to filtering notifications.

1. Filtering decisions are made server-side, there's no mechanism for a client like Pachli to provide a more nuanced approach.
2. Filtering decisions are irrevocable in Mastodon. When a notification is created it is labelled with the filtering decision based on the existing set of filters. If you subsequently change those filters older notifications are not affected.
3. Account filters only apply to notifications, where they could be applied through the UI (as planned for Pachli).
4. The UX is inconsistent with filtering notifications for content. E.g,. if you switch to the "Filtered notifications" part of the Mastodon UI you see the notifications immediately. There's no interstitial to click through, so if the notifications are abusive you're immediately exposed to the abuse.

Also, of course, Mastodon's new notification filters only work if are using a server running a newer version of Mastodon. If you are using other software (e.g., GoToSocial) there is no notification filter support.

There is one feature planned for the Pachli implementation I've had to drop -- support for filtering notifications from accounts that don't follow you. Pachli would need to fetch details of the accounts that are following you, and for accounts with thousands of followers this would take too much time when switching accounts.

An issue ([Include \`relationship\` property in embedded \`Account\`s · Issue #33066](https://github.com/mastodon/mastodon/issues/33066)) has been filed with the Mastodon developer team to help fix this.

## Still to come

### Allow list support

I'm working on a mechanism to provide an allow-list of accounts that are ignored for these filters. This will be populated in a few ways.

1. If you have a filter set to "warn", and click through to see the notification, it will be easy to add the account to the allow-list so future notifications from the same account bypass the filters.

   At the moment if you click "Show anyway" on a filtered notification and then reload your notifications the "Show anyway" decision is not remembered.

2. If you interact with a post by replying, favouriting, bookmarking, or boosting it, the post's account will be added to the allow-list

There will be controls in the UI to let you manage the allow-list (view the accounts on the list, why the account was added to the list, and remove accounts from the list).

### Feedback on UX

Notifications filtered with a warning appear in the normal notifications timeline. This is consistent with how posts matching a content filter are displayed in timelines.

The Mastodon web UI puts filtered notifications in a separate area of the UI. I may experiment with that; feedback welcome.

### Feedback on filtering controls

The filters apply to all notifications irrespective of the notification's type (mention, boost, favourite, etc). That might be too broad.

For example, you might want to see all notifications about accounts boosting your posts, but place notifications about mentions from certain accounts behind a warning.

Also, unlike content filters, account filters are not time-limited, they apply until you change them. It may be appropriate to provide a time-limit option for each filter.

Suppose you make a popular post and suddenly receive a lot of notifications (replies, boosts, etc). You might want to disable those notifications from accounts you do not follow for only 24-48 hours until things return to normal.

This would make the UI more complicated, so I'm waiting for user feedback on whether these would be useful before embarking on it.

### Applying account filters elsewhere

The [Anti-harassment controls](/pachli/2024/08/02/harassment-controls.html) post discussed applying these filters elsewhere; your home timeline, conversations, and so on. That's coming, I'm launching this with notifications first to get early feedback.

### Distributed blocklist support

Also mentioned in the initial blog post, and also coming. Again, getting this working for local decisions and iterating on the UX for notifications is the priority.