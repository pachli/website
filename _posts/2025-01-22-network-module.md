---
layout: post
title: "Could Pachli's network module be a separate library?"
date: "2025-01-22 23:00:00 +0200"
categories: pachli
---
I received the following question as a DM on Mastodon.

> In your sources you have separated network module. Did you think about publish it as standalone library? Can you help me to understand why all ActivityPub applications developers didn't separate their network modules?

The reply doesn't easily fit in to 500 characters, so I thought it was a good fit for the blog.

<!--more-->

# Publishing a standalone library

Pachli's network module is the code under [`/core/network/`](https://github.com/pachli/pachli-android/tree/main/core/network). 

There are three primary reasons why Pachli's network module is not a separate library for other clients to use.

## 1. Suitability of the code for other clients

Pachli's network module has two main components.

The first component contains the data types used by the Mastodon server ([`core/network/model`](https://github.com/pachli/pachli-android/tree/main/core/network/src/main/kotlin/app/pachli/core/network/model)).

Pachli's implementation of these types is both incomplete and over-broad.

It's incomplete because there is some data Pachli does not use. For example, Pachli does not implement the [streaming](https://docs.joinmastodon.org/methods/streaming/) API so none of those types are implemented. 

It's over-broad because Pachli also supports responses from (some) non-Mastodon servers with extensions to the Mastodon API response types. Those would be unhelpful to a project needing only a Mastodon client API.

The second component covers network transport and data encoding. Pachli uses [Moshi](https://github.com/square/moshi) for JSON encoding and [Retrofit](https://square.github.io/retrofit/) for network transport, and the network module contains code using and extending those libraries ([`core/network/json`](https://github.com/pachli/pachli-android/tree/main/core/network/src/main/kotlin/app/pachli/core/network/json) and [`core/network/retrofit`](https://github.com/pachli/pachli-android/tree/main/core/network/src/main/kotlin/app/pachli/core/network/retrofit)).

Other clients may legitimately want to use different libraries ([kotlinx.serialization](https://kotlinlang.org/docs/serialization.html), [Ktor](https://ktor.io/), etc).

## 2. Current state of the code

The networking code is currently in a significant state of flux, as it migrates from two different ways of representing a network response to a third.

Tusky (the project from which Pachli is derived) originally used Retrofit's [`Response`](https://square.github.io/retrofit/2.x/retrofit/retrofit2/Response.html) type to represent network responses.

Then, one of the Tusky maintainers wrote [`NetworkResult`](https://github.com/connyduck/networkresult-calladapter).  The Tusky project started migrating to this type, but never completed the migration.

I disagree with aspects of the `NetworkResult` design (for one thing, it doesn't model response headers, for another it uses Kotlin's `Result` type which relies on exceptions), so I'm fixing it with the [`ApiResult`](https://github.com/pachli/pachli-android/blob/main/core/network/src/main/kotlin/app/pachli/core/network/retrofit/apiresult/ApiResult.kt) type, and I'm migrating all uses of `Response` and `NetworkResult` to `ApiResult`.

> As an aside, I'm preparing a series of blog posts to discuss Pachli's `ApiResult` type and the wider topic of error handling in Android applications.

So if another project tried to use Pachli's network code they'd find three different types with no obvious reason why a particular API call uses one type over another.

## 3. Additional support burden

Given those two issues there's no sense in releasing Pachli's networking module as a separate library.

However, even if they were solved, providing the module as a separate library for third party projects to use would add an additional support burden to the Pachli project while not directly furthering the project's aims.

As a separate library -- assuming it attracted any use outside the project -- it would be subject to bug reports and feature requests that may be out of scope for the Pachli project. Dealing with those would take time the project doesn't really have at the moment.

It also complicates the process of developing Pachli. At the moment if Mastodon introduces a new API and I want to support it I can do so directly. If the network module was a separate library I would first have to update the library, then release a new version, then configure Pachli to use the new version, and so on.

There are mitigations for this; [Import local gradle projects as modules \| by Dima Brody \| Medium](https://medium.com/@dima.brody/import-local-gradle-projects-as-modules-413a0e5aa0fa) is a good overview of some of those solutions.

But again, it's additional effort the project can't spare.

# Other networking modules for Mastodon clients

Obviously, I can't speak for why other Android Mastodon clients haven't published their networking modules as standalone libraries, although I suspect the reasons I covered in the previous section apply to them too.

If you are looking for a standalone client library you should investigate [BigBone](https://bigbone.social/). BigBone is:

> A Mastodon Client Library for Java and Kotlin
>
> [...]
>
> With BigBone, you can seamlessly build applications that utilize Mastodon’s functionalities, from fetching timelines and notifications to posting updates and interacting with users. Our user-friendly API allows you to focus on crafting your application’s unique user experience without getting bogged down in the complexities of Mastodon’s API.

I haven't used it myself, but after reading some of the code to familiarise myself with it it appears to be well written and regularly updated.

It is a "batteries included" client, by which I mean it handles JSON deserialisation and network transport for you, you do not need to provide your own libraries for those.

For some projects this will be a positive, for others a negative.

# To summarise

Pachli's networking module is quite specific to Pachli's use case and undergoing a large refactoring.

Making it suitable for other projects would be a lot of work with no clear benefit to the Pachli project, and it's not clear it would be beneficial to other projects.

Java/Kotlin projects looking for a batteries-included Mastodon client library should definitely investigate [BigBone](https://bigbone.social).

Huh. That is less than 500 characters...