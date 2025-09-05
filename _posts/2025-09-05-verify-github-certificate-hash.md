---
layout: post
title: "Verifying GitHub releases with a certificate hash"
date: "2025-09-05 09:00:00 +0200"
categories: pachli
---
If you install Pachli or Pachli Current using the GitHub releases you can now verify the installation file (`.apk`) has not been tampered with.

Pachli and Pachli Current GitHub releases are always signed with a certificate with the following hash:

<pre style="overflow-wrap: anywhere; white-space: pre-wrap">
F0:CD:1F:5C:FF:49:9B:E4:C2:12:8C:11:52:FB:91:9D:C2:48:15:15:2A:99:03:C9:09:4F:F8:40:5F:E1:31:C3
</pre>

You can use [App Verifier](https://github.com/soupslurpr/AppVerifier/tree/main) to verify the installation file is signed with this certificate.

This information has also been added to the [download](/download/) page and to the [@pachli@mastodon.social](https://mastodon.social/@pachli) profile. 