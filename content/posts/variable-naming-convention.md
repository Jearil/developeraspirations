+++
title = 'Variable Naming Convention on Android'
date = 2023-10-07T19:30:00-07:00
categories = ['dev', 'android', 'opinion']
author = 'Colin'
+++

This article will focus mainly on the Java and Kotlin programming languages. I understand other languages have their own coding styles and you should generally conform to the style of the language first.

I started working on Android around 2014 while I was working at [LinkedIn](https://www.linkedin.com). For the most part at the time, a lot of Android code is just like any other Java code and generally the Java conventions are applicable to code done for Android. There was one thing though that was done both at LinkedIn and Facebook that never made sense to me as far as variable naming conventions go, and that is the single character prepends to variable names.

You see, for the [AOSP](https://source.android.com/)(Android Open Source Project) they have a set of [style guidelines](https://source.android.com/docs/setup/contribute/code-style) for anyone who wants to contribute to the Android OS itself. One of the guidelines revolves around [field name conventions](https://source.android.com/docs/setup/contribute/code-style#follow-field-naming-conventions). Specifically, it imposes a few general rules for naming your variables.

* Non-public, non-static field names start with an m.*
* Static field names start with an s.
* Other fields start with a lower-case letter.
* Static final fields (constants, deeply immutable) are ALL_CAPS_WITH_UNDERSCORES.

I personally disagree with this style myself as it's pointlessly close to [Hungarian Notation](https://en.wikipedia.org/wiki/Hungarian_notation) which incorporate aspects of the variable such as type or visibility into the variable name itself. But the project was started by someone who likes that sort of thing I guess, and I can understand wanting to keep doing it for consistency.

What I don't understand is why any other project that's not the AOSP would pick it up. LinkedIn and Facebook both used an m before a non-public, non-static field and used an s for static fields. I remember asking why it was done that way and they cited the AOSP code style guidelines. But that would be like adopting the Linux Kernel coding style guidelines for any code you write that runs on Linux. It really makes no sense to impose the style guidelines for a different project on your own project. I understand using the general Java coding style guides, but the AOSP ones aren't very good and really don't make sense for most projects.

Recently, one of my coworkers started writing code that would contain 2 variables whose name was the same other than one was prepended with a underscore _ . If you had something like `widget` you might also have something called `_widget`. The main difference between these two variables is that the one named `widget` is publicly accessible (and mostly immutable) while the `_widget` is a private variable that you can mutate which is reflected in the pubic one. This is in Kotlin, so it's not a standard naming convention [**\[See update below\]**](#update). The reason why my coworker did that was because they read an example piece of code that did it that way. I think this is probably the same way that the AOSP naming convention made its way into so many other projects. Someone else did it, probably from some official seeming source, so it must be the right way to do it.

Naming variables the same but with a `_` before it is confusing though. When I'm reading the code or extending it, which do I use? They can both be read basically the same way, only the `_` one can be modified. They have a different purpose, and therefore should have a different name. Just using the `_` symbol adds ambiguity to the meaning and usage of the variable, increases the ability for a dev reading the code to be confused, and doesn't inherently convey any meaning. What does convey meaning are words.

One of the reasons why my coworker preferred to use the `_` to differentiate the variables is because it is shorter. They would have to type less. One truth in all programming is that [Code is read much more often than it is written](https://devblogs.microsoft.com/oldnewthing/20070406-00/?p=27343). Optimizing for speed of writing is the wrong thing to optimize for. Always optimize for reading the code. This of course applies to proper uses of comments, structure, and variable names. It's not good enough to just make code that does the thing you want it to do. You want to write code that's easy to read, inherently understandable, and easy to refactor and change. Prepending a `_` in front of a variable name to give it a different meaning does not add to readability but rather detracts from it.

Overall, code style guidelines are a great thing to have. Almost all languages have their own and I would recommend following the guidelines for that specific language. If you plan to deviate in your own project, make sure that there's a good reason and that your changes make sense and improve readability. Hungarian Notation adds noise, `_` to the start of a variable (in Java or Kotlin; I understand it has a specific meaning in some languages like Python) adds no context or value, and `m` and `s` prepends are duplicates of information already in your code.

## Update
I was actually looking more into the `_` being used as part of a variable name in Kotlin and despite what I thought, it's actually in the Kotlin Coding conventions under [Names for backing properties](https://kotlinlang.org/docs/coding-conventions.html#names-for-backing-properties) which is how my coworker was using it. Basically if you have 2 properties that are conceptually the same but one is a public API and the other is an implementation detail, the underscore in the name is used for the implementation detail. I was so used to `_` not being part of variable names in Java I didn't look it up fully for Kotlin.

I still stand by sticking with variable naming conventions and not using Hungarian Notation. Also AOSP style guidelines should not be used outside of the Android Open Source Project itself.
