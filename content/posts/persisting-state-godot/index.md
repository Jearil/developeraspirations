+++
title = 'Persisting State in Godot'
date = 2023-11-14T17:00:00-08:00
categories = ['dev']
tags = ['gamedev']
author = 'Colin'
image = 'title.png'
+++

I haven't settled on my finished game idea, but I've been busy exploring systems that I want to create in the meantime. While I still want to clean up my [bridge]({{< ref "/posts/making-bridges" >}}) system, that success has propelled me into wanting to design some other systems that I can generically apply to any game that I want to make. Among those systems are **Dialog**, **Interactions**, **Inventory**, and **Persistence**. That last system is the one I would like to talk about today.

## What is persistence?

Originally when I was thinking of persistence what I was really thinking of was saving and loading a game. Essentially, in most games we need to save progress before the player quits the game and restore that progress when they resume. This is true for any game that isn't short with no progression. Having not made a game before and not having done this in Godot either, I wanted to find out what the standard way of saving/loading game states was. Most of the YouTube tutorials people have posted are terrible. They just generically talk about how you can store data with Json and restore it using the same. I've been programming for 20 years; I definitely know about Json and how to save and restore generic data. But the issue is more about what data and how do we restore it? There's a [video](https://youtu.be/_gBpk5nKyXU?si=f_6ppxBq1ECmdyun) by Jason Lothamer that is better than most and goes into some of those things.

Let's take a simple example. Say I have a game with a character, a tree, and a treasure chest. The character can walk around and possibly open the chest. Maybe there's something inside that the character can gain. They could also cut down the tree. When saving the game, I need to be able to do several things:

1. Save the character's current position (their x, y coordinates)
2. Save the open/closed state of the chest
3. Save the character's inventory in case they got something from the chest
4. Save the non-existence of the tree if cut down
5. Save what scene the character is in; in case the game has multiple rooms with multiple scenes.

There are a few different types of data that I need to collect now. The character's position, the chest's open/closed state, and the tree are all scene specific data. There might be other scenes that need different data, and we'd have to save those as well. Having scenes act as a key for that data sort of name spaces it so we don't just have a generic pile of storage keys that will get confusing. The tree, however, is a weird case in which we actually need to track when it's removed from the scene so that when we restore the scene from disk, we remove it again.

We also have some global information. The character's inventory will travel with them across scenes and should be stored globally. Also, which scene (room) the character is in would need to be stored globally as you can only really be in one scene at a time. Assuming we're storing everything in a tree (probably Json or protobufs), we'd have data looking like the following:

```json
{
    "global" : {
        "inventory" : [
            5 // key for a rock that was in the chest
        ]
     },
    "currentScene" : "res://scenes/world.tscn",
    "sceneData" : {
        "res://scenes/world.tscn" : {
            "chestOpened" : true,
            "treeExists" : false,
            "player" : {
                "posX" : 30,
                "posY" : 25,
            }
        }
    }
}
```

So here we have some global data which includes the player's inventory. We also have a top-level item for the current scene, so we know when the user selects load from the main menu what scene to load. Finally, we have some scene data which contains data about the current scene such as if the chest is open, the tree exists, and the player's position.

Ideally then, on load we could perform a scene transition loading up the scene from `currentScene`. Once that scene is loaded, we could pass in the `sceneData` from that scene and feed it into some sort of save/restore component on the scene. It would be responsible for changing the variables of the various objects on the scene or removing them from the scene tree all together.

## Persistence as part of the game

Saving and restoring state isn't just for save games though. We need to do this actively even while the game is running. It doesn't have to be to disk each time something changes as that may cause a lot of jank due to IO, but we at least need an in-memory copy of the game's current save state. Imagine if you were in that scene where you opened the box and cut down the tree, then you leave to go to a different room. In Godot, and most engines really from what I understand, you load up the new room/scene/level and unload the old one to save memory. However, all those properties were in memory just while that scene was loaded. When you change to another room, the state of that chest is lost unless you save it upon leaving and restore it up on entering again.

This means that to have a game where the game state itself stays consistent between scenes, we need to build in a persistence system very early on in the game's lifecycle. Without it, there's no consequences to our actions. Saving and loading, even if not to disk, is required just for normal gameplay. Designing this system early and making it easy to use, consistent, and fast is important. Previously I was going to work on a dialog system that would show you logs of what dialog options you had viewed in the past. But honestly, to do that, you need a good persistence system first. It's a foundational element to any game.

## Jason's Library

Jason from the above video included a [demo project](https://github.com/jhlothamer/save_and_load_demo/tree/godot4) that has saving/loading library attached to it. Unfortunately, it has not been updated to Godot 4 and a bunch of the functions he's called has changed since then. I'm not a fan of how it uses "magic strings" to do persistence. You need to specify which fields will be persisted as just strings of the names in each Node you want to save data too, and that doesn't sit well with me. Also, his code is all GDScript and I'm concerned on how it would translate to my C# development. So, while I won't be using his code directly for persistence in my game, I will be reading through it and heavily using the ideas in it for a way to tackle persistence and recreation of data objects.

## Plugin

Jason did another thing in his demo project of making his code a plugin. [Jace Varlet](https://www.youtube.com/@jembawls) in his [video](https://youtu.be/6BsPkI4pCOI?si=BFC1jLJ7uZF94N2L) about his dialog system (which I will also take inspiration from), he also designed it as a Godot plugin. I do think it's probably important that I start learning the Godot plugin system so I will be doing that for the persistence system I build. I'll do my best to make it generic enough that it can be published externally from my game so that others could use it, but first I must design it.

That's it for now. Hopefully the next time I update I'll have some progress on this persistence system and maybe a demo to show it off.
