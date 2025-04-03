---
layout: post
title: "Pachli Current releases on GitHub / Obtainium"
date: "2025-04-03 09:00:00 +0200"
---
Pachli Current is now available on a dedicated GitHub release page. If you don't use Google Play you can still install, test, and report bugs with Pachli Current.

> Pachli Current is the pre-release variant, with new features and bug fixes that benefit from wider testing. Installing Pachli Current and [reporting any bugs](https://github.com/pachli/pachli-android/issues/new/choose) you find is a very useful way to contribute to the project.

You can install Pachli Current from GitHub manually, or you can install Pachli Current using [Obtainium](https://obtainium.imranr.dev/).

<!--more-->

# Using Obtainium

## From a link

If you are viewing this page on the device with Obtainium installed then the following link should start Obtainium with the correct configuration.

After Obtainium has started tap the **Add** button to finish installing Pachli Current.

> <a href="obtainium://add/github.com/pachli/pachli-android-current">Tap this to install Pachli Current with Obtainium</a>

## Manually

You can configure Obtainium manually if the link did not work or you are not reading these instructions on the device with Obtainium installed.

### If you are already familiar with Obtainium

1. Add a new app
2. Enter `https://github.com/pachli/pachli-android-current` as the **App source URL**.
3. That's it

### If this is your first time using Obtainium

Open Obtainium, which should show the list of Obtainium-managed apps. There will be one app, Obtainium itself.

<img alt="" src="/assets/posts/2025-03-xx-obtainium/open-obtainium.png" class="shadow">

Tap the **Add App** button at the bottom of the screen. The **Add App** screen will appear, with two fields.

<img alt="" src="/assets/posts/2025-03-xx-obtainium/add-app.png" class="shadow">

In the **App source URL** (first) field enter the following exactly as it appears below:

```
https://github.com/pachli/pachli-android-current
```

Additional options may appear when Obtainium determines Pachli will be downloaded from GitHub. You can ignore those options.

Tap the **Add** button next to the **App source URL** field.

You should see this screen.

<img alt="" src="/assets/posts/2025-03-xx-obtainium/success.png" class="shadow">

The precise characters after **pachli-current-...** will vary depending on Pachli Current release.

You can then go back from this screen, and Pachli Current will appear in the list of apps managed by Obtainium.

<img alt="" src="/assets/posts/2025-03-xx-obtainium/new-app-list.png" class="shadow">

You have finished. Pachli Current is now installed. Obtainium and Pachli will periodically check for new updates and inform you when they are available.

# Installing from GitHub

To install Pachli Current from GitHub:

1. Open https://github.com/pachli/pachli-android-current/releases/latest
2. From the **Assets** section download the file that ends `.apk` to your device.
3. Open this file on your device.

Pachli Current will periodically check for updates and you will be prompted to install them.

> **Understanding the filename**
> 
> The Pachli Current filename on GitHub has the following sections:
>
> `Pachli_[releaseVersion]_[versionCode]_[commitRef]_[variant]_release-signed.apk`
> 
> where:
> 
> - `releaseVersion` is the base version of Pachli this is built from
> - `versionCode` is the Android version code for this release
> - `commitRef` is the specific Git commit reference this release was built from
> - `variant` is always `orangeGithub`; `orange` means this is Pachli Current, `Github` means this is the build for GitHub
