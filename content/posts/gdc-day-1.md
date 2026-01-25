+++
title = 'First Day at GDC'
date = 2025-03-17T22:10:00-07:00
categories = ['blog', 'gdc']
tags = ['gamedev']
author = 'Colin'
+++

My first day at GDC was interesting and exhausting.

Like many conventions with panels, there's always a mix of some that are boring or unhelpful, and some that are actually interesting and which provide something of value. Today was no exception. I'll go through the panel part of my day first and then talk about other stuff after that.

# Panels
The first part of the day was going to a variety of panels. I did have a brief break in the middle to go back and get a non-caffeinated  energy drink (they exist), and another break after the last panel, but it was pretty go-go-go most of the day. Here's a breakdown of the panels I went to.

## Unity Keynote
Honestly, I'm not even sure why I went to this panel other than it was going to talk about unreleased stuff. I played with [Unity](https://unity.com/) a while ago and didn't really like it all that much. When they started doing stupid anti-dev things, I had a good reason to never really touch it again. I ended up using [Godot](https://godotengine.org/) which [I love]({{< ref "/posts/learning-godot" >}}), so a Unity presentation wouldn't have much for me.

And that was true.

They talked about some fancy new rendering things they're doing. It looks like they're trying to more directly compete with Unreal for high end graphics which doesn't appeal to me as a solo dev. They also talked about integrating AI into their editor (like everyone is doing), and honestly that wasn't very interesting either. There were some things relating to multiplayer games that I did think was neat, but since I'm not going to be programming in Unity any time soon it was also not helpful to me.

The line was long, and I got there early so I had a decent seat, I was just bored the whole time. Not a great start, but things did improve.

## You Are Not Alone
The rest of my panels were all part of the Independent Games Summit which is the one that I registered for. The first was about solo devs. At first, I didn't really like this panel either. It started with someone who joined a big gaming company, made a bunch of mistakes, and talked about how they managed that and their imposter syndrome. I do have imposter syndrome relating to game development, but not because I work for a big game company. Mainly it's because I *don't* work for a big game company. So I didn't really relate to that speaker.

Luckly, there were 2 more speakers. The next talked about their game which was designed after 1980's and 90's adventure games. The first screenshot might as well have come from Sierra OnLine. It was beautiful. It's called [The Crimson Diamond](https://store.steampowered.com/app/1098770/The_Crimson_Diamond/) and she talked about how even though she was a solo developer, she still had a lot of help. People like play testers, her audio guy, people who ported her game to other systems, and people who made the game engine. Even though they didn't write the game themselves, they were still involved so it showed that even as a solo there's still other people. That was kind of neat.

She also talked about the benefits of starting a community and promoting via dev streams on twitch and discord. Something that might be difficult for me to do, but maybe something to look into as well.

Finally there was something who wrote [Potions: A Curious Tale](https://store.steampowered.com/app/378690/Potions_A_Curious_Tale/) and she had a lot to share about her process and the mistakes that she made. It seemed like she was heavily focused on promoting which did help her get seen, but also ended up getting her some hate for the way that she did it.

She had some pretty good tips that I took notes on which I'll try to digest and figure out how I can apply later on.

## How to Plan for Audio as a Developer
This talk was actually really interesting. I haven't done any audio work and while I'm not an expert after having seen this panel, it does give some ideas on how to approach things. The talk was mainly in the context of hiring an external sound engineer and how to work with them, something I probably won't be able to afford to do. However, it also did give some suggestions on how to do some of it on your own and some of the tools and practices used in sound design.

I have a giant page of notes and a ton of tips about the different kinds of sounds in a game along with some of the processes used to modify sounds. This is another area where I think just rereading my notes and digesting it might yield something positive. At the very least, I have the names of some tools and frameworks I can look into to better incorporate sound.

## Funding a Sustainable Cooperative Indie Studio in the Apocalypse
This one is probably tied with Unity for my least favorite panel. It was about worker-owned game studios and how to survive, but it did not vibe with me at all. I did appreciate that they started by listing a bunch of privileges that their coop enjoyed such as: a decade in the industry, connections with investors, a huge network of people to lean on, etc. Right off the bat it was exactly the opposite of where I'm at. I have no connections in the industry, no connections for funding, and I haven't been doing this for very long.

The second part of the talk by a profession from a university in Seattle was better, but still I left it early to make it to my next panel. And I'm super glad I did.

## Developing at 5mb per Year. The Making of 'Animal Well'
This panel was just a super cool talk about [Animal Well](https://store.steampowered.com/app/813230/ANIMAL_WELL/). Billy Basso was really fun to listen to and seemed like a really cool geek. He talked about the tools that he used (which were super low level... basically Visual Studio 2019, Aseprite, Reaper, and Notepad), and some of the tricks he used to develop the game. It was interesting that the game is so small because he built his own game engine and used no libraries. It was all just straight C++. He talked about his level editors and showed both of them off, along with how he did lighting, animation, water, the asset pipeline, and how one of his rules for the game was that the binary would have no text in it (everything was stored as binary). He even wrote his own encryption system where the player's inputs were used as part of the decryption key for some assets to prevent data mining.

Overall, it was just a really cool and inspiring talk. The guy next to me said it was just Billy getting to go up and flex for a half hour, and that might be true, but also warranted. The tech he did was pretty impressive. I hope he makes more stuff in the future.

# GDC Nights
There's this event called GDC nights which is supposed to be the official sort of after-party. I was both looking forward to it, but also a bit intimidated by it. It's supposed to be for networking and meeting new people, which I'm traditionally not the best at. I've also been feeling more impostor syndrome and struggling finding people. I ended up making a bluesky post about it.

<blockquote class="bluesky-embed" data-bluesky-uri="at://did:plc:gie4wy6vo4ixac455zwxapw6/app.bsky.feed.post/3lkmippmnak2b" data-bluesky-cid="bafyreihug6odgdeb6xdxm4lm72eilw2hy5gqlye4gdelqu6pirzzts4qga" data-bluesky-embed-color-mode="system"><p lang="en">I sometimes hesitate to call myself a #gamedev because I haven&#x27;t released a game and my day job is android programming at Google which is not making games. At #GDC alone as an independent dev. Hoping to try to meet other devs tonight though not sure where to start. I&#x27;ll be at GDC nights.</p>&mdash; Colin ➡️ GDC (<a href="https://bsky.app/profile/did:plc:gie4wy6vo4ixac455zwxapw6?ref_src=embed">@jearil.bsky.social</a>) <a href="https://bsky.app/profile/did:plc:gie4wy6vo4ixac455zwxapw6/post/3lkmippmnak2b?ref_src=embed">March 17, 2025 at 6:17 PM</a></blockquote><script async src="https://embed.bsky.app/static/embed.js" charset="utf-8"></script>

<blockquote class="bluesky-embed" data-bluesky-uri="at://did:plc:gie4wy6vo4ixac455zwxapw6/app.bsky.feed.post/3lkmippmvzs2b" data-bluesky-cid="bafyreihtdksiatd2tgowcmdz25npifywvobtybjyh3zzs7u3jx4pegfxja" data-bluesky-embed-color-mode="system"><p lang="en">If anyone I don&#x27;t know (or do know honestly) who is at #GDC and wants to meet someone new to chat with I&#x27;d love the opportunity. Otherwise, I&#x27;ll work myself up to be as extroverted as I can!</p>&mdash; Colin ➡️ GDC (<a href="https://bsky.app/profile/did:plc:gie4wy6vo4ixac455zwxapw6?ref_src=embed">@jearil.bsky.social</a>) <a href="https://bsky.app/profile/did:plc:gie4wy6vo4ixac455zwxapw6/post/3lkmippmvzs2b?ref_src=embed">March 17, 2025 at 6:17 PM</a></blockquote><script async src="https://embed.bsky.app/static/embed.js" charset="utf-8"></script>

And I ended up getting a reply

<blockquote class="bluesky-embed" data-bluesky-uri="at://did:plc:btq6w5h3el65eogojxjm7wxd/app.bsky.feed.post/3lkmjf6tl7c2o" data-bluesky-cid="bafyreigcgvfnfbmvdl4hmp3ekfqccda7b7vtpou4n5nbof5wydp67agxle" data-bluesky-embed-color-mode="system"><p lang="en">Fellow former mobile dev here! Happy to meet up, DM if you want</p>&mdash; Aaron Hedquist ➡️ GDC (<a href="https://bsky.app/profile/did:plc:btq6w5h3el65eogojxjm7wxd?ref_src=embed">@aarhed.bsky.social</a>) <a href="https://bsky.app/profile/did:plc:btq6w5h3el65eogojxjm7wxd/post/3lkmjf6tl7c2o?ref_src=embed">March 17, 2025 at 6:29 PM</a></blockquote><script async src="https://embed.bsky.app/static/embed.js" charset="utf-8"></script>

I met up with Aaron who is a dev at Polyarc (They made [Moss](https://store.steampowered.com/app/846470/Moss/) for VR which is a pretty big name in the VR field) who is also at GDC alone and got to chat and hang out for the evening. He showed me his personal indie game that he's working on that looked really cool, and we watched an Improv show together.

It was nice to have someone to talk to and share a few things with. Maybe we'll hang out a little more later this week.

# Conclusion
I also randomly met someone on my team at my day job at the Google booth. That was neat. I also got some swag in the form of socks from the [JetBrains](https://www.jetbrains.com/) booth. I've always loved their products.

It's getting late and I'm exhausted. I'll try to post again tomorrow, but it might be rough. Overall
