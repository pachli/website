---
layout: post
title: "Opt-in crash reporting"
date: "2023-12-12 22:00:00 +0200"
categories: pachli
---

If Pachli Current crashes it's very helpful if the developers can see exactly where it crashed. Sometimes that's obvious from bug reports, or the problem is easy for the developers to reproduce. And reproducing a problem is the first step to fixing it.

And sometimes the information is just not available to the user, or the problem is not easy to reproduce.

For example, [bug report #306](https://github.com/pachli/pachli-android/issues/306).

To make this easier the most recent release of [Pachli Current](/download#pachli-current) catches crashes, records concrete information about where the crash occurred and what was happening at the time, and allows you to opt-in to sending it to the developers.

**No information is ever sent to the developers without your express permission. The crash-handling code is not present in the regular Pachli application.**

<!--more-->

If Pachli Current crashes you will see the following dialog:

![Screenshot showing Pachli Current crash dialog](/assets/posts/2023-12-xx-crash-reporting/crash-dialog.png)

This is your first opportunity to opt-out. If you click "Cancel" then the crash report is ignored and no information is sent.

If you click OK an e-mail is prepared and your e-mail client is launched. The e-mail looks like this:

![Screenshot showing Pachli Current crash e-mail](/assets/posts/2023-12-xx-crash-reporting/crash-email.png)

This is your second opportunity to opt-out. If you do not send the e-mail then the crash report is ignored.

Per the instructions you can provide additional context about what you were doing when the crash occurred.

The bulk of the e-mail is information about your device (hardware, Android version, etc), the version of Pachli Current that crashed, and the place in the code where the crash occurred.

You can review this information and choose to redact any of it if you wish.

Obviously, sending the e-mail will share your e-mail address with the developers. It will **only** be used to contact you if more information is needed to help solve the problem or to verify the problem is solved.