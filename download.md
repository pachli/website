---
layout: page
title: Install Pachli
permalink: /download/
---
# Choose a variant

Pachli is available in two variants:

- **Pachli** is the regular variant, released every month.
- **Pachli Current** is the pre-release variant, with new features and bug fixes that benefit from wider testing. Installing Pachli Current and [reporting any bugs](https://github.com/pachli/pachli-android/issues/new/choose) you find is a very useful way to contribute to the project.

Pachli and Pachli Current can be installed at the same time and the two variants do not share any data.

![Screenshot showing Pachli and Pachli Current installed together](/assets/download/pachlis.png)

# Pachli

Pachli is updated at least once a month, typically at the end of each month.

Install from {% include playlink.html link="Google Play" app="app.pachli" campaign="download" content="textlink" %}, [F-Droid](https://f-droid.org/packages/app.pachli), [GitHub](https://github.com/pachli/pachli-android/releases/latest), or GitHub with [Obtainium](obtainium://add/github.com/pachli/pachli-android).

{% include playlink.html link='<img alt="Get Pachli on Google Play" width="207" height="80" src="/assets/download/google-play-badge.png"/>' app="app.pachli" campaign="download" content="buttonlink" %} [<img src="/assets/download/fdroid-badge.png" alt="Get Pachli on F-Droid" width="207" height="80">](https://f-droid.org/packages/app.pachli) [<img alt="Get Pachli with Obtainium" width="207" height="80" src="/assets/download/obtainium-badge.png"/>](obtainium://add/github.com/pachli/pachli-android)

Each release has an associated article on this site and release announcement from the [@pachli@mastodon.social](https://mastodon.social/@pachli) account.

New releases appear on GitHub immediately.

New releases are typically approved on Google Play within 12-24 hours.

The release is then made available to an increasing percentage of the users every day. This helps catch issues that were not caught in Pachli Current.

| Day                  | Percentage |
|----------------------|------------|
| Release day          | 10%        |
| Release day + 1 day  | 30%        |
| Release day + 2 days | 70%        |
| Release day + 3 days | 100%       |

So the new release will normally be available to you within four days of the release announcement.

There is typically a 3-5 day delay before a new release is available on F-Droid.

# Pachli Current

Pachli Current is typically updated once or twice a week.

Pachli Current can be installed from {% include playlink.html link="Google Play" app="app.pachli.current" campaign="download" content="textlink" %}, [GitHub](https://github.com/pachli/pachli-android-current/releases/latest), or GitHub with [Obtainium](obtainium://add/github.com/pachli/pachli-android-current).

{% include playlink.html link='<img alt="Get Pachli Current on Google Play" width="207" height="80" src="/assets/download/google-play-badge.png"/>' app="app.pachli.current" campaign="download" content="buttonlink" %} [<img alt="Get Pachli with Obtainium" width="207" height="80" src="/assets/download/obtainium-badge.png"/>](obtainium://add/github.com/pachli/pachli-android-current)

New releases appear on GitHub immediately.

There is typically a 12-24 hour delay before a new release is available on Google Play. Releases are made available to 100% of the users immediately.

Pachli Current is not available from F-Droid as the F-Droid repository does not support these sorts of releases ([#1153](https://gitlab.com/fdroid/fdroidserver/-/issues/1153)).

# GitHub signing certificate hash

GitHub releases of Pachli and Pachli Current are signed with a certificate with the following SHA-256 hash:

<pre style="overflow-wrap: anywhere; white-space: pre-wrap">
F0:CD:1F:5C:FF:49:9B:E4:C2:12:8C:11:52:FB:91:9D:C2:48:15:15:2A:99:03:C9:09:4F:F8:40:5F:E1:31:C3
</pre>

You can use [App Verifier](https://github.com/soupslurpr/AppVerifier/tree/main) to verify the GitHub APK was signed with this certificate. 

# Source code

The source code is available on GitHub, at [https://github.com/pachli/pachli-android](https://github.com/pachli/pachli-android).

# Previous releases

Previous releases can be downloaded from:

- [Pachli GitHub Release page](https://github.com/pachli/pachli-android/releases).
- [Pachli Current GitHub Release page](https://github.com/pachli/pachli-android-current/releases).

---

Google Play and the Google Play logo are trademarks of Google LLC.