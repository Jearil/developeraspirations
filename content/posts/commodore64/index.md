+++
date = '2026-02-28T11:04:17-08:00'
draft = true
title = 'Commodore 64'
+++

I came across an advertisement over the holidays about the [Commodore 64 Ultimate](https://www.commodore.net/product-page/commodore-64-ultimate-basic-beige-batch2). I was amused at the time and thought, while neat, it wasn't worth getting. They had a sale at the time that if you bought it at any point in 2025 it would cost $50 less.

Ultimately, I could have saved $50.

It was in the back of my mind and I kept thinking about it. Compared to anything modern, the Commodore 64's hardware is obviously underpowered. With a 1 Mhz MOS 6510 and 64kb of ram, no modern OS could run on it. And yet, that limitation is intriguing.

![The Commodore 64 Ultimate](commodore64.png)

I never had a Commodore 64 growing up, though I was exposed to them. In my Aunt's basement there was one with a few games. At school, we used C64s to learn how to type before DOS and Windows eventually took over. I remember having an Intellivision, and later on an NES, Genesis, and eventually a Windows 3.11 PC. However, the Commodore was always a fascinating machine to me, with its esoteric commands for loading programs and the `BASIC` prompt that invited one to not just run programs, but to write them as well.

There was a book I remember using when I was young that had a bunch of `BASIC` programs in it. I remember having my mom type in a program from that book which took hours. Or maybe less. I was young, so 10 minutes probably felt like hours. In the end, it would create a picture of a house that had a chimney with smoke coming out of it. The smoke was animated and I was captivated that the words she typed somehow made an animated house. I don't think it was a Commodore 64, but it was some early computer that could run `BASIC` that you typed in, and lost all data when the computer was turned off. It was one of those early experiences that caught my imagination and made me want to work with computers for the rest of my life.

Today, computers and software are so advanced that they are starting to write themselves. Young people who have had access to computers often use them as utilities, understanding less about their inner workings than those of us who came of age during the 80s and 90s. It makes sense, you don't need to know as much about them to use them effectively today. It's similar to how the generation before me really understood their cars, how they worked, and how to fix them. In my generation it became less common, and is more rare today. When a technology is new, you need to know a lot about it to use it. Later, it gets streamlined and becomes easier to use and more commodified, and the required knowledge goes down.

Having access to a Commodore 64 in 2026 is an interesting proposition, however. You're given the `BASIC` prompt. You have to know commands to load things. Programming a C64 requires patience and knowledge. You have to fit things in a small amount of memory. I'm sure you can vibe code your way to something, but assembly is tricky, and `BASIC` is slow. Living with such constraits makes it more interesting than the modern computers where we can brute force solutions with enough CPU, RAM, and GPU. There's an elegance in conforming to those constraints.

In that regard, I've become interested in what was possible in 1982 using advancements in software that we've gained in the last 40 years. What could have been possible if you had only access to hardware of the C64 era, but with today's software tools and knowledge? That question led me to an interesting project: **Vision Basic**.

![Vision Basic comes in an actual physical Box!](vision_basic_box.jpg)

## Vision Basic
[Vision Basic](https://visionbasic.net/) is a fascinating project written by Dennis Osborn and released in 2022. Its purpose is to create a custom version of `BASIC` which compiles to native code, enabling them to run faster. Such compilers existed back in the day in the form of the [Blitz](https://en.wikipedia.org/wiki/Blitz_BASIC), however **Vision Basic** also allows you to combine `BASIC` with assembly, using custom functions along with quality of life improvements like textual tags in place of line numbers for goto references. The whole thing runs on an actual Commodore 64 and is its own programming environment, which is drastically different to use compared to our modern systems.

Purchasing **Vision Basic** was an interesting experience. It's a piece of software that you can only buy physically. It comes in a physical box with a physical manual, and the software itself comes in a 5.25" floppy! Though there's also a USB included in case you don't have a floppy drive, as  most people do not. It's so odd to recieve software in a physical box with a large physical manual (over 350 pages). While there is a way to get a digital download of **Vision Basic**, you can't actually get a copy of the manual digitally; it's only available in print. I suspect it's to reduce copying, but I also think it's a good idea to preserve that feeling of how software was distributed back in the 80s and 90s.

![The floppy is real, and would work if I had a drive](vision_basic_disc.jpg)

The manual is fascinating. It begins by describing how Vision Basic came to be originally in the late 90's as a personal project that Dennis worked on while sitting in hopsital waiting rooms, having been diagnosed with cancer. He had a lot of time on his hands and a notebook, so he wrote portions of it during that time. He stopped working it it after getting married and having children in the early 2000's, but picked it up again in the mid-teens. He describes wanting to use his favoriate language, `BASIC`, but have it run faster like assembly. And the piece of software that he made is remarkable. If you yourself pick up a Commodore 64 Ultimate and are interested in programming it, I would recommend giving it a go. Just the novalty of packaged software with a real manual is itself a treat, but the language and compiler itself are quite extraordinary.

## Programming The Commodore 64

As I've stated, part of my fascination with the Commodore 64 in 2026 is as a programmer. It is something that I think I can appreciate now so much more than I would have had I owned one as a child. Having been a programmer for over 20 years, that experience makes the device's limitations more interesting to me than they would have been when I was younger. Beyond **Vision Basic**, the Commodore 64 comes with two main ways to program it that were included with the device itself. The first is of course `BASIC`, which loads every time you turn it on. The second is MOS 6502 assembly, a much more difficult yet performant way to code.

When you bought a Commodore 64, it came with a fairly large spiral-bound user manual. That manual not only contains the operating instructions for the computer but also a primer on `BASIC` programming. It does not touch on assembly, being primarily intended for home use. However, a similar book was created that one could buy called *Commodore 64 Programmer's Reference Guide*. Unfortuantely these are rare and often in poor condition. However, a wonderful individual in Scotland who has a site called [Pickled Light](https://pickledlightprojects.com/) has recreated the *Programmer's Reference Guide* and *User's Guide* in a printable PDF along with [instructions](https://pickledlightprojects.com/documents/c64-guides/) on how to have the professional printed for relatively little cost. He reformatted all of the original text in order to be printable. I did this myself and the results are pretty remarkable.

![The Commodore 64 Programmer's Reference Guide from Pickled Light printed via Lulu](c64_Programmers_Guide.jpg)

All of this old tech and programming practices are fascinating to someone who didn't experience them as the main way of interacting with a computer. I don't know what types of programs I plan to make for the Commodore 64, or if I'll even finish any that I start, but I do know that I'll find it interesting to partake in the journey of learning about it.