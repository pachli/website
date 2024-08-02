---
layout: post
title: "Anti-harassment controls in Pachli 2.9.0"
date: "2024-08-02 12:00:00 +0200"
categories: pachli
---
I am planning on including features in Pachli 2.9.0 to help users manage and reduce the harassment they may encounter on Mastodon.

I need feedback on the features described in this post before I start the implementation.

<!--more-->

I am interested in feedback from the following constituencies:

- People who have experienced harassment on Mastodon
- People who have developed similar features in other clients, possibly on other networks

**If you have not experienced harassment on Mastodon, or actively worked on solutions before, then this discussion is not for you**. You can help by boosting the Mastodon post announcing this effort, and/or forwarding it to anyone you know who has faced harassment on Mastodon.

## Background

Pachli has a new release at the end of every month.

In any particular month there's a mix of bug fixing and working on one or two larger items to improve the user's experience.

For example:

- 2.2.0 - initial support for enabling/disabling features based on the user's server
- 2.3.0 - better media preview and playback, "check for update" functionality
- 2.4.0 - improved list management
- 2.5.0 - improved timeline management
- 2.6.0 - show suggested accounts
- 2.7.0 - warn if language appears incorrect, show a UI for search operators, show bylines

Pachli 2.8.0 (end of August 2024) is going to be the "fix notifications" release. I think I understand enough about the problem now to ensure notifications are delivered in a timely fashion.

After reading many threads on the topic it's clear Mastodon clients can do more to improve the experience of users who are facing harassment on Mastodon.

So I'm planning for Pachli 2.9.0 (end of September 2024) to focus on anti-harassment features.

> This list is ordered by the priority I currently think they should be implemented in. This understanding may change in response to feedback from others.

> These features are in addition to the existing support users have for filtering individual posts based on their content, blocking or muting an individual user, or blocking an entire domain from their account. Those are not being changed.

## Problems

I've determined an initial, tentative list of features to implement based on the following problems. See the "Nuance and caveats" section for additional information.

### Users are harassed by accounts on specific servers, and moderators on their own server are slow to block those servers

Pachli will allow users to enter at least one external blocklist by URL.

For example, the URL for one of the [oliphant.social blocklists](https://writer.oliphant.social/oliphant/the-oliphant-social-blocklist).

If selected then Pachli will periodically synchronise a copy of the blocklist and use it to filter your timelines. Any post from an account at a server on the blocklist is marked for filtering.

Like the existing content filtering functionality you will be able to decide whether the blocklist causes a post to be hidden entirely, or replaced with a warning and you can click through to see the post if you wish.

If you are following an account from a server on a blocklist the account's posts will not be filtered. Your choices of who to follow take precedence over the blocklist.

Pachli *may* come pre-configured with the URLs of some existing blocklists to allow the user to quickly select one or more without needing to know their URLs.

### Users are harassed by notifications they have been @-mentioned in by their harassers

Pachli will allow users to filter notifications according to any of the following criteria:

- Accounts they do not follow
- Accounts that do not follow them
- New accounts (younger than 30 days)
- Accounts limited by your server admins

In addition, if the user has selected to use an external blocklist then notifications from accounts on servers on the blocklist will also be filtered.

Like the existing content filtering functionality you will be able to decide whether the filters cause a notification to be hidden entirely, or replaced with a warning, and you can click through to see the notification if you wish.

Mastodon 4.3.0 provides notionally similar functionality. Pachli will implement this client side so the feature is not dependent on the upgrade schedule of the server they are using, and it will work if their server is not running Mastodon.

### Users face harassment in threads they have started

When viewing a thread Pachli currently shows you all posts in the thread (known to your server). This includes replies from accounts you do not follow.

Pachli will allow users to filter a thread to show only replies from accounts they follow.

Like the existing content filtering functionality you will be able to decide whether the filters cause a post to be hidden entirely, or replaced with a warning and you can click through to see the post if you wish.

### Users face harassment in conversations / direct messages

Pachli will allow users to filter "conversations" (often also called "direct messages" or "private messages", although the term is misleading), using the same criteria as notifications:

- Conversations initiated by accounts you do not follow
- Conversations initiated by accounts that do not follow you
- Conversations initiated by new accounts (younger than 30 days)
- Conversations initiated by accounts limited by your server admins

None of these will apply to conversations you initiate.

In addition, if the user has chosen to use an external blocklist then conversations initiated from accounts on servers on the blocklist will also be filtered.

Like the existing filtering functionality you will be able to decide whether the filters cause the initial post in a conversation to be hidden entirely, or replaced with a warning and you can click through to see the conversation if you wish.

### Easier access to "block" functions from a post

Blocking an account currently requires at least three taps; one on the post's "..." menu, one to choose "Block", and one to confirm.

A new preference to enable/disable the confirmation dialog for blocking an account will be provided, defaulting to "on" to match current behaviour. If "off" then two taps will be necessary to block an account.

The short-lived pop-up message that confirms an account has been blocked will include an "Undo" button to make it easy to revert mis-taps.

A "Show block button" preference will be introduced. If enabled this will add a "Block" button to the existing buttons at the bottom of each post ("Reply", "Boost", etc). This will default to "off", both to match existing behaviour, and because there is an accessibility trade-off when more buttons are added below each post. As more buttons are added the greater the risk the user taps the wrong button by mistake.

If the "Show block button" preference is on and the "Confirm before blocking an account" preference is off then accounts can be blocked with one tap.

A new preference, "Prompt to block domain when blocking account" will be introduced. If enabled, and after an account has been successfully blocked (whether that needed one, two, or three taps), the user will be asked if they want to block the domain as well. This makes the existing "Block domain" functionality more accessible.

### Improve the "Report account" UI

Currently, reporting an account allows you to choose one or more posts to include in the report, and you can provide additional commentary.

This will be extended to allow you to select one or more of the server's published rules you believe the account is violating.

This should allow your server's moderators to act faster when triaging and responding to the report.

## Nuance and caveats

### Adding accounts to an allow list

As already noted, any accounts you follow are exempt from the account filtering features described earlier.

In addition, if you choose to filter accounts behind a warning, and then click through the warning to see the filtered post (or notification) you will also have the option to add the account to an allow list, and future posts from the account will not be filtered.

### Accounts on your local server with roles are excluded from account filters

Accounts on your local server may have roles associated with them. Typically, `Owner`, `Admin`, or `Moderator`, although your server may be configured with additional roles (see [Roles - Mastodon documentation](https://docs.joinmastodon.org/admin/roles/) for more on this).

Any post or notification from an account on your local server with any role will be exempt from the account filtering described earlier. I assume you want to receive messages from your server's moderators.

Accounts on remote servers with roles **are not excluded** from the filtering.

### Some account data can be faked, bypassing account filters

A malicious remote server administrator could create an account today, and then adjust the account's creation date to months or years in the past. This would bypass any account filtering based on account age.

### Crafting the warning message

If you choose to replace a post with a warning the warning message has to show *some* information about the original post so you can make an informed decision about whether to click through.

At the moment I think the message will be similar to

> Post from a user @someserver.social<br>
> Hidden because {reason}

Where the {reason} is one of the filtering reasons mentioned earlier, for example "... you do not follow this account" or "... the account is < 30 days old".

The server name ("someserver.social" in this example) is included as it is probably the least useful vector for harassment.

Other data about the account, such as username, the display name (including emojis), and description can be used for harassment. Account metrics (e.g., the number of followers) can also be faked or used for harassment.

### Search results are not affected

These account filters will not apply to search results. I assume when you have explicitly searched for something you want to see unfiltered results.

### These are not a replacement for server changes

To be clear, these client improvements are not a replacement for changes at the server level. For example, filtering a thread to only show replies from people you follow will shield you from harassment, but the harassment is still visible to other people reading the thread.

## What do I need from you?

If you have experienced harassment on Mastodon and are prepared to talk about it I would like to hear from you.

I have some specific questions:

1. Will the features described above improve your experience?
2. Does the ordering of those features make sense? Do you consider any of them to be particularly important (or unimportant)?
3. Are there other client changes that could improve your experience?

But any other feedback is welcome.

To provide feedback (in order of preference):

- I do not expect you to discuss your experiences of harassment in public, so private feedback can be sent by e-mail to [team@pachli.app](mailto:team@pachli.app).
- If you do want to provide long-form public feedback please use the [Harassment controls discussion](https://github.com/pachli/pachli-android/discussions/864) in the Pachli forum
- Feedback can also be sent to the [@pachli@mastodon.social](https://mastodon.social/@pachli) account

## FAQ

### Isn't this a blocklist? I think blocklists are bad.

This is not a blocklist. It's using a blocklist to apply filters at the client level. It does not block accounts at the server.

This avoids concerns people have expressed with server-level blocklists, including

**Server-level blocklists have no opt-out**: here the choice to use a given blocklist to drive filtering decisions is entirely the user's.

**Server-level blocklists affect everyone on the server**: here the choice to use a given blocklist affects just the user who makes the decision.

**Server-level blocklists can break follower relationships**: by using the blocklist to drive content filtering decisions the user's follower relationships are not disrupted, and the user's choice to follow a user always takes precedence over the blocklist.

### Will all of this land in 2.9.0?

Depends on how difficult the work is and user feedback.

The list of features above is organised by expected priority, so they'll land in roughly that order. Since there's ~ 4 weeks between each release some features might only be finished for releases after 2.9.0.

And of course, the list of features above, or the specific functionality described, or the prioritisation, may change in response to feedback.